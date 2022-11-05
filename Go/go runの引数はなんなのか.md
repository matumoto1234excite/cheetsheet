# go runの引数はなんなのか



https://blog.hirokuma.work/2020/02/golanggo-run.html



> \> Typically the package is specified as a list of .go source files from a single directory, but it may also be an import path, file system path, or pattern matching a single known package, as in 'go run .' or 'go run my/cmd'.
>
> 複数のgoファイルを含んだ単一のディレクトリ(importパス、systemパス)、パターンに一致する単一のパッケージなどが典型的だと。



通常、パッケージは単一のディレクトリにある .go ソースファイルのリストとして指定されますが、インポートパス、ファイルシステムパス、または 'go run .' や 'go run my/cmd' のように単一の既知のパッケージに一致するパターンとして指定することもできます。



相対パスは推奨されていないっぽい？



まあ基本的にmainパッケージとかが含まれている一番上のディレクトリを指定するのが無難そう