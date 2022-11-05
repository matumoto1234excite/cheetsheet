# dockerのネットワーク

コンテナ間の通信はどうやって実現できるか



## dockerのネットワークを使った解決

dockerはdockerサーバ自体が提供しているネットワークが存在している

このネットワーク上でaliasをつければよい



例

php:alpineから、mysqlコンテナをdbという名前で他のコンテナからアクセスできるようにする

```bash
$ docker run -d -e MYSQL_ROOT_PASSWORD=my-secret-pw --name db mysql:5.7
$ docker run -it --rm --link db:db php:alpine sh
```



### dockerのネットワーク追加

dockerはデフォルトの内部ネットワークだけでなく、ユーザー定義のネットワークもできちゃう



「sample」という名前のネットワークを構築するコマンド

```bash
$ docker network create -d bridge --subnet 172.26.0.0/24 sample
```

「sample」上にmysqlを設置し、dbという名前でネットワーク内からならつなげられるように設定

```bash
$ docker run -d --network sample --network-alias db -e MYSQL_ROOT_PASSWORD=my-seqret-pw mysql:5.7
```

php:alpineコンテナを同じネットワークに乗っける

```bash
$docker run -it --rm --network sample php:alpine sh
```