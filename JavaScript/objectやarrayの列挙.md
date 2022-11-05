# 列挙

配列の列挙

範囲for文を使おう

```js
hoge = [3,1,4,1,5];
for(const element of hoge.values()){
    console.log(element);
}
```



オブジェクトの列挙

```js
hoge = {
    name: 'matumoto',
    title: 'movie',
    age: 10101,
};
for(const element of Object.keys(hoge)){ // key
    console.log(element);
}
for(const element of Object.values(hoge)){ // value
    console.log(element);
}
for(const element of Object.entries(hoge)){ // [key,value]の配列
    console.log(element[0] + ' ' + element[1]);
}
for(const [key,val] of Object.entries(hoge)){
    console.log(key + ' ' + val);
}
```

