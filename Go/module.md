# module

## 初期設定

`go mod init`をする

```bash
$ go mod init github.com/matumoto1234/go-todo
```

みたいな感じで



そうすると、go.mod というファイルが勝手に出来上がり、そこに現プロジェクトで使っているモジュールなどが追記されていく





## モジュールを追加したいとき

なにかのモジュールを使っているプロジェクトで使いたいときは `go get`をすればいい

```bash
$ go get github.com/gin-gonic/gin@latest
# -u をつけると依存関係もまとめて go.mod に追加される
```



`go get`を行うと、go.mod に追加される

もし、`-u`オプションをして、使わない依存関係がgo.modにあるのがうっとおしくなったら `go mod tidy`で使っていないものをgo.modから勝手に削除してもらえばいい(逆に使っているものは追記される)



また、よく勘違いしやすいバイナリのインストールについては Go1.18 から廃止され `go install`を使うようになった



