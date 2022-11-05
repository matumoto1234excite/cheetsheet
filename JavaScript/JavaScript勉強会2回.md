# JavaScript勉強会2回



## browserの開発者モードを使おう

開いているページのHTMLを見ることができる

ショートカットはShift + Ctrl + i



## HTMLについて

Hyper Text Markup Language

- tag

  imgやdiv

- id

  Attribute

  一つのHTMLの中で同じidは１つしか使えない

  一つのHTMLの要素に割り当てられるidは一つのみ

- class

  何回でも使えるid



## CSSについて

Cascading Style Sheets



```css
// タグ
body {
    // 中身
}

// class
.content {
    // 中身
}

// id
#hoge {
    // 中身
}
```





## DOM API

Document Object Modelの略

HTMLの要素をJavaScriptで取得し操作することができる

ブラウザで https://sccp2021.github.io/html_learn/ にアクセス

開発者ツールでコンソールを開く

以下を実行

```js
document.getElementById("main")
document.getElementById("greeting")
document.getElementsByClassName("content")
document.getElementsByTagName("div")
let greeting = document.getElementById("greeting")
greeting.textContent = "I'm matsumoto hibiki."
```



代表的なDOM API

- document

  ページ全体の情報を扱うオブジェクト

  このオブジェクトを操作することで、HTMLの中の要素を取り出して操作することができる

- element

  HTMLの要素を扱うオブジェクト

- document.getElementById

  document(今開いているページ)から、idをもとにelementを1つ取り出す

  これだけgetElementで単数形なのはidは一つしかないため

- document.getElementsByClassName

  documentから、classをもとにelementを取り出す

- document.createElement

  elementを作る

- element.appendChild

  elementの子を追加する

- element.remove

  自分自身を取り除く

以下をためしてみる

```js
const main = document.getElementById("main")
const pElement = document.createElement("p")
pElement.textContent = "Hello World!!!!!!!!!!!!!!!!!!"
main.appendChild(pElement)
pElement.remove()
```



よく使うもの

- hoge.textContent

  要素の文字列

- hoge.value

  inputとかにある入力された文字列



EventListner

関数を引数に受け取ってイベントが起こった際にその関数を実行する

```js
function onButtonClick() {
  const input = document.getElementById("inputText")
  const output = document.getElementById("outputText")
  output.textContent = input.value
}


const button = document.getElementById("showButton")
button.addEventListener("click", onButtonClick)
```



無名関数

```js
const button = document.getElementById("showButton")
button.addEventListener("click", function() {
  const input = document.getElementById("inputText")
  const output = document.getElementById("outputText")
  output.textContent = input.value
})
```

関数を引数に取るときに無名関数にすることもできる



TODOリストアプリ

https://qiita.com/atlansien/items/c582fe2c6d5af943e55c