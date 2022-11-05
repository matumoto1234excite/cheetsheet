# inline 変数



inline 関数と同じ用法であるらしい



## inline 関数とは？

ソースコードのインライン展開をするという認識はじつは誤解だったりする



inline 修飾子をつけることが意味するものは、

- インライン展開するヒントをコンパイラに与える
- 変数の実態は一つのみの、同じ変数を宣言できる



```cpp
// C++17以降 -----

// ヘッダ
struct X {
  // ソースで変数fooを定義する必要がない
  static inline int foo;
};


// C++14以前 -----

// ヘッダ
struct X {
  // ヘッダでは変数の宣言のみを行い
  static int foo;
};

// ソース
// 変数fooを定義する
int X::foo;
```



メンバ変数の定数に関わってくるお話



```cpp
struct hoge {
  static constexpr int val = 123;
};
```

みたいなのってC++17以降なら暗黙的に`inline`がついている



クラスの外にある変数と同じように振る舞う



## 参考

- https://cpprefjp.github.io/lang/cpp17/inline_variables.html
- https://qiita.com/Nabetani/items/d8a3ebccaef03cd18d81