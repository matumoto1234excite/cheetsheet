# Nuxt.jsチートシート



### インストール

[https://nuxtjs.org/docs/2.x/get-started/installation](https://nuxtjs.org/docs/2.x/get-started/installation)

を見るのが速い。大体公式ドキュメントに書いてある。公式ドキュメントが日本語で割と豊富な気がする。



### 実行

```bash
$ npm run dev
$ yarn dev
```

cdでそのディレクトリに移動してからnpmかyarnで実行する。`localhost:3000`とかに作られるはず。



### nuxt.config.js

拡張機能とかを追加したらここに書くことがある。拡張機能をnpmでインストールしたのに、ビルドに失敗するなぁ..とかってときはnuxt.config.jsに書いてなくて失敗していることが多い。



### npm系のコマンドでエラーが出る

```bash
$ rm -rf node_modules/ package-lock.json
$ npm cache clear --force
$ npm cache clean --force
$ npm install
```

自動生成されるnode_modulesとかpackage-lock.jsonを消してから、キャッシュを全部リセットするといい。そして再インストール。

ちなみに、`rm -rf`は`-r`が再帰的(recursive)で、`-f`がyes/noが出ない強制的(force)。



### npm一覧

```bash
$ npm ls --depth=0
```





### router-viewタグ

<template>
    <router-view></router-view>
</template>

という風に`router-view`タグで囲ったところにpagesの中のvueが表示される。



### pagesディレクトリ

pagesは勝手にrouter-vueがなされていて、pages/aiueo.vueとかがあると、`/aiueo`にアクセスしたときにaiueo.vueが表示される。

pages/_id.vueにすると、`/aaaa`にアクセスしたときにaaaaがparams.idという変数になってscriptタグ内で使える。(正直これがよくわかってない)

```html
<script>
export default {
  async asyncData ({ $content, params }) {
    const page = await $content('articles', params.slug).fetch()
    return {
      page
    }
  }
}
</script>
```

これで動くからよくわかんないんだよなー。`async`も知らないし、`await`もよくわからない。これで動くのは`@nuxt/content`を入れているおかげなのかもしれない。てか、たぶんそう。



### remark系

##### remark-collapseがやばい

```js
content: {
    markdown: {
        remarkPlugins: {
        	'remark-collapse'
        }
    }
}
```

ってやると動かなくなる。

`remark`系はだいたい`nuxt.config.js`に書くけど`remark-collapse`だけは書くとバグる。なんで？



## Vue.jsに関して



### Vueの基本構造

```vue
<template>
</template>

<script>
</script>

<style>
</style>
```

みたいな感じの構造になっている。

`<template>`タグは一つのタグしか子に持てないので、

```vue
<template>
	<div>
		hoge...
	</div>
</template>
```

こんな感じにしよう。



### styleタグ

`<style scoped>`ってやるとその.vueファイルだけに適用されるCSSになる。



### scriptタグ

```javascript
export default {
  data: () => ({
    drawer: false,
    menus: [
      {
        name: 'データ構造',
        subMenus: [
          {
            janame: '二分探索',
            enname: 'BinarySearch',
            path: 'binarysearch'
          },
          {
            janame: '累積和',
            enname: 'CumulativeSum',
            path: 'cumulativesum'
          }
        ]
      },
      {
        name: '動的計画法',
        subMenus: [
          {
            janame: '最長共通部分列',
            enname: 'LongestCommonSubsequence',
            path: 'longestcommonsubsequence'
          }
        ]
      }
    ]
  })
}
```

こんなになっている。

```
data: () => ({
	hoge: false
})
```

よりも

```
data: () {
	return {
		hoge: false
	}
}
```

の方が分かりやすいと思う。

__ちなみに、`data:()`ってのは`data:function()`の省略形__





