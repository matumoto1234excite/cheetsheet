# Nuxt.jsアプリを GitHub Pages に自動デプロイする



自動といっても半自動？

コマンドを打つとデプロイするようにするだけ





1. ```bash
   $ npm install push-dir --save
   ```

2. ```json
   // package.json
   "scripts": {
     "deploy": "push-dir --dir=dist --branch=gh-pages --cleanup"
   }
   ```

3. パスの変更（faviconなど）

   ```js
   // nuxt.config.js
   
   head: {
     title: pkg.name,
     meta: [
       { charset: 'utf-8' },
       { name: 'viewport', content: 'width=device-width, initial-scale=1' },
       { hid: 'description', name: 'description', content: pkg.description }
     ],
     link: [
       { rel: 'icon', type: 'image/x-icon', href: '/<リポジトリ名>/favicon.ico' }
     ]
   },
   ```

   ```js
   // nuxt.config.js
   router: {
     base: '/<リポジトリ名>/'
   },
   ```

   

4. `npm run generate`

5. `npm run deploy`





## 参考

- https://upd.world/nuxtjs-deploy-gh-pages/
- https://github.com/L33T-KR3W/push-dir