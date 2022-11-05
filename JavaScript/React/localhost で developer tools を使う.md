# localhost で developer tools を使う



create-react-app で localhost を起動して、chrome の developer tools を開いたままリロードとかすると接続エラーになるものの解決策



原因は知らないが、Network タブの プルダウンメニューのところを No throttling にするだけ

![image-20220221080352149](C:\Users\matum\AppData\Roaming\Typora\typora-user-images\image-20220221080352149.png)

元々は Offline になっていたけど、なぜダメなのかよくわかっていない