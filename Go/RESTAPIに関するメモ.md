# RESTAPIに関するメモ

GoのimportはGOPATH/src/以下を参照するからGOPATH/src/にimportするfmtとかを置かなきゃならない

と思いきや、go1.12らへんからGOPATH/srcが廃止となり、Go Modulesが出てきた

`go mod init projectname`
をするとgo.modファイルができて、あとはgo getをして追加なりしていく感じっぽい？

go.modができたことで、バージョンをディレクトリごとに分けられるのがメリットらしい

go buildで依存関係をインストールできるらしい

Go Modulesが使えるのかどうかはgo envをして確認する
go env -w GO111MODULE=on
で使うようにできる

github.com/ant0ine/go-json-restをimportしてREADMEのHelloWorldプログラムをコピペしてgo runしたら動いた！ありがとう！

RESTAPI完全に理解した（HelloWorldできた）

そもそも僕がやろうとしているのはRESTAPIではないという話がある
あと、Goに関するQiita記事が多すぎてありがたい

