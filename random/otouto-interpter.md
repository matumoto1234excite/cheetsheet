# otouto-interpter



### elseStatement の isError が必要な理由

トークンのタイプが `Else` じゃないときは `isError: false` として返す

これはつまり、elseStatement が呼び出されたときにelse が続いていなかったことを表している

```
if (コンディション) {
    文
} else {
    文
}
```

というようにしており、if のあとは else の有無にかかわらず parseElseStatement を呼び出しているからこれをしている



isError が true となるときは？

- 上のプログラムの else の文（elseStatementとなるところ）がエラーだったとき



そのときに限って `isError`をtrue にしている



この区別のために isError がいるっぽい



え？parseElseStatementを呼び出すときに判別できそうだけど...
うー－ん



Elseトークンが存在しているかどうかを確認→`parseElseStatement`を呼び出す
の形にするべきですね



Elseトークンが存在していなかったらただの if 文になるだけだし



結論として、isErrorはいらなくて `optional`でいいです



### 再帰データ型の表現

再帰データ型とかいいながら、別にそんなことをしなくてもよさそうな気がしてきた

本来であれば Boost.Variant の recursion variant 型 とかを使う場面ではありそうだけど、二分探索木のときみたいに普通にポインタメンバ変数を持てば解決しそう



![image-20211228215830373](C:\Users\matum\AppData\Roaming\Typora\typora-user-images\image-20211228215830373.png)

となっていることから、

```cpp
struct IfStatement;
struct Assignment;
struct Expression;

using Statement = std::variant<IfStatement, Assignment, Expression>;

struct IfStatement {
  Statement *statement;
};
```

みたいな実装で動くんじゃないかな





## Statement

スマートポインタについて軽く勉強したので、Statementについては下の実装にしよう

```cpp
#include "Assignment.hpp"
#include "Expression.hpp"

struct IfStatement;

using Statement = std::optional<std::variant<IfStatement, Assignment, Expression>>>;

struct IfStatement {
  unique_ptr<Statement> stmt_ptr;
  IfStatement(): stmt_ptr(nullptr) {}
};
```



みたいな感じで

`unique_ptr`については`shared_ptr`にしてもいいかも





### lexical-analyzer で返ってくるもの

lexical-analyzerは渡された文字列をトークン列にして返す



`vector<Token>`を返す感じでよい？

`optional<vector<Token>>`で良さそう

```cpp
using Tokens = std::vector<Token>;
optional<Tokens> lexical_analyze(std::string s){
}
```

で良さそう





### Token はどうしようか

3種類のTokenがいる

- typeだけを持つToken

  `SymbolToken`

- typeとvalueを持つToken

  `IntToken`,`BoolToken`

- typeとnameを持つToken

  `IdentifierToken`



Token は `Token::type` で判別できれば良い



インタプリタなので実行時に判別できるようにしたいから、型(コンパイル時)で判別するようにはしなくていい

※インタプリタじゃなくて静的型付けの言語にしたいんだったらここで型で判別するようにすればよさそう



typeを`std::string`で扱えばいいだけの話ではあるんだけど、より厳しく制限したい

具体的には、

```ts
type Parens = 'LParen' | 'RParen'
type Braces = 'LBrace' | 'RBrace'
type LogicOpeSymbol = 'Not' | 'PipePipe' | 'AndAnd' | 'And' | 'Pipe'
type CompareSymbol = 'LEqual' | 'LThan' | 'EqualEqual' | 'NotEqual' | 'EqualEqualEqual' | 'NotEqualEqual'
type Symbols = (
    'Asterisk'| 'Slash' | 'Equal' | 'Plus' | 'Minus' |'Comma' | 'Semicolon' |
    CompareSymbol | Parens | Braces |LogicOpeSymbol
)

type SymbolToken = { type: Symbols }
type IdentToken = {
    type: 'Ident',
    name: string
}
type IntToken = {
    type: 'Int',
    value: number
}
type BoolToken = {
    type: 'Bool',
    value: boolean
}
type Keyword = 'If' | 'Else' | 'Def' | 'Null'
type KeywordToken = BoolToken | { type: Keyword }
type UnknownCharacterToken = {
    type: 'UnknownCharacter',
    value: string
}
export type Token = SymbolToken | IdentToken | IntToken | KeywordToken | UnknownCharacterToken
export type Tokens = Token[]
```



のように、指定した文字列のみが入るようにしたい

これは C++20 以降の concept でできることですかね

C++17 で作ろうと思ってるのでまあ妥協?

いや、全ての型をstructで作ればいいのか？

むりで～～す　std::variant のネストが深くなるし、わかりづらくなってる



どうせ構文解析ライブラリにはならないし、C++20で作っちゃうか

正確にはdraft版のC++2aだけど

g++-11 の `-std=c++20`を使うと正式版が使える

すげー



type の分岐を concept に落とし込みたい

concept って自作できるのか？

おそらくは可能

```cpp
template <typename T>
concept Addable = requires (T a, T b) {
  a + b;
};

template <typename T>
requires Addable
void add_print(T a, T b, T c) {
  std::cout << a + b + c << std::endl;
}
```



のように書くことができる

ただし、

```cpp
template <typename T>
concept AAA = requires (T s) {
  s == "aaa";
};

template <typename T>
requires AAA
void add_print(T s) {
  std::cout << a << std::endl;
}
```

みたいにしてもsの値を`"aaa"`だけには制限できなかった

これはほんとに謎



