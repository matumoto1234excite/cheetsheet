# watchプロパティ



これで`dataReady`変更時に`watch`で読み取られる

```vue
<script>
export default {
  data() {
    return {
      restaurants: []
    }
  },
  computed: {
    dataReady: function(){
      return this.$store.state.restaurants.dataReady;
    }
  },
  watch: {
    dataReady(newDataReady, oldDataReady) {
      console.log(oldDataReady);
      if(newDataReady){
        this.restaurants = this.$store.state.restaurants.restaurants;
      }
    }
  },
}
</script>
```



なぜこうなったのか

そもそも、computed内の関数で値を変えようとすると副作用を許さないらしく、代入などが行えない



そのため、dataもしくはcomputedの値の変更を監視できるwatchプロパティを使う必要がある

watchプロパティで作った関数は第一引数に新しい値、第二引数に古い値が入る