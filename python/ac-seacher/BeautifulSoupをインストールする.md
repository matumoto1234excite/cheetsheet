# `BeautifulSoup`をインストールする



#### え？`BeautifulSoup`をご存じない？

HTMLの抽出をしてくれるpythonライブラリです

同じpythonライブラリのSeleniumよりも早い（というかSeleniumだとHTMLの抽出動作が遅い）



#### インストール

```bash
$ sudo apt-get install python-bs4
```

でもできるらしいが、[この記事](https://pcl.solima.net/pyblog/archives/163)によると`pip`を使う方がよさそう

じゃあ、`pip`でやりますか

```bash
$ pip --version
```

をしたらちゃんと動いたのでさっそくインストールしてみる

```bash
$ pip install beautifulsoup4
```

インストールDONE！



念のため...

```bash
$ python3
>>> a = 10
>>> b = 5
>>> print(a*b)
50
>>> import bs4
>>> exit()
```

ちゃんと動いたのでよさそう

