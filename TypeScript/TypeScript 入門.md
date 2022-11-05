# TypeScript 入門



## 環境構築

```bash
$ npm install -g typescript
```

これをすると`tsc`（TypeScript Conpiler）が入る

```bash
$ tsc hoge.ts
$ node hoge.js
```

みたいなかんじでトランスパイルして`.js`ファイルを実行するかたち



# 構文



基本的には JavaScript と一緒



型は変数のうしろにつく

```typescript
const n: number = 0;
const a: string[] = [];
const b: Array<string> = [];
// a と b は同じ意味

function hoge(s: string) : void {
  console.log(s);
}
```



## 型エイリアス

```typescript
type numstr = number | string
type hello = 'Hello'
```

type で新しい型を作れる



## Generics

```typescript
const a:Array<string> = [];
const b:Array<number> = [];
```

c++ の vector っぽい



c++ の template っぽく作ることもできる

```typescript
function test<T>(arg: T): T {
  return arg;
}

type mypair<T1,T2> = {
  first: T1,
  second: T2,
}

class mytrio<T1,T2,T3> {
  first: T1;
  second: T2;
  third: T3;
}
```



## オブジェクト

```typescript
const a: { value: number } = {};

a.value = 10;
```

型で明示すると、それが前提となった動きをしてくれる



c++ でいう pair の配列っぽいことができる

```typescript
const a: Array<{A:number, B:number}> = [];
```



## スーパークラスとサブクラス

string は文字リテラルのスーパークラス

文字リテラルは string のサブクラス



親子の関係がある

