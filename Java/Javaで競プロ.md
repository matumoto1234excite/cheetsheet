# Javaで競プロ

## テンプレ
テンプレは特にない
`Scanner stdin = new Scanner(System.in);`を毎回書くくらい

## 注意点
ハマった知見とかを注意点として書いていく

### `List<Integer> l = ArrayList<Integer>(1000);`は1000要素確保してくれるわけではない
これね〜、GoやC++で言うところのCapacityを指定しているだけなんだけど、記事とか見てもそれが明記されてないのが悪いよ〜〜〜
侍エンジニアもQiitaの記事も言ってないのが悪い

> 指定した要素数で初期化します

みたいなこと書かれていたら要素数だと思っちゃうよなあ

ちなみに、javaの`ArrayList`はC++の`std::vector`と出来ることがほとんど一緒で、`List`は配列のインターフェースってだけ

### `Stream.map`などはインデックスの情報を持てない
`map`の旨味の半分くらいが消えた
`Stream.filter`, `Stream.forEach`なども同様にインデックスの情報を持てない

### ラムダ式はローカル変数をキャプチャできない
正確には、ヒープ領域にあるローカル変数をキャプチャできないってだけで `final`とかがついた、スタック領域にあるローカル変数はキャプチャできる

つまり、下のようなことができない
```java
int sum = 0;
aList.forEach((a) -> sum += a);
```

まあこの使用自体はそこまで嫌いじゃない
関数として制約が強くていいね、とは思うがラムダ式である意味ある？とも思う


### `Stream.toList()`がAtCoderのバージョンが古くて使えない
バージョン上げてくれ〜〜〜
どのバージョンから使えるようになってるのか知らんけど

代わりに、`Stream.collect(Collections.toList())` みたいに長く書く必要がある

### `Map::merge`はややこしい
`TreeMap`使ってて気づいたんだけど、ややこしい

`Map::merge(key, defaultValue, (defaultValue, value) -> result)`みたいなイメージ（第三引数の関数のdefaultValueとvalueの順番は忘れた）

`List<Integer>`の要素をカウントする`TreeMap`を書くなら下のように書くのが無難
```java
TreeMap<Integer, Integer> counter = new TreeMap<Integer, Integer>();
aList.forEach(a -> {
	counter.merge(a, /*default=*/1, Integer::sum);
});
```

これ、`counter`に対して副作用があって嫌なんだけど、副作用なしで書こうとすると地獄だし、`Stream.map`にインデックスが取れないことから絶望した
```java
TreeMap<Integer, Integer> counter = aList
.stream()
.collect(
		Collectors.groupingBy() ,
		 (map, a) -> map.merge(a, 1, (key, count) -> count + 1),
		 TreeMap::putAll
		 );
```

### ジェネリックのあるクラスのキャストはunchecked警告が欲しい
- https://qiita.com/shojit/items/e6a3ac1b3400b3dc6352
