# Dockerfile



## え？Dockerfileをご存じない！？

Dockerfileはdockerのイメージを自動で作成してくれるファイル

Docker build .を打つとDockerfileを自動で読み込み、書かれている通りのDockerイメージを作成してくれる

一例

```dockerfile
FROM ubuntu:18.10

LABEL version="1.0"
LAVEL description="Dockerfileのテスト、Apacheサーバー"

RUN apt-get update
RUN apt-get install -y apache2

CMD ["apachectl", "-D", "FOREGROUND"]
```

誰がどの環境で`docker build`しても全く同じイメージが作られる！すごい！



##  Dockerfileの命令

| 命令        | 説明                         |
| :---------- | :--------------------------- |
| FROM        | ベースイメージの指定         |
| RUN         | コマンド実行                 |
| CMD         | コンテナの実行コマンド       |
| LABEL       | ラベルを設定                 |
| EXPOSE      | ポートのエクスポート         |
| ENV         | 環境変数                     |
| ADD         | ファイル/ディレクトリの追加  |
| COPY        | ファイルのコピー             |
| ENTRYPOINT  | コンテナの実行コマンド       |
| VOLUME      | ボリュームのマウント         |
| USER        | ユーザーの指定               |
| WOEKDIR     | 作業ディレクトリ             |
| ARG         | Dockerfile内の変数           |
| ONBUILD     | ビルド実行後に実行される命令 |
| STOPSSIGNAL | システムコールシグナルの設定 |
| HEALTHCHECK | コンテナのヘルスチェック     |
| SHELL       | デフォルトシェルの設定       |

Dockerfileでは、DockerコンテナをどのDockerイメージから生成するかを必ず書く必要があります。

```dockerfile
FROM [イメージ名]
FROM [イメージ名]:[タグ名]
FROM [イメージ名]@[ダイジェスト]
```

FROM命令は必須です。ダイジェストは、DockerHubにアップロードすると自動で付与される識別子で、ユニーク。



# Dockerイメージのレイヤー構造理解して、nginx起動させる

```dockerfile
# STEP1 Ubuntu
FROM ubuntu:latest
# STEP2 Nginxのインストール
RUN apt-get update && apt-get install -y -q nginx
# STEP3 ファイルのコピー
COPY index.html /usr/share/nginx/html/
# STEP4 Nginxの起動
CMD ["nginx","-g","deamon off;"] 
```

この例のDockerfileと同じディレクトリに任意の「index.html」という名前のファイルを用意する。
このファイルをbuildすると、命令1行ごとにイメージを生成される。
生成された4つのイメージから共有イメージが作成される。





以下、この記事

[Dockerfileを書いてみる](https://qiita.com/shin-ch13/items/1de829288db2670276e8)



##  1. Dockerfileの作成

```bash
$ vim Dockerfile
```

```dockerfile
# どのイメージを基にするか
FROM centos
# 作成したユーザの情報
LABEL maintainer="Admin <admin@admin.com>"
# RUN: docker buildするときに実行される
RUN echo "now building..."
# CMD: docker runするときに実行される
CMD echo "now running..."
```

Dockerfileをビルドして"admin/echo"イメージの作成

-t : ビルド成功後メッセージ表示

```bash
$ sudo docker build -t admin/echo .
```

"admin/echo"イメージからコンテナの作成

```bash
$ sudo docker run admin/echo
```



1. Dockerfileを書く
2. buildする
3. runする

がおおまかな流れっぽい

