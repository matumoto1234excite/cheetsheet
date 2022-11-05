# nuxt.jsでliff



nuxt.jsでliffを使うにはそこら辺にあるサイトのようにやってもうまくできない

というか、`import liff from "@line/liff;"`を`index.vue`とかで書くと`window is not defined`というエラーが出て動かなくなってしまう

その原因はnode.jsでwindowが使えないのに@line/liffパッケージのindex.jsでwindowを使ってしまっているため

それを回避するにはnode.jsを使っているサーバー側ではなくて、クライアント側でのみ動くようにする必要がある

じゃあ、それをnuxt.jsでやるにはどうするか



nuxt.jsのpluginsには呼び出す際にモードを指定できるのでそれを使う

```js
// nuxt.config.js
export default {
  plugins: [
    { src: '~/plugins/liff.js', mode: 'client' }
  ],
}
```

modeでclientを設定するとクライアント側でのみ動くようになる



plugins/liff.jsでは次のようにすると`hoge.vue`とかで`this.$liffinit(liffId)`で呼び出せるようになる

```js
// plugins/liff.js
import Vue from 'vue';
import liff from "@line/liff";


Vue.prototype.$liffInit = async ( liffId ) => {
  const res = await liff.init({ liffId: liffId });
  console.log(res);


  if (!liff.isInClient() && !liff.isLoggedIn()) {
    liff.login();
  } else {
    const isInClient = liff.isInClient();
    console.log(isInClient);
    liff.getProfile()
      .then(profile => {
        const userName = profile.displayName;
        console.log(userName);
      })
  }
}
```



```vue
<script>
export default {
  this.$liffInit(this.$config.liffId)
    .then(() => {
      console.log("hello. Loginning now!");
    });
}
</script>
```



