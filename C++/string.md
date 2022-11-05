# string

はい

https://cpprefjp.github.io/reference/string/basic_string.html



実はstringってbasic_string型をエイリアスしたものだったりする

あと、string_viewというのがconstexpr stringの代わりで用意されている

他に特にいうことはないので、注意点とかだけを書く



## コンストラクタ

https://cpprefjp.github.io/reference/string/basic_string/op_constructor.html

```cpp
string s(100,' '); // ' 'を100文字分
string s="aiueo";
```







## 文字列の連結

```cpp
string s;
s += "hogehoge";
s = s + "hogehoge";
```

下のやつだと計算量が無駄にかかるので気を付けましょう

$O(N^2)$​になったりする



## 



