# cors



クロスオリジンリソースシェアリング



## pathは変えるな！！



corsする際はaxiosでGET,POST,などを間違えなければあとは全部バックエンドがやってくれる

あと、fetchで`{mode:"no-cors"}`をつけるのはちゃんとした返答が返されない噓解法なので気を付けましょう



nuxtでやるならたぶんnuxt.config.jsにproxyとかやる必要がありそう



呼び出す側はこんなんでいけます

```js
    this.$axios.post("https://ic0tkzuy55.execute-api.ap-northeast-1.amazonaws.com/tk/test")
      .then((res) => {
        console.log("cors succeeded!");
        console.log(res);
      })
      .catch((err) => {
        console.log("cors error!");
        console.log(err);
      });
```



corsライブラリです

```js
const response = {
        statusCode: 200,
        headers: {
            "Access-Control-Allow-Origin" : "*" // Required for CORS support to work
        },
        body: JSON.stringify({ "message": "Hello World!" })
    };

    return response;
```



serverless.yml

```yaml
       - http:
          path: hhh
          method: post
          cors:
            origin: '*'
            headers:
              - Content-Type
              - X-Amz-Date
              - Authorization
              - X-Api-Key
              - X-Amz-Security-Token
              - X-Amz-User-Agent
            allowCredentials: false
```

