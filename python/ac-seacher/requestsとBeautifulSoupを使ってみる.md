# `requests`と`BeautifulSoup`を使ってみる



#### え？`requests`をご存じない？

URLを指定すればGETとかができます

便利ですね



#### `reqests`のインストール

```bash
$ pip install requests
```

これを打ったらすでにインストールされてたっぽい

いつインストールしたんだ...?



念のため...

```bash
$ python3
>>> import requests
>>> r = requests.get('https://www.yahoo.co.jp/')
>>> exit()
```

ちゃんと動いたっぽい



実験的にやってみる

```python
import requests
from bs4 import BeautifulSoup

r = requests.get("https://atcoder.jp/contests/abc201/submissions/22699598")

submitted_code = BeautifulSoup(r.content, "html.parser")

print(submitted_code.find("pre"))
```

こんな10行もいかないコードで提出したコードが取ってこれちゃったねぇ

python、ありがとう...