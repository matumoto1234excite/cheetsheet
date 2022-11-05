# python の文字コード関係



`codecs`を使おう！



```python
import codecs
with codecs.open('./config.yml', encoding='utf-8') as file:
  file.write('hoge')
```



`write`があやしい動作しているなと思った`print`を使おう！

```python
import codecs
with codecs.open('./config.yml', encoding='utf-8') as file:
  print('hoge', file=file)
```



`json.dumps` したものを出力するときはアスキーを使わないようにしよう！

```python
aaa = {
  hoge: 'piyo'
}

print(json.dumps(aaa, ensureAscii=False))

import coedecs
with codecs.open('./config.yml', encoding='utf-8') as file:
  json.dump(aaa, ensureAscii=False, indent=2, file=file)
```



