# awaitとasync



async関数の中でないとawaitはつけられない



ちなみに、あしんく警察が在中しています

正しくはasync=えいしんく

awaitはあうぇいと



## awaitとasyncのイメージ

プログラムを実行中にAPIとかをたたいたら返ってくるまで待たないといけないけど、そこで待たずにほかの処理をするためにawaitを使う



```js
await axios.get('https://hoge.com') // ここはasyncが付けられた関数の中
```

みたいに(axiosは事前に`axios = require('axios')`しています)



こうすることでaxios.getの実行結果を待たずにほかの処理を続けることができる

じゃあ、帰ってきた結果どうすん念



axiosでthen使う必要はなくて、これ↓みたいに使えるっぽい

https://qiita.com/shisama/items/61cdcc09dc69fd8d3127



```js
const res = await axios.get('https://hoge.com');
// resは以下が使えて、この文自体try,catchで囲う
// res.data
// res.status
// res.statusText
// res.headers
// res.config
```



帰ってきた結果はtry,catchの中で使う

今回使ったthen文だとthenの中でだけ使う

```js
await axios.get(requestURL)
.then(response => {
    // 返信するメッセージを作成
    message = {
      type: 'text',
      text: '',
    };

    for(const element of response.data.message.values()){
      message.text += '【' + element.title + '】\n';
      message.text += '開始:' + element.startTime + '\n';
      message.text += '終了:' + element.endTime + '\n';
    }
})
.catch(error => {
    console.log(error.response);
});
```



try,catchで書くとこんなんになる

```js
try {
    const res = await axios.get('https://hoge.com');
    message = {
        type: 'text',
        text: '',
    };
    
    for(const element of res.data.message.values()){
      message.text += '【' + element.title + '】\n';
      message.text += '開始:' + element.startTime + '\n';
      message.text += '終了:' + element.endTime + '\n';
    }
} catch(error) {
    console.log(error.response);
}
```





公式ドキュメント↓

https://github.com/axios/axios



