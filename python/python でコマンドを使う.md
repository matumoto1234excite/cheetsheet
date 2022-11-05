# python でコマンドを使う



`subprocess.run`を使おう！



```python
import subprocess
from subprocess import PIPE

args = ['oj-bundle', '/home/matumoto/code_box/library/tools/debug.hpp']
res= subprocess.run(args, stdout=PIPE, stderr=PIPE, text=True)

if res.stdout:
    decoded = res.stdout
    # print(decoded)
    lines = decoded.splitlines()
    for line in lines:
        if '#line' in line:
            continue
        print(line)
```



`subprocess.check_output` とかがあるけど、それは3.5（3.6だったかも？）より前のバージョンでの機能で新しいものでは`subprocess.run`が推奨されている



というか、`subprocess.run`が完全上位互換なので、前のものを使う必要がないんだよな



上の例の5行目の部分はこうとも書ける

```python
res= subprocess.run('oj-bundle /home/matumoto/code_box/library/tools/debug.hpp', shell=True, stdout=PIPE, stderr=PIPE, text=True)
```



shell引数をTrueにすると、そのまま実行してくれるっぽい