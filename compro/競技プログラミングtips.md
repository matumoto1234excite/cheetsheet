# 競技プログラミングtips



- 実験しろ！

- コーナーケースを考えろ！（制約のMIN MAX）

- doubleは怖い

- 答えで二分探索するといい。答えが決まっていたらO(N)で判定できるかを考える

- priority_queueとか使うと行ける問題もある

- 制約で犯罪考察しろ

  N=10^12だったらsqrt(N)で考える

  sqrt(N)より大きいか小さいかで場合分けする
  
- やばい計算式はWolframにつっこむ

- 末尾の要素とswapしてpop_backすれば真ん中も消せる

- modがちいさいときは鳩ノ巣原理を考える

- 最適に選んだ系では片方を最低点基準にして言い換える

  ```
  例:a_iとb_iを最適に選んだ時の差の最大値は？ => -b_1-b_2...-b_nを始めとしたときのa_iを選んだ和の最大値は？
  ```

- https://algo-logic.info/how-to-think-cp/#toc_id_1_8ココ見ればいい

- XORはビットごとに独立。DFS60回やるみたいなこともできる。

- Zero Sum Rangesは使えそうか？

- aとbをつなぐ辺はG[b]=aとかG[a]=bとかで表せる

- Functional Graphはありませんか？



## クエリ系

### 差分更新を考える

ある数列があって、a_i -> x に更新したときの総和は？みたいな問題であらかじめ全体の総和を求めておいて、個々の差分を更新することでO(1)とかO(logN)とかでクエリを処理する



### クエリを先読みして座標圧縮

```cpp
template <typename T>
vector<T> compress(vector<T> a){
    vector<T> res=a;
    sort(a.begin(),a.end());
    a.erase(unique(a.begin(),a.end()),a.end());
    for(int &x:res) x=lower_bound(a.begin(),a.end(),x)-a.begin();
    return res;
}
```

座標圧縮は上のコードでできる。あらかじめソートしてユニークしておけば、二分探索のO(logN)で値->座標圧縮後のインデックスを取得できる。

`fenwick_tree`（フェネック木もしくはBinaryIndexedTree)と相性がいいので色々考える価値はありそう。

a_i以下の値の個数の場合

aを座標圧縮しておいてfenwick_treeで管理する。(`fenwick_tree.add(座標圧縮後のインデックス, 1);`)

0~座標圧縮後のインデックスで、その値以下の個数が分かる。



## XをYにする系

数とか数列に操作を行ってYにしてくださいみたいなやつ。

### YからXを考える。

逆からできるか考えてみる。



## 数式系

### 天井関数

$$
\lceil \frac{a}{b} \rceil
$$

を求めたいなら
$$
\frac{a}{b} \leq x となる最小の整数x
$$
を考える。

