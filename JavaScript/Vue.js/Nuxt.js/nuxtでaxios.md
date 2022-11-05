# nuxtでaxios



nuxtはaxiosをするには普通のaxiosを使うより`@nuxtjs/axios`を使う方が簡単にできる

色んなサイトで`asyncData`を使っているけどそんなものを使わなくても`mounted(){}`で動かせる



nuxt.config.jsにmoduleを追加すればOK

あと、nuxt.config.jsでproxyをうにょうにょするはず

https://zenn.dev/mouse_484/articles/nuxt-axios-cors



```vue
<script>
export default {
  mounted() {
    this.$axios.post("https://ic0tkzuy55.execute-api.ap-northeast-1.amazonaws.com/tk/test")
      .then((res) => {
        console.log("cors succeeded!");
        console.log(res);
      })
      .catch((err) => {
        console.log("cors error!");
        console.log(err);
      });
  }
}
</script>
```



