**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:05](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645977910154669)

よくわからないけど、今回のバックエンドはクリーンアーキテクチャっぽい設計がされていた？

[01:08](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978096623489)

テスト用のデータをその場に全て書いていたのを、せめてtestData.tsとかに置いておくべきだったな。

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:08](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978097343369)

はい

[01:08](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978126961799)

ダミー実装と本実装を簡単に差し替えられる構成になっていました

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:09](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978170606869)

と言うと？

[01:10](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978220953679)

出来上がっていない関数とかは型の合うデータを返すだけの関数として定義しておくとかですか？

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:11](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978308771599)

そうね
Controller, UseCase, Repository, Service
これらを分離することによって疎結合にしていたので

[01:12](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978352110829)

基本的に全てinterfaceで抽象化しているから実装が終わっていなくてもそれを使う部分の実装を進められるし

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:16](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978588672749)

設計って、必要になりそうなものを考えて、それを作っていく上でやりやすい環境を考えることだと思っていますがあってますか？

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:19](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645978797334539)

そうね、割と的を得ていそう

![img](https://ca.slack-edge.com/TA4GGP58B-UJ4M097S9-e4be14027f8a-48)

**[tashiro](https://app.slack.com/team/UJ4M097S9)![:python:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fpython%2Ff72b63720ced4af2.png)**[01:24](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979083061819)

まぁ必要なものって後から気づくパターンもあるから、そういうのに対応しやすいように（変更しやすいように）するのも設計の役目だと思う

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-24)[1 件の返信](https://app.slack.com/client/TA4GGP58B/C021BFKPJ4S)

2ヶ月前スレッドを表示する



![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:26](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979160508489)

クリーンアーキテクチャとかいろいろ手法はあるけど、本質はいかに開発をやりやすくするかな気がする
銀の弾丸はないし

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:26](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979162358489)

よく思っているのが、必要になりそうなものを考えるってめっちゃむずくないですか？
必要になって初めて、あ、作ろってなってしまう。
そうすると設計の後半部分がうまくできていても意味がなくなってしまうので、前半をまずうまくできる様になりたいなと思ったのですが

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:27](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979231833369)

うーん、これは難しい話ではあるな
ただ、必要になったタイミングで今まで書いたコードが障壁にならないようにするのも設計だと思っている

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:27](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979243921029)

確かに？

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:27](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979278216029)

凝集度・結合度をちゃんと考えるとそういう場合に活きてくる

[01:28](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979339185159)

今回のバックエンドもUseCaseを途中で追加で増やす必要があったときにRepository層に処理を適度に分けていたおかげですんなり実装できたのがいくつかあったし

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:29](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979386206279)

なるほど

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:39](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645979962105819)

今思ったのだと、クリーンアーキテクチャの考え方を知った状態だと現状で必要そうなものを考えるのって案外楽になる？Aが必要でそれにはBとCが必要でって言うのを、それぞれクリーンアーキテクチャ上での何とか層に当てはめて考えていくと結構頭が整理されて、じゃあ次はこれが必要だよねって言うのがするする出てくるかも。

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:43](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645980216938159)

そうね
それのベースとなったレイヤードアーキテクチャについて知るとよさそう

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:47](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645980457965439)

発表後のブレイクアウトルームでそんなこと言ってましたね

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:56](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981004962379)

うわ、なんか自作言語でやったことを思い出す

[01:57](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981071827179)

そういえばこう言う時に出てくるビジネスってどんな意味なんでしょう？

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:58](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981138116489)

ビジネスロジックのこと？

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[01:59](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981180175569)

そうですね

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[01:59](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981181151449)

これはあくまで俺の解釈だけど、「エンジニア以外にも理解可能な、日本語で記述可能な処理」

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:00](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981209934389)

なるほど？

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[02:04](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981453571809)

例えば今回のハッカソンだと「LovePointのJSONをクライアントから受け取ってAuthorizationのtokenのユーザーがbroken_atがnullなcoupleを持っていない場合にMySQLのuser_love_pointsテーブルにinsertする」はエンジニアにしか理解できないけど、「ログインしているユーザーが好き度を相手のユーザーIDと一緒に送ると、ログイン中のユーザーが既にカップル成立していないかチェックして、してない場合はサーバー側で好き度を保存する」はエンジニア以外にもある程度理解可能じゃん （編集済み） 

[02:07](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981630431609)

で、俺がよく言うUseCaseってのはこのビジネスロジックを表現する場所のことで、この層ではMySQLとかのことは可能な限り意識せずにこの処理を日本語をそのままプログラミング言語に変換したように書く

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:08](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981698800469)

なるほど

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[02:08](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981719606129)

まあここの書きやすさはある程度言語に依存するんだけどｗ

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:08](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981728944189)

w

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[02:09](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981742816029)

俺的にはfor文ですら使いたくないんだけどGoは書かざるを得ないので……

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:09](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981786576309)

なんか、お疲れ様です

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[02:10](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981807739669)

まあ別にいいんだけどねｗ
今回のチーム開発ではGoが一番いい選択肢だと思ってるし

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:10](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981819685099)

そうですねw

[02:10](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981850188839)

で、実際にどうやってって言うのを、もっと下の層に押し込めていくと

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[02:10](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645981854643669)

そうそう

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:18](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645982291140559)

reactの場合はhooks周りをこう言ったものに当てはめていけばいいんですかね

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[02:23](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645982585375329)

そうね、処理を適切にhooksに分けていけるとよさそうな気はする

![img](https://ca.slack-edge.com/TA4GGP58B-U01ULBXUX1T-ff47d0a80a69-48)

**[ERASER](https://app.slack.com/team/U01ULBXUX1T)**[02:46](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645983998629309)

コンポーネントはAtomic Design、hooksはクリーンアーキテクチャっぽく、ページを最上位層におくのが基本的に良さそうな気がしてきた

[02:47](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645984046511659)

この線で今回のやつ再設計してみるか

[02:51](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645984278445619)

とはいえまずは設計手法と実例学ばないとな

![img](https://ca.slack-edge.com/TA4GGP58B-UA59ULSNP-e9f1255a2ff4-48)

**[マヤミト](https://app.slack.com/team/UA59ULSNP)![:kotlin:](https://slack-imgs.com/?c=1&o1=gu&url=https%3A%2F%2Femoji.slack-edge.com%2FTA4GGP58B%2Fkotlin%2Ff3ac05cd6b1a231d.png)**[04:12](https://zliworkspace.slack.com/archives/C021BFKPJ4S/p1645989174543909)

まあただクライアントサイドはまたサーバーサイドとはちょっと違うし、特にReactとかではあまりクリーンアーキテクチャは見ない気がするから、そのへんちゃんと調べたほうがよさそう