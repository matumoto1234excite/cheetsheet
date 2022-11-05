# 全方位木DP（ReRootingDP）

えー難しいです



## お気持ち

お気持ちだけなら割と分かりやすい

というか使い方だけがむずすぎる

1. 全頂点に対するなんらかの値を一括に求めたい
2. 一回の計算で根の値と子方向への値は求められる。（親方向への値は求められていない）
3. 根を親とする頂点たちは唯一、親の値が分かっているので求められる。
4. 3を再帰

全頂点を数回探索するだけなので $O(N)$



- [keymoonの記事](https://qiita.com/keymoon/items/2a52f1b0fb7ef67fb89e)



keymoonの記事で実装したものに準拠すると全方位木DPに必要なものは

- 木の情報（頂点数と辺）
- 単位元（identify）
- 二項演算（merge）
- 自分自身を根として隣接頂点の演算結果の総積に加える操作（addNode）

だけ





木の情報はいいとして、単位元と二項演算はモノイド（結合法則と単位元）である必要がある



問題はaddNode

これは自分自身を演算結果に加えるもの



例として、DFSで距離を出そうとするときに、今見ている頂点自身を隣接頂点の演算結果に加えるときには自分自身の距離を含めるという意味で+1する

```cs
int DFS(int root, int parent)
{
    int result = 0;
    //rootの全ての隣接する頂点に対して探索を行う
    foreach (var adjacent in adjacents[root])
    {
        //親方向には辺を伸ばさないようにする(根付き有向木を実現)
        if (adjacent == parent) continue;
        //子部分木についての答えと今までの答えをマージ
        result = Max(result, DFS(adjacent, root));
    }
    //自分のノードの分の深さを追加
    return result + 1;
}
```

これの`result + 1`の+1の部分がそれ



### どういう仕組みなんだ

`childSubtreeRes(par, idx)`:=親parからidx番目の子の値

ここに全てが詰まっている

0--1--2

みたいな木があったとして

childSubtreeRes\[0][0]:=0を親として0番目の子の値（0を親とした頂点1の値）

みたいなのになる





## 使用例

ここからは[ABC220-F](https://atcoder.jp/contests/abc220/tasks/abc220_f)の例を見ていく

### 概要

全頂点を根として、根からの距離のを総和を求める問題



全方位木DPしろって顔に書いてあるのでやる



どうやるんだ？になる



### 仕組みの説明のつづき



入力例1

0--1--2

みたいな木がある

childSubtreeRes\[0][0]:=0を親として0番目の子の値（0を親とした頂点1の値）

なので、childSubtreeRes\[0][0]=2が入る

childSubtreeRes\[1][0]=1（0番目の子は頂点0とする）が入る

childSubtreeRes\[1][1]=1（1番目の子は頂点1とする）が入る



(。´・ω・)ん?値ってなんの値だ？



実際、二種類の値が必要になる

- ある頂点vの子の部分木の総和
- ある頂点rootを根としたときの頂点vの距離



rootはforループで回すとして、決め打つ

そうするとchildSubtreeRes\[root][0からrootの隣接頂点数]の総和を取ればこの問題のrootを根としたときの値が出る

さらにそのついでに自分の隣接頂点を親としたchildSubtreeRes\[adjacent][adjacentから見た自分の番号]も計算できる



隣接頂点を親とした値はそれ以外の方向の隣接頂点の値を足したものなのでいわゆる両方向累積によって可能

あと、自分自身も足すのでaddNodeも忘れずにする

この部分

```cpp
    for ( auto v : order ) {
      int adj_cnt = g[v].size();
      vector<T> accum_back(adj_cnt);
      accum_back.back() = identity;
      for ( int j = adj_cnt - 1; j >= 1; j-- ) {
        accum_back[j - 1] = merge(accum_back[j], ch_tree[v][j]);
      }
      T accum_front = identity;
      for ( int j = 0; j < adj_cnt; j++ ) {
        // g[v][j].firstを親として、それ以外の方向の隣接頂点の値merge(accum_front, accum_back[j])に自分自身を足している
        T res = add_node(merge(accum_front, accum_back[j]), v, *this);
        ch_tree[g[v][j].first][seen_idx[v][j]] = res;
        accum_front = merge(accum_front, ch_tree[v][j]);
      }
      // 隣接頂点の値全てを足して自分自身を加えると自分の値になる
      results[v] = add_node(accum_front, v, *this);
    }
```



つまり

`addNode(res,v)`というのは、resには頂点vの子方向の部分木の総和が入っている

今回の問題のres.firstには子方向の距離の総和とし、res.secondには自分自身の距離とすると

first=自分が子に含まれるようになるので、子方向の総和+自分自身の距離をして、

second=自分自身の距離を加えるので+1をする



というようなものにすれば良い

```cpp
Pll add_node(Pll res, int v, re_rooting_dp<Pll, ll> &tree) {
  // res.first := 子方向の結果
  // res.second := 自分自身の距離
  return Pll(res.first + res.second, res.second + 1);
}
```



あー難しかった