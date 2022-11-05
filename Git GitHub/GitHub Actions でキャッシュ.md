# GitHub Actions でキャッシュ



- [公式ドキュメント](https://github.com/actions/cache)



↑のやつを使えばよい



- [npm ci をするときの参考](https://dev.classmethod.jp/articles/cicd-npm-ci-cache/)



npm による CI をするときは `npm i` ではなく `npm ci` をすべき



- `npm i`

  package.json を参照して node_modules を生成する
  既存の node_modules があった場合は差分だけ install を行う

- `npm ci`

  package-lock.json を参照して node_modules を生成する

  既存の node_modules があった場合でもそれを上書きする形で新しく構築する

  また、package-lock.json は環境などで `npm i` が行われたときのバージョンが記述されているため、CI環境とローカルでの差が生まれない



ということで、CI をまわす場合は `npm ci`　をしたほうがよい



そして、node_modules のキャッシュはとっても新しく構築してしまい意味がないので ~/.npm をキャッシュすべき

> npmは、パッケージをインストールする際に `~/.npm` にキャッシュを保存し、同じパッケージが必要になった場合に、ネットワークへのアクセスなくインストールが可能です。
> そのため、 `npm ci` を行う場合でも `~/.npm` をキャッシュすれば、インストールの高速化を図ることができます。



ということなので、npm ci を使って ~/.npm をキャッシュしようね