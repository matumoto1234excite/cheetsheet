# Node.js のアップデート



`n` という node のパッケージ管理ツールを使う



node のインストール自体は apt でやる

npm にくっついてくるから

```bash
$ sudo apt install npm
```

みたいな感じで node は入る





## n のインストール

npm でやる

```bash
$ sudo npm install -g n
$ n --stable // node の stable(推奨版)のバージョンを表示
$ n --latest // node の latest(最新版)のバージョンを表示
$ n stable // stable をインストール(この時点ではまだバージョンは変わらない)
$ n
ここでインストールされているものの中からバージョンを選択する
```

