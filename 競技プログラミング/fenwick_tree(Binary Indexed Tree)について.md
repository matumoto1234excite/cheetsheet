# fenwick_tree(Binary Indexed Tree)について

fenwick_treeについてのまとめ



## fenwick_treeでなにができるか

一言でいうと、値の更新ができる累積和

- 値の更新

  add(index, value)みたいな感じでO(logN)

- 区間和取得

  sum(left, right)みたいな感じでO(logN)

  実際はsum(right)-sum(left)みたいな感じにしている



( ･`д･´)<それセグメント木でもできるよ！

fenwick_treeだと定数倍が軽い、実装も軽い、分かりやすい、メモリも少ない



## 値の管理方法

添え字を2進数で見てがちゃがちゃする

Binary Indexed Treeとも呼ばれるゆえん

大半の記事では`1-indexed`で管理している



1には[1,1]の合計値が入っている

2には[1,2]の合計値が入っている

3には[3,3]の合計値が入っている

4には[1,4]の合計値が入っている

5には[5,5]の合計値が入っている

6には[5,6]の合計値が入っている

7には[7,7]の合計値が入っている

8には[1,8]の合計値が入っている



k & (-k)で最も後ろのビットを取得できる

最も後ろのビットを足し引きすることで処理を行う



ただ、実用上はやはり`0-indexed`の方が使い勝手が良い

そこで、普通の累積和のように先頭に0を付け加えて、添え字を一つずらすことで`1-indexed`の実装方針かつ使う際は`0-indexed`で使える



## 値の更新

```cpp
// data:値を管理する配列, n:配列の長さ
// i:更新する値の添え字, x:更新する値
void add(int i, int x){
    for(int k=i; k<n; k+=(k&-k)){
        data[k]+=x
    }
}

// 0-indexed バージョン
// iを+1すれば良い。こうすると、sumなどで行う範囲は半開区間[)になる
void add(int i, int x){
    for(int k=++i;k<n;k+=(k&-k)){
        data[k]+=x;
    }
}
```



## 区間和取得

```cpp
// [1,x]の和を取得
int sum(int i, int x){
    int res=0;
    for(int k=i;k>0;k-=(k&-k)){
        res+=data[k];
    }
    return res;
}

// [l,r)の和を取得
int sum(int l, int r){
    // sum(x)が閉区間なので-1がいる
    return sum(r-1)-sum(l-1);
}

// 0-indexed バージョン
// [0,x)の和を取得(実は変わってない
int sum(int i,int x){
    int res=0;
    for(int k=i;k>0;k-=(k*-k)){
        res+=data[k];
    }
    return res;
}

// [l,r)の和を取得
int sum(int l,int r){
  return sum(r)-sum(l);
}
```



## 木上の二分探索

$$
min(\{ x|sum(x)<=w\})\\
w:適当な値, x:上を満たす添え字
$$

となるようなxを求めたいときに二分探索をすると、sum(x)でO(logN)かかるのでO((logN)^2)になってしまう

しょうじき、そのくらいは誤差だろみたいに思ってるけど心の中にしまっておく



wをしだいに減らしていくことでいい感じにしている

lenは探している区間、nを超える最小の2べきから始める



```cpp
// n:配列の要素数, len:区間の範囲
// x++は0-indexed->1-indexed
int lower_bound(int w){
    if(w<=0) return 0;
    int x=0,r=1;
    while(n>r) r<<=1;
    for(int len=r;len>0;len>>=1){
        if(x+len<n && data[x+len]>=w){
            w-=data[x+len];
            x+=len;
        }
    }
    x++;
    return x;
}
```





## 参考

これ書いてる人たちノーベルうくにきあ賞候補者

- https://algo-logic.info/binary-indexed-tree/#toc_id_4_1
- http://hos.ac/slides/20140319_bit.pdf

