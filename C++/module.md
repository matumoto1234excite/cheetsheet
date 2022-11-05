# module

 C++20 から module という機能が使えるようになった



これは長らくC++に長らく欠落していた効率的なファイル分割を行う機能である



詳しくはここ

- https://zenn.dev/onihusube/articles/299ed7a3bc6062068fdd
- https://cpprefjp.github.io/lang/cpp20/modules.html



上の記事たちを要約すると、

- module には export や import があり、JavaScriptのように使える
- グローバルモジュールフラグメントだったりプライベートモジュールフラグメントだったりが存在する
- module 宣言の前に`#if`や`#include`のようなトークンは書いてはならない
- moduleの書かれたファイルの拡張子は`.ixx`(MicrotSoftVisualC++の規格で定められているらしい)



のようなことが書かれている



お気持ちとして、○○フラグメント系は構造体のアクセス修飾子の`public:,private:`みたいな挙動をしているので、それが記述された下の領域のことを指しているのを認識するとうれしい

ただ、プライベートモジュールフラグメントは**１つしか書けない**らしいので気を付けるべし



あと、たぶんアンダースコア`_`は命名に使ってはいけないとか書いてあった気がする



例

```cpp
module; // グローバルモジュールフラグメント

// これ以下はグローバルモジュールフラグメントという領域
// ここに #include だったり をする
// ここで #include されたものは import されたときには利用できない（うれしい！）

export module mylibrary;
// ここからはインターフェース
// import されたときに見える部分を書く

namespace mylibrary {
  
  // クラスのエクスポート、暗黙的に全メンバがエクスポートされる
  export class Hoge {
    int value_;
  public:
    Hoge();
    Hoge(int v);
    
    int get() const;
  };
  
  void print_Hoge(const Hoge &h);
}

module : private; // プライベートモジュールフラグメント
// private:module; ｔこれは記事が間違ってるので注意

// これより下は見えない部分
// ここに上の export されている部分の実装を書く

namespace mylibrary {
  Hoge::Hoge() = default;
  Hoge::Hoge(int v) : value_(v) {}
  
  inline int Hoge::get() const {
    return this->value_;
  }
  
  void print_Hoge(const Hoge &h) {
    std::cout << h.get() << std::endl;
  }
}
```

これめちゃくちゃよくないですか！？

よくない！？

すげええええええええええええええええええええええええ



上の例は モジュールのインターフェース単位を実装単位を一つのファイルで行ったが、記事では`.ixx`でインターフェース単位を、`.cpp`で実装単位を分けて行っている例も記載されている



さらに利用例

```cpp
import mylibrary;

int main() {
  mylibrary::Hoge h1;
  mylibrary::Hoge h2(20);
  
  mylibrary::print_Hoge(h1); // 0
  mylibrary::print_Hoge(h2); // 20
}
```



ちなみに、実装単位の方で新しく`print_Fuga`みたいな関数を作ったとしてもそれは完全に**参照できない**

あらかじめインターフェース単位で `export`宣言しておく必要がある





上のZENNの記事の4つ目の最後にある表

めちゃんこわかりやすい

# パーティション、まとめ

ここまでで4+1種類のモジュールの形式が登場しました。ユーザーが書く部分のモジュールとしてはこれで全てです。しかし、似たような言葉が飛び交ってややこしく理解しづらいと思うので簡単にまとめておきます。

| 種別                               | 宣言例                       | 数                  | `export`宣言 |
| ---------------------------------- | ---------------------------- | ------------------- | ------------ |
| プライマリインターフェース単位     | `export module M;`           | `1`（必須）         | 書ける       |
| 実装単位                           | `module M;`                  | `0 <=`              | 書けない     |
| インターフェスパーティション       | `export module M:interface;` | `0 <=`              | 書ける       |
| 実装パーティション                 | `module M:impl;`             | `0 <=`              | 書けない     |
| プライベートモジュールフラグメント | `module : private;`          | `1`（存在する場合） | 書けない     |