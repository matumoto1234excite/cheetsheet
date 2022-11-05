# JavaScript勉強会1回



## 大学のWorkStationにsshで接続しよう

```bash
$ ssh s1280136@sshgate.u-aizu.ac.jp
```





## nodeを立ち上げよう

```bash
$ node --version
```





## JavaScriptの変数

`const`,`let`,`var`があるが、`var`は古いし使わないようにしよう

`const`は定数,`let`は変数



```javascript
let a=1
console.log(a)
a=2
console.log(a)
const b=3
console.log(b)
b=4
console.log(b)
```



## 四則演算

`+`,`-`,`*`,`/`,`%`

左から加,減,乗,除,剰余



## 型

- number

  数を扱う型

  例:`const one = 1`

- string

  文字列を扱う型

  シングルクォーテーションはダブルクォーテーションで囲む

  例:`const str = "Hello, World!"`

- boolean

  真偽値を扱う型

  `true`と`false`のみ

- array

- object



## 配列(array)

`[]`で囲って、カンマ区切りで定義する

例

```javascript
const animals = ["dog", "cat", "bird"]
animals[0] // dog
animals[1] // cat
animals[2] // bird
animals.push("pig")
animals[3] // pig
```



## object

構造体

例

```javascript
const mayamito = {
    name: "Yuta Tomiyama",
    nickname: "mayamito",
    id: "yt8492",
    age: 21
}
console.log(mayamito.name) // Yuta Tomiyama
mayamito.birthday = "20000119"
console.log(mayamito.birthday) // 20000119
```



## JSON

データを文字列で表したもの

JSON.stringifyでJavaScriptの値をJSONの文字列に変換することができる

JSON.parseでJSONの文字列をJavaScriptの値に復元することができる



例

```javascript
const animalsJson=JSON.stringify("animals")
JSON.parse(animalsJson)
const mayamitoJson=JSON.stringify(mayamito) // さっきの構造体
JSON.parse(mayamitoJson) // {"name":"Yuta Tomiyama", "nickname":"mayamito"}
```





## 値の比較

- `===`

  等しいかどうか

- `!==`

  等しくないかどうか

- `<`

  左の値が右の値より小さいかどうか

- `<=`

  左の値が右の値より小さいもしくは等しいかどうか

- `>`

  右の値が左の値より小さいかどうか

- `>=`

  右の値が左の値より小さいもしくは等しいかどうか



## 条件分岐

if文

例

```javascript
const num=8
if(num%2==0) {
    console.log("num is even")
} else if(num%2==1) {
    console.log("num is odd")
} else {
    console.log("なぞです")
}
```



## 繰り返し

for文, while文

```javascript
// for(初期値; 継続条件; 増分){}
for (let i = 0; i<5; i++) {
    console.log(i)
}

// while(継続条件){}
let i = 5
while(i>0){
    console.log(i)
    i--
}
```



## 関数

はい

```js
function is_even(n) {
    if(n%2==0){
        console.log(n+" is even")
    } else {
        console.log(n+" is not even.")
    }
}
is_even(4) // 4 is even
is_even(5) // 5 is not even
```



## アロー関数

```js
// vsはリスト
vs.map(x => parseInt(x, 10));
//↑
//これらは同じ
//↓
vs.map(function(x) {
    return parseInt(x, 10);
})
```

アロー関数が推奨されている

