# 1行のif文を使うときはどんなときか？

Goでは以下のように、if文を以下のように省略形で書くことが出来る

```go
if err := hoge(); err != nil {
  return err
}
```

では、この省略形を使用するときはどんなときか？

## 結論

省略形が見やすいんだったら省略形を使って、見づらいんだったら使わない

## 理由

この記事を見ればOK

- [When Should I Use One Liner if...else Statements in Go?](https://www.calhoun.io/one-liner-if-statements-with-errors/)

上の記事の内容をざっとまとめるとこんな感じになる

- [Go wikiにある1行の長さについての質問](https://github.com/golang/go/wiki/CodeReviewComments#line-length)の紹介
- 省略形を使う影響
- 修正する際にどう書くのが嬉しいか

なんかが書いてある

特に、１つ目のGo wikiのやつは見ておくべきかも知れない

### 小ネタ

- [else ifにも代入文が書ける](https://tenntenn.dev/ja/posts/qiita-791bb47f4cee178b52c3/)
