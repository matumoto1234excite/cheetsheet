# Goのチャンネル

3つの型がある

- `chan T`

- `<-chan T`

  - 引き出すことしかできなくなる

  - ```go
    func a() <-chan string {
      res := make(chan string, 1)
      res <- "hoge!!!"
      return res
    }
    
    b := a()
    s := <- b
    fmt.Println(s) // hoge!!!
    ```

- `chan<- T`

  - 突っ込むことしかできなくなる
  - ほんとにこれであってる？あってないかも





ちょっと遊んでみたテストコード

これは、1秒おきにチャンネルに文字列を流して、それが流れてきたら出力するプログラム

受け取る側は、チャンネルがcloseするまでループをまわし続ける

```go
pack受け取りてage main

import (
	"fmt"
	"time"
)

func main() {
	Do := func(s string) <-chan string {
		ch := make(chan string, 1000000)
		go func(s string) {
			for i:=0;i<3;i++ {
				ch <- s
				time.Sleep(1 * time.Second)
			}
			close(ch)
		}(s)
		
		return ch
	}
	
	res := Do("Hello")
	
	L:
	for {
		select {
		case s, ok := <- res:
			if !ok {
				break L
			}
			fmt.Println(s)
		default:
			fmt.Println("waiting...")
		}
		time.Sleep(500 * time.Millisecond)
	}
	fmt.Println("End!!")
}
```

:arrow_down: プレイグラウンド
https://go.dev/play/p/edqXisL_X9L





チャンネル式のfetcherを作ってみた

```go
package service

import (
	"fmt"
	"io"
	"math/rand"
	"net/http"
	"time"

	"github.com/pkg/errors"
)

type Result struct {
	Body  []byte
	Error error
}

func NewResult(body []byte, err error) *Result {
	return &Result{
		Body:  body,
		Error: err,
	}
}

func fetchGET(apiUrl string) *Result {
	res, err := http.Get(apiUrl)
	if err != nil {
		return NewResult(nil, errors.WithStack(err))
	}
	defer res.Body.Close()

	if res.StatusCode != 200 {
		errMsg := fmt.Sprintf("fetchURL: %v", res.Status)
		return NewResult(nil, errors.New(errMsg))
	}

	body, err := io.ReadAll(res.Body)
	if err != nil {
		return NewResult(nil, errors.WithStack(err))
	}

	return NewResult(body, nil)
}

type Fetcher struct {
	limit   int
	UrlBuff chan string
}

// Do GET request with random second waiting
func (f *Fetcher) Do() <-chan *Result {
	rand.Seed(time.Now().UnixNano())
	resBuff := make(chan *Result, f.limit)

	go func() {
		defer close(resBuff)
		for i := 0; i < f.limit; i++ {
			select {
			case apiUrl, ok := <-f.UrlBuff:
				if ok {
					res := fetchGET(apiUrl)
					resBuff <- res
				} else {
					return
				}
			default:
				/* when UrlBuff is empty, do nothing */
			}
			wait := rand.Intn(3) + 1
			time.Sleep(time.Duration(wait) * time.Second)
		}
	}()

	return resBuff
}

func NewFetcher(limit int) *Fetcher {
	return &Fetcher{
		limit:    limit,
		UrlBuff:  make(chan string, limit),
	}
}
```



使うときは、URLをbuffUrlに突っ込んでいって、突っ込み終わったらあとから`<-chan *Result`を受け取る

ごみ設計がよ