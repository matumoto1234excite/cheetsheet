# is_template

is_template なんてものはないので作りましょう



超絶ありがたい記事様

> [型があるtemplate class型であるかチェックするメタ関数](https://qiita.com/tyanmahou/items/a0d67e221b8971e895c6)



※`using namespace std;`を使用しています

```cpp
template <template <typename...> typename TemplateType, typename Arg>
struct is_template : false_type {};

template <template <typename...> typename TemplateType, typename... Args>
struct is_template<TemplateType, TemplateType<Args...>> : true_type {};

template <typename T>
using is_vector = is_template<vector, T>;

template <typename T>
using is_map = is_template<map, T>;
```



うーーん、すごい



気合でコンテナ型を列挙して`is_container`なんてものも作れそうではある