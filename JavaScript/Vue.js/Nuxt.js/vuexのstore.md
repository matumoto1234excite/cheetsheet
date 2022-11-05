# vuexのstore



vue.jsではvuexというのを使用するらしいが、nuxt.jsには標準で入っている

https://ja.nuxtjs.org/docs/2.x/directory-structure/store

詳しくは公式ドキュメントを見よう



`this.$store.state.名前空間.変数`でコンポーネント間でデータを共有することができる

変数の値を変えたいときはそういう関数を作って、それを実行するのがいいかも

![image-20210730185151245](C:\Users\matum\AppData\Roaming\Typora\typora-user-images\image-20210730185151245.png)



変数の値を変更する際は関数にするのが推奨されているらしい



## 変数宣言

`store/hoge.js`内で行う

ファイルの名前が名前空間になっていて、

```js
// hoge.js
export const state = () => ({
  lng: 0,
  lat: 0
})
```

とすると

templateタグ内だと`{{ $store.hoge.state.lng }}`のように使える

scriptタグ内だと`this.$store.hoge.state.lng`

