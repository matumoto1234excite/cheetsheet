# sudoers で NOPASSWD が効かない



```bash
matumoto ALL=(ALL:ALL) NOPASSWD: /usr/sbin/service docker start
```



上記のように sudoers に設定しても反映されないのがあった



これの原因はまったくわかってないけど解決方法はわかった



- https://heartbeats.jp/hbblog/2010/01/sudonopasswd.html



これによると、設定を設定ファイルの末尾に置けばよいらしい



ほんとになぜだかわかんない

でも解決したのでよし