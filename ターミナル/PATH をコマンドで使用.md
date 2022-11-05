# PATH をコマンドで使用



これは `$PATH` 以下のディレクトリから `node` を `find`している

```bash
$ echo $PATH | sed "s/:/ /g" | xargs echo | find -name node
```

