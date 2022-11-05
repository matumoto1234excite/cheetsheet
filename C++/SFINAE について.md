# SFINAE について

SFINAEはスフィネェと読みます

Substitution Failure Is Not An Errorの略

代入失敗はエラーではない



まだ、経験が浅いだけかもしれないけど可変長引数とセットで扱われると思う。



可変長引数のものは優先度が低いので`hoge(10);`とかって呼ぶと上の`hoge`が呼び出される

```cpp
int hoge(int a){
  
}
int hoge(...){
  
}
```



これを利用してメタプログラミングと一緒に頑張ると色々できる

例：イテレータを持つかどうかの判断

```cpp
template <typename T>
class has_iterator {
  template <typename Container>
  static true_type check(typename Container::iterator *);
  template <typename Container>
  static false_type check(...);

public:
  static const bool value = decltype(check<T>(0))::value;
};

has_iterator<set<int>>::value; // true
has_iterator<int>::value;      // false
```



これは上の関数が呼び出されているが、メンバに`iterator`がなくてエラーになると下の可変長引数のほうに移る







イメージ画像:arrow_down:

![image-20211013065300630](C:\Users\matum\AppData\Roaming\Typora\typora-user-images\image-20211013065300630.png)