メンバ変数か関数を持たせてそれで分岐とかはどうだろう

そもそも分岐が concept でできるようになりそう



```cpp
struct Token {
  std::string type;
  
  Token() = default;
  Token(std::string t): type(t){}
};
```



`types`のほかに`concepts`みたいなディレクトリを作るのが必要そうだと思いつきました

というか、types の代わりになりうる？



```cpp
template <typename T>
concept IntLiteral = requires (T a) {
  a.IntLiteral();
};
```

みたいな concept を作りまくる



ということで作ってみたがこんなのはどうだろう

```cpp
#include <bits/stdc++.h>
using namespace std;


class IntLiteral {
  int value_;

public:
  struct IntLiteral_t;

  IntLiteral() = default;
  IntLiteral(int v){};

  int val() const { return value_; };
  void set(int v) { value_ = v; };
};

class BoolLiteral {
  bool value_;

public:
  BoolLiteral() = default;
  BoolLiteral(bool v){};

  static constexpr string_view type = "BoolLiteral";

  bool val() const { return value_; };
  void set(bool v) { value_ = v; };
};

template <typename T>
concept IntLiteralConcept = requires(T a) {
  typename T::IntLiteral_t;
};

template <typename T>
requires IntLiteralConcept<T>
void print_IntLiteral(T a) {
  cout << T::type << endl;
}

int main() {
  IntLiteral i(10);

  print_IntLiteral(i); // ok IntLiteralConcept を満たしている

  BoolLiteral b(true);
  
  print_IntLiteral(b); // エラー！ BoolLiteral::IntLiteral_t は存在しない
}
```

う、うー－－ん



まあなくはないかも



## Expression

はいきたやばいやつ

再帰しまくり、なにこれ



![image-20220101234940899](C:\Users\matum\AppData\Roaming\Typora\typora-user-images\image-20220101234940899.png)

お？地獄か？ほとんど双方向になってない？おしまいおしまい



ただ、コードで見るとかなり分かりやすい



```ts
// expressionTypes.ts の一部

type IntLiteral = { type: 'IntLiteral', value: number }
type BoolLiteral = { type: 'BoolLiteral', value: boolean }
type NullLiteral = { type: 'NullLiteral' }
export type Literal = IntLiteral | BoolLiteral | NullLiteral

export type Variable = {
    type: 'Variable',
    name: string
}

export type FuncCall = {
    type: 'FuncCall',
    name: string,
    arguments: Expression[]
}

type InfixOperation<T extends string> = {
    type: T,
    left: Expression,
    right: Expression
}

export type AddSubMulDiv = InfixOperation<'Sub' | 'Add' | 'Mul' | 'Div'>

export type OrOperation = InfixOperation<'OrOperation'>

export type AndOperation = InfixOperation<'AndOperation'>

export type LogicalOperation = OrOperation | AndOperation

export type UnaryOperator = {
    type: 'UnaryPlus' | 'UnaryMinus' | 'UnaryNot',
    expression: Expression
}

export type HighLevelCompare = {
    type: 'HighLevelCompare',
    kindOfCompare: '===' | '!==' | '<=' | '<',
    left: Expression,
    right: Expression
}
export type LowLevelCompare = {
    type: 'LowLevelCompare',
    kindOfCompare: '===' | '!==',
    left: Expression,
    right: Expression
}

type Compare = HighLevelCompare | LowLevelCompare

export type Expression = Literal | Variable | FuncCall | AddSubMulDiv | UnaryOperator | Compare | LogicalOperation
```



本質としては

```ts
export type FuncCall = {
    type: 'FuncCall',
    name: string,
    arguments: Expression[]
}

export type Expression = FuncCall
```

みたいなところ



これを解決できればほかも全部解決する





とりあえず、スマートポインタを使ってやってみる

```cpp
struct FuncCall;

using Expression = FuncCall;

struct FuncCall {
  std::string type;
  std::string name;
  std::vector<std::unique_ptr<Expression>> arguments;
};
```

みたいな感じか



割となんとかなりそうなんだよねこれで



Expressionのめんどくさいことは先に宣言が必要だからファイルで分けない方が理解しやすいということ

でもファイルでわけたい気持ちがあるよねー



### unique_ptr か shared_ptr か問題

できるかぎり unique_ptr にしたいが...



なんか unique_ptr で良いような気がしています

関数呼び出し→expressionを使用 みたいなことが多いけど、それって毎回 move できますよね

じゃあオッケーか？



オッケーじゃないです

unique_ptr にしないといけない理由があって、Expression のコピーができなくなる

`Expression &` から `Expression` への変換が不可能になってしまうので `shared_ptr`になる

なんで不可能になるかっていうと、`Expression = variant<AddSubMulDiv, FunctionCalling>; ` みたいになっているが、これらすべての型で `T operator=(T&)`（コピー演算子）がある必要があって、それってメンバのコピーをする必要があるわけなんだけど、むりなんだよね

unique_ptr がメンバにいるせいで

なので、自分でコピー演算子をmoveで定義することもできるけど、コピーだけどコピーしてない演算子を定義するのは論外なのでshared_ptr にすべき





### 設計について

基本的には Add型 Sub 型 Mul 型 Div 型 を作って

`AddSubMulDiv<Add>`みたいにして使うべき

そうすると

```cpp
if constexpr (is_same_v<AddSubMulDiv<Add>, decltype(a)>) {
  
}
```

みたいな分岐が可能になる



そういう設計にすると、`static constexpr string_view type;`がいらなくなる
