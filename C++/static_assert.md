# static_assert



`assert`

![image-20210915232412315](C:\Users\matum\AppData\Roaming\Typora\typora-user-images\image-20210915232412315.png)

```cpp
#include <cassert>
using namespace std;

int main(){
  assert(false);
}
```

のようなものをAtCoderに投げると、`RE`になる

実行時にエラーが起こっている





`static_assert`を使うと、`CE`になる

```cpp
int main(){
  static_assert(false, "hoge");
  static_assert(false); // C++17以降ではエラーメッセージの省略可能
}
```

includeは、ない



こうすると、テンプレート引数でassertをする際などはこっちのstatic_assertを使った方がよい



https://cpprefjp.github.io/lang/cpp11/static_assert.html