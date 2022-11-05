# ostringstream

出力したものが文字列になればいいなぁって思ったことありませんか？ありますよね？？？

数字の0埋めとかができる

`printf`を使わなくてもいいね！

```cpp
ostringstream scout;
scout << setfill('0') << setw(6) << 10;
cout << scout.str() << endl;

// 結果
000010
```

