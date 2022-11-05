# git hooks



- [参考記事](https://qiita.com/noraworld/items/c562de68a627ae792c6c)



git で行うコマンドのときに、もし設定していればスクリプトを動かすことができる



具体的には、`.git/hooks/pre-commit`みたいなファイルがあればそのファイルが適宜実行される



- [一覧っぽいやつ](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/githooks.html)
- [実装例](https://qiita.com/tbpgr/items/222030af9cc266f9781e)



## チーム開発での使い方



`.git` のローカルでの変更になるので、`.git/hooks/xxx`をそのまま追加するのはよろしくなさそう

というかそもそも push できない



># 自作のスクリプトを読み込む設定を追加
>
>Git フックの仕組みがわかったところで自作のフックスクリプトを読み込む設定を追加してみましょう。ホームディレクトリに `.git_template` というディレクトリを作成し、その中に `hooks` ディレクトリを作成します。
>
>```
>$ mkdir -p ~/.git_template/hooks
>```
>
>`.git_template` ディレクトリに Git のテンプレートが入っていることを Git で認識できるように設定を追加します。
>
>```
>$ git config --global init.templatedir '~/.git_template'
>```

（上の参考記事より）



~~読み込む方法があるっぽいので、おそらく`.git_template`を作ったほうがいいんだろうな~~

[Git のテンプレートディレクトリ機能](https://git-scm.com/docs/git-init#_template_directory)を使っても、既存のディレクトリに対して適応させることはできない（clone や init のときのみ）

既存のディレクトリに適応させるにはいい感じに Makefile やシェルスクリプトなどを作って`.git/hooks/`に置くしかないのでは？（`cp`コマンド手打ちでもいいけど）



↑なんて思っていた時期が私にもありました

- [神記事](https://astatsuya.medium.com/githooks%E3%81%AEpre-push%E3%82%92%E5%85%B1%E6%9C%89%E3%81%97%E3%81%A6%E3%83%AC%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%82%92%E5%81%A5%E5%85%A8%E3%81%AB%E4%BF%9D%E3%81%A4-7156def39b64)
- [神記事2](https://www.farend.co.jp/blog/2020/04/git-hook/)



これによると、`core.hooksPath`を変更するとよいらしい

```bash
$ git config --local core.hooksPath xxx
```

のようにすると xxx がフック用ディレクトリとして登録される
これで、`.git_hooks`みたいなディレクトリにまとめて管理できるようになる



個人の hooks を設定したいのであれば2 番目の記事に乗ってるように、`core.hooksPath`をいじらずに`.git/hooks/`にコピーする必要がある



pre-commit の例

```python
#!/usr/bin/python3
import sys
import re
import subprocess

# stdin: <local_ref> <local_sha1> <remote_ref> <remote_sha1>
# sample:
#   local_ref   = refs/heads/master
#   local_sha1  = 68a07ee4f6af8271dc40caae6cc23f283122ed11
#   remote_ref  = refs/heads/master
#   remote_sha1 = efd4d512f34b11e3cf5c12433bbedd4b1532716f
local_ref, local_sha1, remote_ref, remote_sha1 = input().split()

pushing_branch = remote_ref.replace('refs/heads/', '')

patterns = ['main']

is_matched = False

for pattern in patterns:
  if re.match(pattern, pushing_branch) != None:
    is_matched = True

if is_matched:
  prefix = 'warning: '
  print(prefix + 'Push to remote ' + pushing_branch + ', continue? [y/N]', end=' ', flush=True)

  res = subprocess.run('exec < /dev/tty; read ANSWER; echo $ANSWER', shell=True, capture_output=True, text=True)
  answer = res.stdout

  if answer == '\n' or answer[0] == 'n' or answer[0] == 'N':
    print('Push cancelled.')
    exit(1)
  else:
    print('OK. Push start.')
```



pre-commit の例

```python
#!/usr/bin/python3
import subprocess

def verify_commit_branch():
  result = subprocess.run('git rev-parse --abbrev-ref HEAD', shell=True, capture_output=True, text=True)

  branch = result.stdout

  if branch == 'main\n':
    prefix = 'fatal: '
    print(prefix + 'Please do not commit to the main branch.')
    exit(1)


def verify_linter():
  subprocess.run('npm run eslint', shell=True)
  subprocess.run('npm run stylelint', shell=True)


verify_commit_branch()
verify_linter()
```



commit-msg の例

```python
#!/usr/bin/python3
import sys
import re
import codecs

path = sys.argv[1]

with codecs.open(path, mode='r', encoding='utf-8') as f:
  commit_message = f.read()
  
  if re.match(r'#[0-9]+:', commit_message) == None:
    prefix = 'fatal: '
    spaces = ' ' * len(prefix)
    print(prefix + 'No issue number at the beginning of the commit message.')
    print(spaces + 'The accepted format is as follows:')
    print(spaces + spaces + '#[0-9]+:')
    print()
    print(spaces + 'The valid example: git commit -m \'#10:Update README.md\'')
    exit(1)
```

