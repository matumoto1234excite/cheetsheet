# testlibについて



## patternについて



- [ソースコードのコメント部分](https://github.com/MikeMirzayanov/testlib/blob/master/testlib.h#L480)

- [ソースコードの実装部分](https://github.com/MikeMirzayanov/testlib/blob/master/testlib.h#L1104)



> Very simple regex-like pattern.
> It used for two purposes: validation and generation.
>
> For example, pattern("[a-z]{1,5}").next(rnd) will return random string from lowercase latin letters with length from 1 to 5.
> It is easier to call rnd.next("[a-z]{1,5}") for the same effect. 
>
> Another samples:
> "mike|john" will generate (match) "mike" or "john";
> "-?[1-9][0-9]{0,3}" will generate (match) non-zero integers from -9999 to 9999;
> "id-([ac]|b{2})" will generate (match) "id-a", "id-bb", "id-c";
> "[^0-9]*" will match sequences (empty or non-empty) without digits, you can't use it for generations.
>
> You can't use pattern for generation if it contains meta-symbol '*'.
> Also it is not recommended to use it for char-sets with meta-symbol '^' like [^a-z].
>
> For matching very simple greedy algorithm is used.
> For example, pattern "[0-9]?1" will not match "1", because of greedy nature of matching.
> Alternations (meta-symbols "|") are processed with brute-force algorithm, so do not use many alternations in one expression.
>
> If you want to use one expression many times it is better to compile it into a single pattern like "pattern p("[a-z]+")".
> Later you can use "p.matches(std::string s)" or "p.next(random_t& rd)" to check matching or generate new string by pattern.
>
> Simpler way to read token and check it for pattern matching is "inf.readToken("[a-z]+")".
>
> All spaces are ignored in regex, unless escaped with \.
> For example, ouf.readLine("NO SOLUTION") will expect "NOSOLUTION", the correct call should be ouf.readLine("NO\\ SOLUTION") or ouf.readLine(R"(NO\ SOLUTION)") if you prefer raw string literals from C++11.
>
>
> (testlib.h 中のコメントより)



これを要約すると、

- testlib 内で使用される pattern は正規表現に近いものになっている
- 基本的に validation と generation 用に使用されるが、繰り返し記号の`*`や否定記号の`^`といったものは生成の際には使用できない
- pattern の仕様として `|`は全探索アルゴリズムを用いて実装されているため同じ文中に`|`を多用するのは避けてほしい
- 正規表現では空白が無視されることから、`"NO SOLUTION"`という文字列を想定して読み取りたければ`inf.readLine("NO\\ SOLUTION")`のようにしてエスケープをする必要がある



以下認識される記号

- `?`
  - 直前の文字があるなしにマッチ[^1]
- `*`
  - 直前の文字を0回以上繰り返す[^2]
- `+`
  - 直前の文字を1回以上繰り返す[^3]
- `{from,to}`
  - 直前の文字をfromからto回繰り返す
  - `{to}`であった場合はfrom=toの`{from,to}`と認識される
  - `{from,to,a,b,...,}`となった場合はfromとtoのみが認識される
- `[chars]`
  - `[]`で囲われた文字の内どれかが認識される
  - `-`記号が使われていた場合、両隣の文字を認識し、左の文字を`prev`,右の文字を`next`とすると、文字コード上での`[prev,next]`間の文字を展開する（`[a-f]`であれば`[abcdef]`となる）
- `()`
  - `()`で囲われた文字が pattern として認識される（正規表現と同じ使い方）



[^1]:実装上は`{0,1}`となっている
[^2]:実装上は`{0,INT_MAX}`となっている
[^3]:実装上は`{1,INT_MAX}`となっている
