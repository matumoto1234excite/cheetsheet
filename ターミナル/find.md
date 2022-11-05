# find



よく `-name` と検索対象の順番まちがえがち



```bash
$ find 検索対象 -name *.cpp
# -name は実は省略可能
$ find 検索対象 *.cpp 

# 複数の条件は -or
$ find 検索対象 -name *.cpp -or -name *.hpp

# -and もある
$ find 検索対象 -name *.cpp -and -name hoge*
```



ファイル限定とかディレクトリ限定とかもあるらしい



find の結果を空白区切りでやりたい

findコマンドの`-print0`とxargsコマンドの`-0`オプションを使えばOK

例

```bash
$ find ./ \( -type d -and -name tests -and -prune \) -or \( -type f -and -name *.cpp -and -print0 \) | xargs -0 g++-11 -c -std=c++20 -I/home/matumoto/src/iutest-master/include
```



上のコマンドは tests ディレクトリ以下を（testsディレクトリ含めて）除外して、拡張子が`.cpp`のものを空白区切りで g++ に渡しているもの





