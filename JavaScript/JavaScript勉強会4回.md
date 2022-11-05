# JavaScript勉強会4回

今回はサーバー側



## npmについて

npmはライブラリを取ってくる

npmを使うとそこに`.node_modules`に入る



## nodeについて



jsファイルを指定するとそれを実行できる

```bash
$ node hoge.js
```



## expressについて

Node.js向けのHTTPサーバーを構築するためのフレームワーク

これを使うと簡単にサーバーが書ける

`npm install express`ですぐに使える

`npm install cros`はURLをまたいだHTTPリクエストをするためのもの

ちなみにCross-Origin Resourse Sharingの略



これで`http://localhost:3000`にGETができる

```js
// expressのセットアップ
const express = require("express")
const cors = require("cors")
const app = express()
app.use(express.json())
app.use(cors())


// エンドポイントの定義
app.get("/", (req, res) => {
  res.send("Hello world!")
})


// サーバーの起動
app.listen(3000, () => {
  console.log("serer start")
})
```



- app.get
  - サーバーにエンドポイントを登録する
  - エンドポイントは通信を受け付ける場所
  - 第1引数はパス、第2引数は処理をする関数
  - app.get以外にもapp.postなどがある
- app.listen
  - サーバを起動する
  - 第1引数にはポート、第2引数には処理をする関数



## URLについて



`https://todo.yt8492.com/s1260119/todos`について見てみる



- https

  httpよりセキュアな通信を行う

- todo.yt8492.com

  - ドメイン名
  - todo.yt8492.com:443の省略形。（httpの場合は80）httpsだと指定しないと自動的に443になる

- /s1280119/todos

  - パス
  - エンドポイントを定義する関数の第1引数で指定するのがこれ





## HTTPリクエストについて





## HTTPレスポンスについて

expressには3つ方法がある

- res.send

- res.json

- res.end

  これはレスポンスのボディが空で返す





## リクエストのパスをパラメータにする

```js
app.get("/:userId/todos", (req, res) => {
    const userId = req.params["userId"]
    // req.params.userIdでもOK
})
```

paramsの部分はexpress独自で色々やってくれてる

`req.params`にオブジェクトとしてパスパラメータが入っている





##  ローカルファイルの入出力

`fs`を使いましょう

Node.jsだと標準で入っている

`const fs = require("fs")`

write,appendがある

deleteはなさそうで、deleteの代わりにwriteを使う気がする



- `fs.writeFileSync`

  - ```js
    fs.writeFileSync("./data.txt", "書き込む内容！", (err) => {
        if (err) throw err
    })
    ```

  - 同期あり

- `fs.appendFileSync`

  - writeFileSyncのappendバージョン



成果物

```js
// expressのセットアップ
const express = require("express")
const cors = require("cors")
const fs = require("fs")
const app = express()
app.use(express.json())
app.use(cors())


const filePath = "./data.json"

let todoList
let index = 0

// ファイルの読み込み
try {
  const text = fs.readFileSync(filePath, "utf-8")
  todoList = JSON.parse(text)

  for (const todo of todoList){
    num = parseInt(todo.id, 10)
    index = Math.max(index, num)
  }
  index++
} catch(err) {
  console.log(err)
}



// エンドポイントの定義
// GET
app.get("/todos", (req, res) => {
  res.send(todoList)
})


// POST
app.post("/todos", (req, res) => {
  const body = req.body
  const todo = {
    id: String(index),
    text: body.text
  }

  todoList.push(todo)
  index++

  fs.writeFileSync(filePath, JSON.stringify(todoList), (err) => {
    if (err) throw err
  })

  res.end()
})


// DELETE
app.delete("/todos/:id", (req, res) => {
  const id = req.params.id
  let delIdx = 0
  for (let i = 0; i < todoList.length; i++) {
    if (todoList[i].id === id) {
      delIdx = i
      break
    }
  }
  todoList.splice(delIdx, 1)


  fs.writeFileSync(filePath, JSON.stringify(todoList), (err) => {
    if (err) throw err
  })

  res.end()
})


// サーバーの起動
app.listen(3000, () => {
  console.log("serer start")
})
```

