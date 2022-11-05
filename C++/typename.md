# typename



C++ の `typename` ってなに？っていうことでね

書いていきたいと思います



## テンプレートパラメータでの typename

```cpp
template <typename T>
struct a{
  // なんかの処理
};
```

これはテンプレートのパラメータ T が **型であることを宣言** するために使われている



ここで、`typename`の部分を`class`にしてもなにも違いはない

人によってどのように使い分けるかは自由



## 階層を持つテンプレートのための typename

```cpp
template <typename T>
struct a{
  vector<T> data;
  
  using DataType = T;
  using Iterator = typename vector<T>::iterator;
};
```



1つ目の `using` に関してはなにも問題はない

2つ目は `typename` をつけなければコンパイルエラー！！



### なぜ？

T はテンプレートパラメータなので、不確定

`vector<???>::iterator`になってしまう



`クラス名::xxxx` という形式は型だけでなく、定数にも使われる可能性がある。 そのため、型かどうかハッキリしないものに対して別名定義である using(typedef) を使うと、コンパイルエラーとなってしまう。



コンパイルを通すには **typename** を記述して <u>次に来るのが型だとコンパイラに伝える</u> 必要がある



階層を持つテンプレートには、**型だということを宣言する typename** が必要だと覚えような



# 参考

ほぼこれを引用した

- [C++ typename の 2 つの使い方](http://yohshiy.blog.fc2.com/blog-entry-336.html)

