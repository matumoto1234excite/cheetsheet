# trash-cliについて



trash-cliはhttps://qiita.com/SUZUKI_Masaya/items/3148b5f1d9fa9fdb3b51で見つけた便利なやつ



trash-putでゴミ箱におけるので以下のエイリアスでrmをtrash-putにしている

>1. `~/.bashrc`の末尾に以下を追記します。
>
>   ```
>   if type trash-put &> /dev/null
>   then
>       alias rm=trash-put
>   fi
>   ```
>
>2. `source ~/.bashrc`コマンドを実行し、`.bashrc`への変更を反映します。
>
>※Qiitaの記事より





## trash-cliの使い方

### ゴミ箱にあるファイルの一覧表示

```
$ trash-list
```

### ゴミ箱にあるファイルを元に戻す

```
$ trash-restore
```

### ゴミ箱を空にする

```
$ trash-empty
```

### ゴミ箱の中のファイルを完全に削除する

```
$ trash-rm {ファイル名}
```





こいつら長いのでエイリアスを作った

上から

tls

trestore

tempty

trm