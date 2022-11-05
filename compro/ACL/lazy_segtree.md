# lazy_segtree



https://atcoder.github.io/ac-library/document_ja/lazysegtree.html

全てが公式ドキュメントにのってる気がするな



## できること

- 区間更新
- 区間取得



## のっけられるもの

モノイドとそれの写像

写像の条件はこれ

- $$
  \begin{align}
  Fは恒等写像idを含む。つまり、任意のx \in Sに対しid(x)=xを満たす。
  \end{align}
  $$
  
- $$
  Fは写像の合成について閉じている。つまり、任意のf,g\in Fに対し f \circ g \in Fである。
  $$

- $$
  任意のf \in F,x,y \in Sに対しf(x \cdot y) = f(x) \cdot f(y)を満たす。
  $$







### 写像is何

モノイドからモノイドへ値を更新するなにかの操作

要するに更新クエリとか、区間取得クエリのこと





## どうやって使うのか

じゃあ、次のようなMINの区間取得、区間更新を例にする

区間取得:=[l,r]の最小値を求める

区間更新:=[l,r]にxを加算する



今回のモノイド

- 集合:=int

- 二項演算:=min(a,b)

- 単位元:=INF



区間更新

- mapping:=更新分を足したものを返す

- composition:=f.x+g.x

- id:=f.xに0を足す



mappingは何をするのか

写像FをモノイドSに適応してモノイドSを返す



compositionは何をするのか

写像F同士の合成

fとgを順に適応したときの写像を返す



idは何をするのか

写像Fに対する恒等写像

要するに写像Fの単位元となる操作



```cpp
struct S {
    int sum;
};

struct F {
    int x; // 更新分
};

constexpr S INF = S{2e9}; // これ動くのか？

S op(S a, S b) { return min(a.sum, b.sum); }
S e() { return INF; }
S mapping(F f, S a) { return S{a.sum + f.x}; }
F composition(F f, F g) { return F{f.x + g.x}; }
F id() { return F{0}; }
```



使ったら割と慣れそうではある

ブラックボックスとして使うだけでも割と難しいのだけど、実際に作ってみたいというのはほんの少しだけあるかな



## テクニック

値を置き換える系の恒等写像idはどうしようか

idを存在しない値にしてmappingやcompositionの際に場合分けをするとよい

```cpp
S mapping(F f, S a) {
    if ( f == id ) {
        return a;
    }
    return f;
}
```

- https://betrue12.hateblo.jp/entry/2020/09/23/005940

  色んな場合の例を載せてくれている

  えらい、ノーベルうくにきあ賞

- https://opt-cp.com/lazysegtree-practice/

  3問載せてくれている

  ありがとう