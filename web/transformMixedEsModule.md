# ビルド後にrequireが残っていて、ブラウザでエラーになるやつ

[ここ](https://azukiazusa.dev/blog/vite-require/) とか見るとブラウザじゃ`require`が使えないことがちゃんと書かれているし、なんなら見える箇所での`require`は`import`に変えればいいよと書いてくれている

でも、`node_modules`内とかの見えない場所で`require`が使われていたら、修正しようがないじゃんという問題がある

- [viteのそれっぽいissue](https://github.com/vitejs/vite/issues/3409)

動くようにするためには、以下をコンフィグに書き込めばOK

```js
export default {
  build: {
    commonjsOptions: {
      transformMixedEsModules: true,
    },
  },
},
```

もし仮に問題のあるパッケージが特定できているなら、[このプラグイン](https://github.com/originjs/vite-plugins/tree/main/packages/vite-plugin-commonjs)を試してみるのもあり
