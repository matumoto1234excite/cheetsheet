# JavaScript勉強会3回



## アロー関数

- 無名関数よりもアロー関数の方がよく使われる
- Internet Explorerとかでは動かないかもしれないが、今時気にする必要はない
- `(引数) => {}`

```js
const plus1 = (x) => {
    return x + 1;
}

console.log(plus1(2)) // 3

// 関数の中身が1行の場合、中括弧とreturnはいらない
const plus2 = x => x + 2
console.log(plus2(2)) // 4
```



## HTTP通信

HTTPはHypertext Transfer Protocolの略

- HTMLやJSONを扱うことが多い
- リクエストとレスポンスという概念がある
  - リクエストはクライアントからサーバー
  - レスポンスはサーバーからクライアント



### HTTPリクエスト

大きく分けて3つの要素からなる

- 開始行

  - メソッド
  - URL
  - HTTPバージョン

- ヘッダー

  - ボディの形式や認証情報

  - 必須ではない

- ボディ

  - リクエストの本文

  - 必須ではない



### HTTPレスポンス

大きく分けて3つの要素からなる

- 開始行

  - ステータスコード

    404とか502とか

    「HTTPステータスコード」とかで検索するといろいろ出てくる

  - HTTPバージョン

- ヘッダー

  - ボディの形式やキャッシュの有効期限など
  - 必須ではない

- ボディ

  - レスポンスの本文
  - 必須ではない



### HTTPメソッド

主に5つ

- GET

  - リソースの読み込み

- POST

  - リソースの送信

- PUT

  - リソースの置き換え

    twitterのプロフィールの更新など

- PATCH

  - リソースの部分的な置き換え

    PUTとPATCHの使い分けについては「PUT PATCH 使い分け」とかで調べると良い

- DELETE

  - リソースの削除



### JavaScriptでHTTP通信を行う

- `fetch`という関数を使う（`fetch`以外にも`axios`などの手段がある）
- `fetch("url").then(関数)`みたいな形
- `.then().then()`みたいにすることで前の`then`の返り値を新しい`then`の中で使える
- `then`の中身は

```js
// fetchは何も指定しない場合、GETになる
fetch("https://todo.yt8492.com/")
  .then(response => response.json()) // 帰ってきたデータをjsonにする
  .then(data => console.log(data)) // jsonにしたデータをコンソールに出力する

// HTTPリクエストの種類をPOSTに指定する
fetch("https://todo.yt8492.com/", {
  method: "POST",
  body: JSON.stringify({message: "Hello"}), // リクエストの本文
  headers: {
      'Content-Type': 'application/json' // ボディの形式を指定する
    }
})
  .then(response => response.json())
  .then(data => console.log(data))
```



#### Promiseって？

`fetch`の結果は`Promise`になる

`Promise`は非同期処理に使われる

実行した時点では帰ってきた結果ではないが、値が帰ってき次第、その値になる

`Promise`には3つの状態がある

- *pending*: 初期状態。成功も失敗もしていません。
- *fulfilled*: 処理が成功して完了したことを意味します。
- *rejected*: 処理が失敗したことを意味します。



#### `.then`の意味

`.then`は処理の結果が帰ってきたら行われる処理

`Promise`が`fulfilled`になったら`.then`に遷移する

同期処理、非同期処理に大きくかかわってくる



#### curlコマンド

`curl`コマンドはHTTPリクエストを送れるコマンド

`curl -X GET https://google.com`みたいに`-X`オプションでHTTPメソッドを使えるし、つけないと自動的にGETになる



