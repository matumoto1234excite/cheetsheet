# docker-composeを使った効率化



## 不便なコンテナ開発

- コンテナを一つ一つ起動しなければならない
- ネットワーク設定を考えなければならない
- コンテナ起動コマンドのスニペットがぶくぶく太っていく

=>「操作より設定」の概念を導入して解決



## docker-compose

- 設定ファイルを通して、コンテナを立ち上げるのに必要なコマンドを簡略化する
- ネットワークの設定も自動で設定してくれる
- 設定ファイルをリポジトリ管理することで、構成管理を透明化できる
- .env対応
- kubernetesのpodみたいなもん
- ECSのタスクみたいなもん



## 設定ファイル（docker-compose.yml）

あくまで一例

```yaml
version: '3'
services:
  workspace:
    build: workspace/
    volumes:
      - ${BASE_DIR}
  php-fpm:
    build: ./php-fpm
    volumes:
      - ${BASE_DIR}
    expose:
      - "9000"
      
  nginx:
    build:
      context: ./nginx
      args:
        - PHP_UPSTREAM=php-fpm
    ports:
      - "8080:80"
      - "444:443"
    volumes:
      - ./logs/nginx/:var/log/nginx
      - ./nginx/sites/:/etc/nginx/sites-available
      - ./nginx/ssl/:etc/nginx/ssl
      - ${BASE_DIR}
  
  db:
    image: mysql:5.7
    environment:
      - MYSQL_DATABSE=homestead
      - MYSQL_USER=homestead
      - MYSQL_PASSWORD=secret
      - MYSQL_ROOT_PASSWORD=root
    volumes:
      - mysql:/var/lib/mysql
 
 volumes:
   mysql:
     drive: "local"
```

上の設定の説明

- version

  docker-compose.ymlの記法のバージョン

  docker-compose自体のバージョンによって使えたり使えなかったりする

  例

  ```yaml
  version '3'
  ```

- services

  それぞれが動作するコンテナを意味している

  システムを分離できたら、それらを全部書き込んでいく

  ```yaml
  services:
    workspace:
      ...
      ...
    
    php-fpm:
      ...
    
    db:
      ...
  ```

  

- image

  コンテナのイメージをそのまま使う場合に使用

  `image: mysql:5.7`

- build

  自前のイメージを使う場合に、Dockerfileの存在するディレクトリを指定

  ```yaml
  nginx:
    build: ./nginx
  ```

- environment

  起動時に必要な環境変数（配列形式で指定）

  ```yaml
  environment:
    - MYSQL_DATABASE=homestead
    - MYSQL_USER=homestead
    - MYSQL_PASSWORD=secret
    - MYSQL_ROOT_PASSWORD=root
  ```

- ports

  ポートフォワードするときのポートを設定

  ```yaml
  ports:
    - "8080:80"
    - "444:443"
  ```

- volumes

  共有ボリュームの設定（配列形式で指定）

  ```yaml
  volumes:
    - ../mysql:/var/lib/mysql
  ```

- depends_on

  自分が立ち上がる時に一緒に立ち上がっているべきコンテナ（サービスを指定）

  ```yaml
  depends_on:
    - php-fpm
    - db
    - cache
  ```

  

## docker-composeコマンド

- `up`

  サービスを立ち上げる

  ターゲット指定した場合、depends_onに認定されたサービスが有る場合はそれらも一緒に立ち上げる

  例

  設定されているコンテナ全部立ち上げる

  ```bash
  $ docker-compose up
  ```

  例

  nginxコンテナをバックグラウンドで動作させる

  ```bash
  $ docker-compose up -d nginx
  ```

- `down`

  立ち上がっているサービスを停止させ、コンテナを除去する

  やることやって、作業を終了するときなどに使う

  ```bash
  $ docker-compose down
  ```



# まとめ

- コンテナ開発を始めよう
- システムを分離して役割に応じてコンテナを立てよう
- ネットワーク機能を使ってコンテナ同士をつなげよう
- docker-composeを使ってコンテナ開発を楽にしよう