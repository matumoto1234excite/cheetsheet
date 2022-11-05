# OAuth2.0

Authorization code grant

AuthZ

これは認可のプロトコル



分かんなくなったらこれを見ろ

https://qiita.com/TakahikoKawasaki/items/e37caf50776e00e733be



5つの資源がある

- user_agent

- client

  クライアントアプリケーションのことを指す

  もしくはサードパーティアプリケーション

- Authorization server

- Resource server

- Resource owner



Access Tokenをもらう



user_agentにはTokenを持たせない方がよいのはそれはそう

サーバーレスでやるにはめんどくさい

OAuthはエクスプレスが前提になっている