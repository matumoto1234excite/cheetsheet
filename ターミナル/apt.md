# apt



```bash
# バージョンとかを見る
$ apt info パッケージ名

# インストール
$ apt install パッケージ名

# アップグレード
$ apt install --upgrade パッケージ名

# PPAを更新（追加？）
$ sudo add-apt-repository ppa:longsleep/golang-backports

# いろいろ見る
$ apt-cache showpkg パッケージ名
```



## PPA ってなーに？

> **PPA**は**Ubuntu**ユーザーのチームや個人がそれぞれ管理している非公式のApp Storeのようなもので、**Ubuntu**の公式レポジトリからはダンロードできないソフトウェアや最新のバージョンのソフトウェアを手に入れることができます。

そもそも、Personal Package Archive の略



`/etc/apt/source.list`にそもそもいろいろなパッケージが入っていて、それが公式リポジトリ

非公式リポジトリが別にあって、そこでは最新バージョンが用意されていることが多い



PPAに追加すると`update`の際にバージョンが更新されていく