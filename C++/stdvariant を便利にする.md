# std::variant を便利にする



- https://matumoto-h.hatenablog.com/entry/2022/01/19/231039
- https://matumoto-h.hatenablog.com/entry/2022/01/18/202704



上の記事で、gets と holds を作った



これによって以下のようなコードを書くことができる





```cpp
if(holds<int>(hoge)) {
  int value = gets<int>(hoge).value();
}
```

ネストを深くせずに、値を保持しているかの確認と、その値の取得が行えるため、代数的データ構造が便利になる



やったね



