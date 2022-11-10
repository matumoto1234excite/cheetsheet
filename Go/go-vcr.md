go-vcrのvcrはVideo Cassette Recorderの略

とりあえず、下のスライドを見ておけばOK
- https://speakerdeck.com/yyh_gl/vcr-in-go-motukuzi-dong-sheng-cheng-dele-sitiyauhua

go-vcrが使える条件としては、http.Clientの注入ができればOK


```go
type MyClient struct {
	Client *http.Client
}

func NewMyClient(client *http.Client) *MyClient {
	return &MyClient{
		Client: client
	}
}
```

より正確には、RoundTripper というインターフェースを実装している
通常の`http.Client`で `client.Get("apis/user")` のようなことをするとnet/http.DefaultTransportがそれを行うが、そこをrecorderで置き換える

```go
func main() {
	r, err := recorder.New("cassettes/directory/matumoto")
	if err != nil {
		log.Fatal(err)
	}
	defer r.Stop()

	client := &http.Client {
		Transport: r,
		Timeout:   3 * time.Second,
	}
	url := "[https://httpbin.org/headers](https://httpbin.org/headers)"
	res, err := client.Get(url)
	if err != nil {
		log.Fatal(err)
	}
	
	_, err := io.Copy(os.Stdout, res.Body)
	if err != nil {
		log.Fatal(err)
	}
	defer res.Body.Close()
}
```

これを実行すると、cassettes/directory/matumoto.yaml が生成される

1回目は普通にリクエストし、2回目はそのyamlがレスポンスとして用いられる
1つのrecorderに対して、1つのmock request(cassette)が対応している

### 参考
- https://pod.hatenablog.com/entry/2020/08/15/011525