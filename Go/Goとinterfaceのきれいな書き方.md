# Goとinterfaceのきれいな書き方



```go
type A interface {
  GetLogin() TwitterService
  Write(TwitterService) error
}

type AImpl struct {
  userName string
  tu TwitterUser
}

// ここにinterfaceで書かれているメソッドを書いていく...

func NewA(userName string, tu TwitterUser) A {
  return &AImpl{
    userName: userName,
    tu      : tu,
  }
}
```



こんな感じでinterfaceを分離させたいときはこう書けばいい

こうすることで、上のレベルで参照する際にAを使えばよくなる



この場合は、TwitterUserがAの下の層にいる想定だけど、こんな感じで使う

最終的にmain.goで以下のようになる

```go
func main() {
  tu := NewTwitterUser(user)
  a := NewA("matumoto", tu)
  a.GetLogin()
  err := a.Write("くえくえ!")
  if err != nil {
    log.Fatal(err)
  }
}
```

みたいな



- インスタンス化は上流に流していく
- エラーも上流へ流していく
- 関数はほぼ無く、基本的にメソッドになる(interfaceに機能が大体のっかるので)



などなど

