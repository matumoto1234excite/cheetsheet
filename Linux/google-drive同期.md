# google-drive の同期を行う


## 人気のある?LinuxでのGoogleDriveの同期方法


- google-drive-ocamlfuse

「google drive arch linux」とかで調べるとこれが出てくる  
日本語の記事だとだいたいこれな気がする

ただし、ArchLinuxではAURのものとかを入れようとするとビルドで失敗するので、やめた

`opam install` などを試してみても謎のエラーが出るので別のものを使うようにする

そもそも、cloudcrossがいけないんだよなぁ...


## 使うツール

- grive

というものを使用する

ちょうど日本語の記事がいくつかあるのでそれを参考にする

- https://blog.katio.net/page/63175ef5cd9f33e16b87

自動同期もあって（5分ごとに同期する）、その機能を使ってみたいがAURにはないらしいので断念

GitHubにあがっているソースコードのうちの.service.inの拡張子のものを `/etc/systemd/system/` に入れたのち、  
`systemctl enable grive-timer@google-drive.timer` などを行ってみたが timer に関してエラーが出てしまう

そのうち解決したい

