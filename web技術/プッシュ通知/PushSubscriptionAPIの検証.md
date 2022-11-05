# PushSubscriptionとFirebaseCloudMessagingを用いた実装

こんにちは、現在エキサイト株式会社のメディア事業部でインターンをさせていただいている松本[^1]です

ちょうどPush APIの[PushSubscription](https://developer.mozilla.org/ja/docs/Web/API/PushSubscription)を知る機会があったので、検証も兼ねて簡単な実装をしてみました

なお、今回実装してみたコードは以下のGitHubリポジトリで公開しています

<!-- TODO: ここにGitHubリポジトリのリンク -->

## PushSubscriptionとは？

ブラウザのWebプッシュ通知にまつわる [Push API](https://developer.mozilla.org/ja/docs/Web/API/Push_API) の機能の一つです

似たようなWeb APIに [Notification API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API/Using_the_Notifications_API) というものがありますが、別の役割を持っています

ざっくりとした違いは、Push API がサーバからブラウザに対してのものであり、Notification APIはブラウザからOSへのものであるといった感じです  

Push APIの [PushSubscription.endpoint](https://developer.mozilla.org/ja/docs/Web/API/PushSubscription/endpoint) から提供されるエンドポイントにHTTPリクエストを送ることで、Webプッシュ通知を実装することができます

## FirebaseCloudMessagingを使用したWebプッシュ通知の仕組み

<!-- 今回は FirebaseCloudMessaging を Push API と併せて使用してみましたが、Firebaseの他にも PubNob や Pusher といったサービスがあったりします -->



## なにを検証したのか

## 実装したコード

## 実装したコードの説明

## あとがき

## 参考

[^1]: https://twitter.com/matumoto_1234
