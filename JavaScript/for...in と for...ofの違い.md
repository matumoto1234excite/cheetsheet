# for...in と for...ofの違い



これを見よう

https://qiita.com/a05kk/items/d6f49ca5bd15f045ea6c



- 配列に対して`for...in`は使えない

  - `for...of`もしくは`Arrays.forEach()`を使いましょう

- `for...in`はオブジェクトに使う

  - ```js
    var myTeam = {
        name: '本田',
        age: '33',
        birthplace: '大阪'
    }
    
    for( var item in myTeam){
        console.log(item);
    } 
    
    //name
    //age
    //birthplace
    ```

- 

