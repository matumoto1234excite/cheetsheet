# FirebaseCloudMessagingのバージョン

2022/08/30現在、以下の2種類が存在する

-   [Legacy HTTP API](https://firebase.google.com/docs/cloud-messaging/http-server-ref?hl=ja)
    
-   [HTTP v1 API](https://firebase.google.com/docs/cloud-messaging/concept-options)
    

軽く調べてみた感じほとんどの記事がLegacy HTTP APIを使用されて書かれたものであり、HTTP v1 API では機能の追加、形式の変更、安全性の向上など、様々な面が改善されている

[移行ガイド](https://firebase.google.com/docs/cloud-messaging/migrate-v1?hl=ja)も用意されているのでおおまかに違いを把握したい場合は見ておくこと

ちなみに、[このブログ](https://firebase.blog/posts/2017/11/whats-new-with-fcm-customizing-messages)の投稿日時をみた感じHTTP v1 APIが発表されたのは2017年らしい？

## GCM Sender ID機能について(2023/02/22 追記)

久しぶりに動かしてみようとしたら、おそらくGCM Sender ID機能が2022年後半に削除されているような記述があった

- [https://bugs.chromium.org/p/chromium/issues/detail?id=979235](https://bugs.chromium.org/p/chromium/issues/detail?id=979235)

これによって、GCMを使ったような古いWebプッシュ通知の方式が廃止されたので気をつけるべし

## Legacy HTTP APIについて

※この方式では前述したGCMSenderIDの変更によりうまくいかないので注意

Legacy HTTP APIでは、`https://fcm.googleapis.com/fcm/send`がエンドポイントとして用意されている

プッシュ通知を送るための大まかな流れとして、以下のようになる

1.  FCMの登録トークンを取得する
    
2.  `https://fcm.googleapis.com/fcm/send`にプッシュ通知メッセージ内容と登録トークンをPOSTする
    - `Authorization: key=ここにFirebase Consoleにかかれているサーバーキー` をHTTPリクエストヘッダーに追加
    
3.  プッシュ通知が送られる
    

※ちなみに、Legacyよりさらに以前は[GoogleCloudMessaging](https://developers.google.com/cloud-messaging)というのが使用されていたが、2019年にサービス終了している

## Webプッシュ通知のメッセージ内容の暗号化について

[このドキュメント](https://firebase.google.com/docs/cloud-messaging/concept-options#notifications)などを見ると書いてあるが、Webプッシュ通知を送る際のペイロード（HTTPリクエストのbodyなど）にタイトルや本文を指定すればメッセージ内容をFCMに送ることができ、それをServiceWorker側に渡すことができる

より具体的には、以下の手順になる

1.  https://fcm.googleapis.com/fcm/send にプッシュ通知メッセージ内容と登録トークンをPOSTする
    
    1.  これでFCMからServiceWorkerに送られる
        
2.  ServiceWorkerが[Pushイベント](https://developer.mozilla.org/ja/docs/Web/API/PushEvent)を受け取る
    
    1.  PushEvent.dataにtitleやbodyがある
        

ここで、注意なのが暗号化せずにFCMにPOSTリクエストを送ってもPushイベントの.dataはnullになってしまうということ

では、どのように暗号化するのかというと、暗号化の手順は[https://web.dev/push-notifications-web-push-protocol/#the-payload-encryption](https://web.dev/push-notifications-web-push-protocol/#the-payload-encryption) にのっている

少し手順が長いのでこの記事の概要と暗号化の手順を以下にかいつまんで書く

まず、PushSubscriptionには[.getKey()](https://developer.mozilla.org/en-US/docs/Web/API/PushSubscription/getKey)というメソッドが存在し、.getKey(p256dh) もしくは .getKey(auth) とすると、それぞれP-256曲線状の楕円曲線暗号の公開鍵と認可秘密鍵が取得できる

また、PushSubscriptionのインスタンスを JSON.stringify で文字列にしてみるとそれぞれ keys という子要素として現れ、内容が読み取れる

そして、これらの鍵を使用してペイロードの暗号化を行う

基本的には、暗号化を行うライブラリがほとんどの言語に存在しているのでそれを使用すれば良いが、もしライブラリが存在しない場合は先ほどのドキュメントを読んで暗号化の手順を踏むしかない

暗号化だけでなく、リクエストヘッダにもソルトなどを含める必要があるため注意すること

※暗号化の手順や、通知の概要は [https://web.dev/notifications/](https://web.dev/notifications/) にのっているので必要になったら見ること

ここまで書いた

---

ここから下書き

### gcm_sender_idについて

どこを調べても gcm_sender_id に関する公式からのドキュメントがない

gcm_sender_idはmanifest.jsonに書かれ、FirebaseCloudMessagingを使用する場合は以下の固定値となっている

"gcm_sender_id": "103953800507"

-   [https://zenn.dev/kmifa/scraps/5c74ab0600984f](https://zenn.dev/kmifa/scraps/5c74ab0600984f)
    

### 登録トークンについて

登録トークンがブラウザのバックグラウンドで走るServiceWorkderごとに一意に発行されることで、送りたい端末を識別しています

ServiceWorkerは、APIとして大体のブラウザで用意されており、[https://developer.mozilla.org/ja/docs/Web/API/Service_Worker_API](https://developer.mozilla.org/ja/docs/Web/API/Service_Worker_API) あたりが参考になります

ServiceWorkerはJavaScript

登録トークンの取得については[https://firebase.google.com/docs/reference/js/v8/firebase.messaging.Messaging#gettoken](https://firebase.google.com/docs/reference/js/v8/firebase.messaging.Messaging#gettoken) あたりを参考にすると良いです

-   登録トークンの取得方法とそれに必要な情報
    
-   ServiceWorkerごとに登録トークンが発行されること
    

## HTTP v1 APIについて

-   Legacyどういう違いがあるのか
    

## 既存の仕様について

-   GCMを使った形跡があることと、そのコードの場所
    
-   endpointなどが[https://developer.mozilla.org/en-US/docs/Web/API/PushSubscription/endpoint](https://developer.mozilla.org/en-US/docs/Web/API/PushSubscription/endpoint) を使用していること
    
-   既存のDBに保存されているendpointのURL/{id}の形式はFCM側で対応しておらず、ライブラリ側でいい感じに処理してくれている可能性があること
    
-   ServiceWorkerごとにendpointが発行されること
    

# 参考

-   [https://web.dev/notifications/](https://web.dev/notifications/)
    
-   [https://firebase.blog/posts/2017/11/whats-new-with-fcm-customizing-messages](https://firebase.blog/posts/2017/11/whats-new-with-fcm-customizing-messages)
    
-   [https://qiita.com/nishi-sankosc/items/b9040ee57e6b7223ff21](https://qiita.com/nishi-sankosc/items/b9040ee57e6b7223ff21)
    
-   [https://docs.microsoft.com/ja-jp/xamarin/android/data-cloud/google-messaging/firebase-cloud-messaging](https://docs.microsoft.com/ja-jp/xamarin/android/data-cloud/google-messaging/firebase-cloud-messaging)
    
-   [https://developer.mozilla.org/en-US/docs/Web/API/PushSubscription](https://developer.mozilla.org/en-US/docs/Web/API/PushSubscription)
