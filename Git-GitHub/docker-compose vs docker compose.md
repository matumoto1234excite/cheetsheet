# docker-compose vs docker compose

docker-compose と docker compose には違いがあるっぽい



## なにが違うのか

もともと使われてたのが docker-compose の方



V2 として Go で実装されたのが docker compose とのことらしい（V1 は docker-compose）



- [公式ドキュメント](https://docs.docker.com/compose/cli-command/)
- [Zenn の記事](https://zenn.dev/skanehira/articles/2021-06-03-new-docker-compose)



↑の公式ドキュメントを参照するとインストール方法とかが書いてある

Docker Desktop を使っている人用のインストールと、Linux向けのインストール方法が書かれていてありがたい

WSLを使っている人はLinuxのやつを使えば良さそう



一応下記がインストールコマンド

> ### Install on Linux
>
> You can install Compose V2 by downloading the appropriate binary for your system from the [project release page](https://github.com/docker/compose/releases) and copying it into `$HOME/.docker/cli-plugins` as `docker-compose`.
>
> 1. Run the following command to download the current stable release of Docker Compose:
>
>    ```
>     $ mkdir -p ~/.docker/cli-plugins/
>     $ curl -SL https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
>    ```
>
>    This command installs Compose V2 for the active user under `$HOME` directory. To install Docker Compose for all users on your system, replace `~/.docker/cli-plugins` with `/usr/local/lib/docker/cli-plugins`.
>
> 2. Apply executable permissions to the binary:
>
>    ```
>     $ chmod +x ~/.docker/cli-plugins/docker-compose
>    ```
>
> 3. Test your installation
>
>    ```
>     $ docker compose version
>    ```



自分用に、コピペしてはれるよう

```bash
# docker compose コマンドを ~/.docker/cli-plugins/ にダウンロード
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose

# すべてのユーザーに対して実行可能権限を付与
chmod a+x ~/.docker/cli-plugins/docker-compose

# バージョンの確認
docker compose version
```

