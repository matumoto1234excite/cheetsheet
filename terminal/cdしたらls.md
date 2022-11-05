

# cdしたらlsをする

これでQOL爆上がりです



```shell
# これは.bashrc
cdpwdls () {
    \cd "$@" && pwd && ls
}
alias cd="cdpwdls"
```

これまじでいい



設定しおえたら`source`で適応して試してみるとよさそう

```bash
$ source ~/.bashrc
$ cd どこか好きな場所
```

