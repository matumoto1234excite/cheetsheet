# thisとbind



そもそもthisとは？

thisはその時々によって変わるものです。説明が難しいので、例を見てください。

```js
const aaa = function() { alert(this.x); }
const bbb = { x:"b!", f:aaa };
const ccc = { x:"c!", f:aaa };
b.f(); // b!
c.f(); // c!
```

ちなみに、これはアロー関数だとうまく機能しない

```js
const aaa = () => { console.log(this.x); }
const bbb = { x:"b!", f:aaa };
bbb.f(); // undefined
```







ただ、これをコールバック関数とかに渡すと破滅してしまう

```js
setTimeout(function() {
  bbb.f();
},1000);
// B!が1秒後に出力される

setTimeout(bbb.f, 1000);
// undefindが出力される
```

これはなぜかというと、thisがbbbに対してではなくsetTimeoutに対して働いているから



これを固定させるためにbindを使う

bindは関数に対して行うもの

```js
let ccc = { x:"C!", f:aaa };
ccc.f(); // C!
setTimeout(ccc.f, 1000); // undefined
ccc.f = ccc.f.bind({ x:"C2!" });
setTimeout(ccc.f, 1000); // C2!
```



bindで固定化させるとたぶんもう戻れないっぽい

constみたいなものなのかな



より詳しくはこれをみましょう

- https://qiita.com/hamamoto_abc/items/81e6486ef828bd780fa7
- https://foreignkey.toyao.net/archives/763