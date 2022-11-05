# create-react-appできない





```bash
$ npx create-react-app

You are running `create-react-app` 4.0.3, which is behind the latest release (5.0.0).
```



こんな感じで、`create-react-app`できないときは`npx clear-npx-cache`をしてキャッシュを消そう



```bash
$ npx clear-npx-cache

# ついでにエラーメッセージに書かれている通り、グローバルのものをアンインストールする
$ npm uninstall -g create-react-app
```



