# Windows で DockerDesktop じゃない Docker



DockerDesktop ってGUIだからいやなんだよねってことでCUIの docker を使えるようにする



素で `sudo apt install docker` しても動かないっぽいのでちゃんと調べたときの備忘録

結論から言えば、コマンドをコピペするだけで使えるようになる



- ほとんど引用している参考記事

https://zenn.dev/taiga533/articles/11f1b21ef4a5ff



## 前提

以下の手順でDockerDesktopをいったん止める

- Docker Desktop を開いてSettings(歯車マーク)から`Start Docker Desktop when you log in`のチェックを外す（起動時にDockerDesktopを起動するかのチェック）

- > Docker Desktop をタスクバーから `quit docker desktop`を選択しシャットダウンする

  と参考記事では言っているが、普通に閉じればいいような気がする



## インストール

[公式ドキュメントのインストールページ](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)を参考にUbuntuにDocker Engineをインストールする



ただ、見るのがめんどいなら以下のコマンドをコピペすればOK(コピペして打てるように `$`は先頭に入れていない)

```bash
sudo apt update

# インストールに必要なものをインストール
sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# GPGキー追加
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# dockerのパッケージリポジトリをaptに追加
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# dockerEngineのインストール
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io

# docker-composeのインストール
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# docker daemonの起動
sudo service docker start
```



ちなみに、最後のコマンドの

```bash
$ sudo service docker start
```

は docker daemon を起動しているだけっぽいので、インストールではない





## docker daemon を自動起動するように設定する

先ほどのコマンドで docker daemon を起動していたが、ログインするたびにそれを打つのはめんどくさいので、自動起動できるように設定する



> WSL2ではsystemdがPID1で起動しないので
> WSL2起動時にdocker daemonを起動させるのは難しいです。
> 一応systemdをwsl2で動かすこともできますがsystemdの動作が不安定なのでおすすめしません。
> そのためここではwsl使用時に自動でdocker daemonを起動する方法を紹介します。

↑？？？



言ってる単語がよくわからない

いったいなにを言ってるんだ



- https://qiita.com/ko-zi/items/949d358163bbbad5a91e



↑の記事を参考に設定することにする



docker を自動起動するためには sudo が必要なので、そのまま .zshrc とかに書いても扱えない



そのため、`service docker start` コマンドをパスワードなしで行うために `visudo`でsudoまわりを編集する



```bash
# visudo で sudoers を編集
$ sudo visudo
```

編集する内容は以下

```bash
# docker deamon auto up
matumoto ALL=(ALL:ALL) NOPASSWD: /usr/sbin/service docker start
```



次に、.zshrc に以下を記述して docker が動いていなければ動かすようにする

```bash
$ vim ~.zshrc


#追記
echo $(service docker status | awk '{print $4}') #起動状態を表示
if test $(service docker status | awk '{print $4}') = 'not'; then #停止状態
        sudo /usr/sbin/service docker start #起動
fi
```

