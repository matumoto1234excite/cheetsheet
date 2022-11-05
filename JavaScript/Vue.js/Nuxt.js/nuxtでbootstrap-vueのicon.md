# nuxtでbootstrap-vueのicon



https://stackoverflow.com/questions/61045853/how-to-include-bootstrap-vue-icons-into-nuxtjs-problem-with-navbar-down-arrows



これを見たら`npm i bootstrap-icons`しろって書いてあるのでやるだけ

```bash
$ npm install --save bootstrap-icons
```

をするだけ

```js
modules: [
  'bootstrap-vue/nuxt',{
    icon
  }

  // ...other modules
]
```





https://bootstrap-vue.org/docs/icons

とか

https://icons.getbootstrap.com/#install

を見ると一覧が見れるので気に入ったのを使おう



