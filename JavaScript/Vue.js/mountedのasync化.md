# mountedのasync化



mounted内で非同期処理を行いたいときはどうしたらよいのか

```vue
<script>
export default {
  data() {
    return {
      hogeData: 0,
      // other some data...
    }
  },
  mounted() {
    thenData();
    hogeData = somethingAsyncFunction();
  }
}
</script>
```



答えはここに書いてあった

https://stackoverflow.com/questions/53513538/is-async-await-available-in-vue-js-mounted



```vue
<template>
  <div v-if="dataReady">
    <!-- write your html... -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataReady: false,
      hogeData: 0,
      // other some data...
    }
  },
  async mounted() {
    await thenData();
    hogeData = await somethingAsyncFunction();
    this.dataReady = true;
  }
}
</script>
```



この書き方、頭がよい

