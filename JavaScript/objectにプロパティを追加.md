# objectにプロパティを追加



ここに書いてある

https://qiita.com/chihiro/items/eb8c7b2ceee5274a4a8f



実際やるだけ

```js
let user = {
  id: 1,
  name: "name",
};

user.country = "Japan";
user["language"] = "jp";

console.log("user", user);

// user Object {id: 1, name: "name", country: "Japan", language: "jp"}
```

要素を指定して代入するだけで入る

