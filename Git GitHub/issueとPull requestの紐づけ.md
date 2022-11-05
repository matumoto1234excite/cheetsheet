# issueとPull requestの紐づけ

二つの方法がある

- commit時にリンクさせる

  ```shell
  $ git commit -m "README.md #2 修正"
  ```

  「#issue番号」をメッセージに入れると該当するissueページに自動でリンクを付与してくれる。

  ```sh
  $ git commit -m "update README.md close #1"
  ```

  「close #issue番号」を入れるとがいとうするissueを自動でクローズしてくれる。

  ソースはこれ[GitHubのissueとcommitを紐付ける](https://qiita.com/cotolier_risa/items/210db74e6496d4359be7)

  

- GitHubから手動でリンクさせる

  プルリクエストの右側の欄に「Linked issues」があるからそこで選択する。

  詳しくはこれ[公式ドキュメント](https://docs.github.com/ja/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue)

  



