# push ができないとき



https から ssh に変える



ssh-keygen とか .ssh/config とかする必要がある



github ssh でぐぐろう



- https://qiita.com/shizuma/items/2b2f873a0034839e47ce

とかを見るとよさそう



tashioさんが打ってたコマンド一覧

```bash
$ ssh-keygen -t ecdsa -b 521 -f ~/.ssh/github-wataruhigasi
$ cd ~/.ssh
$ ls
github-wataruhigasi github-wataruhigasi.pub known_hosts
$ cat github-wataruhigasi
--BEGIN OPENSSH PRIVATE KEY--
省略
--END OPENSSH PRIVATE KEY--
$ cat github-wataruhigasi.pub
ecdsa-sha2-nistp521
ここに公開鍵の中身

# ここで github-wataruhigasi.pub の中身をコピーして、github の自分のページ->settings->SSH and GPG keys->New SSH key で、新しい SSH key を作成する（名前はなんでもよい）

$ nano config
# これを .ssh/config に書き込む
Host github.com
    IdentityFile ~/.ssh/github-wataruhigasi
    User git
$ git remote -v
origin https://github.com/wataruhigasi/scoreboard.git (fetch)
origin https://github.com/wataruhigasi/scoreboard.git (push)
$ git remote set-url origin git@github.com:wataruhigasi/scoreboard.git
$ git push origin master
できた！！！！
```

