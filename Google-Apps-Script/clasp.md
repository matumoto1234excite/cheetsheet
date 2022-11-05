# clasp

clasp というのは Google Apps Script のプロジェクト管理を楽にするCLI
npm からインストールでき、自分の好きな開発環境で Google Apps Scirpt プロジェクトの編集ができる



[公式サイト](https://github.com/google/clasp)



## form を使ったやり方

ここではひとまず、GoogleFormの回答をDiscordのチャンネルに横流しするものを作る



### 環境構築

環境構築などはまずこれを見て、やればいい

https://dev.classmethod.jp/articles/vscode-clasp-setting/





### WebhookURLを環境変数に入れる

※環境変数は若干ちがくて、正確にはプロジェクトのプロパティ



1. 上の記事を見終わって環境構築が完了したら、Google Apps Scirpt のエディタを開き、クラシックエディタに変更する。（したい設定がクラシックエディタからしかできない）

2. クラシックエディタにしたら、「ファイル」→「プロジェクトのプロパティ」→「スクリプトのプロパティ」でプロパティを設定する（環境変数のようなもの）

3. ここで、DiscordのチャンネルのWebHook URLを値としていれる





### 関数を書く

送信されたときに実行する関数を選べるので、それようの関数を書く

基本的にはこれを見ればOK

https://zenn.dev/akaregi/articles/2e8963e6fd9c50



ただ、Discordに飛ばすということは `:pray:`みたいなのが書かれているとそのままパースされてしまうので若干の注意は必要（ただしく表示させたいのであればマークダウンエスケープみたいなことをする必要あり？）



### トリガーを設定する

トリガーはまあよしなに設定してくれ

GASの画面をブラウザで開くと左側のアイコンの中にトリガー設定のやつがあるからそこで設定できる



基本的には「送信時」をトリガーとすればよさそう（「起動時」ってなにを指しているのかわからん）



### 送信してみる

実際にフォームを送信するとうまくいっているはず（たぶん）





### .clasp.json

.clasp.json についてわかったことを書く



#### parentId は後から変更できない

parentId というのはすでに存在しているGoogleFormだったりを指定したいときにいれる値
GoogleFormとかのURLにあるID部分から取り出せる

`clasp create --parentId "xxxxxxxxxxxxxx"`みたいにプロジェクトを作る時に指定でき、.clasp.json に`parentId`の値が追加されるが、あとから.clasp.jsonを編集しても`clasp push`のときなどに参照されない



実際に.clasp.jsonから`parentId`の値を空配列にして`clasp push`してもエラーが出されなかった(`clasp --version`をして出たバージョンは2.4.1)



#### TypeScript を使用するかは要相談

  TypeScript を使用してコードを書いたとしても、.gsファイルに変換されるときに日本語などがおかしくなる場合があります(実際にバッククオートで日本語を囲った文字列は文字化けしてしまいました)



#### Google chrome で開けない

`clasp open`などで出たGASへのリンクをそのまま踏むと開けないエラーになることがあるが

https://stafftaion.dcf7.com/438/#toc3

を見れば解決する



とりあえず、新しくプロファイルを作るのが手っ取り早そう
