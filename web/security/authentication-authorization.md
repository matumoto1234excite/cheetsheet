# 認証(authentication)と認可(authorization)

## 認証と認可って？

- **認証は「誰か」を確認する**
	- これ以上でもこれ以下でもなく、純粋な認証はただ「誰か」を確認することだけ
	- どのリソースを使うのかとかは関係ない


- **認可はアクセスの許可や権限**
	- 「誰か」については一切見ていない
	- 家の鍵を持っていれば誰でも入れるのと同じ
	- Bearerトークンを持っている相手に対して特定のリソースへのアクセスを許可する(OAuth2.0)


## OAuth2.0とは？

権限の「認可」を行うためのプロトコル

例えば、Googleに関係するサービスが、あるユーザのGoogleDrvieにアクセスが必要になったとき

1. サービスがユーザにアクセス権限を求める
2. ユーザがGoogleに認証ログインする
3. Googleがユーザにアクセストークンを渡して良いか聞く
4. ユーザが許可
5. Googleがサービスにアクセストークンを渡す
6. この時点で認可完了

## OAuth認証とは？

おかしい言葉、造語？

### なにがいけないのか

- CSRF攻撃
- 認可トークンだけ他人のものにすげ替えられたら検知できない

### どうすれば安全に認証できるのか

OpenIDConnect(OIDC)を使用する

## OpenIDConnectとは？

「認証用」のプロトコル

基本的なフローはOAuth2.0と一緒だが、トークンの部分が単なるBearerトークンではなくID Tokenというものになっている

### ID Tokenとは？

セッション情報などを持っているトークン
これによって、認可トークンをすげ替えられた攻撃も検知できる

# 見るべし
- https://www.youtube.com/watch?v=uWNtRYWNmh8
- https://qiita.com/uasi/items/cfb60588daa18c2ec6f5
- https://zenn.dev/mryhryki/articles/2021-03-28-authentication-and-authorization