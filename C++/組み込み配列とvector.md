# 組み込み配列とvector



vectorをポインタ配列でなく、組み込み配列にしたい！



### vectorから配列

```cpp
vector<int> vs=vector<int>{1,2,3,4,5};

int arr[vs.size()];
copy(vs.begin(),vs.end(),arr);
```

関数にできないのがつらいところ





### 配列からvector

```cpp
int arr[]={1,2,3,4,5};

vector<int> vs(begin(arr),end(arr));
```

こっちは簡単にできる

ほかの手段もたくさん

`int siz = sizeof(arr)/sizeof(int)`みたいにサイズも取れる

c++17以降なら`size(arr)`でいける



## 参考

https://programdoria.com/programming/cpp/arrayvector/