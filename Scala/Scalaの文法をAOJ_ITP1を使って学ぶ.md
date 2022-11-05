# Scalaの文法をAOJ_ITP1を使って学ぶ

タイトル通りのことをする

環境構築はまた別

`sbt console` した状態を想定しており...



この中で登場するプログラム類はある人の指導とチェックを受けながら書いたものなので、matumoto本人が全て一から書いたわけではない



あと全部を埋めたわけではなく、かいつまんで解いていった形になっているので注意



### ITP1_1_A

```scala
// object Main extends App {
//   println("Hello World")
// }

object Main {
  def main(argv: Array[String]): Unit = {
    println("Hello World")
  }
}
```

二通りの方法があるねえ

`App`を継承するとその中に書いてある文が実行されるようになるらしい

下の書き方の方が関数を別で書いたりするときに便利なので下の方で書く



### ITP1_1_B

```scala
import scala.io.StdIn.readInt

object Main {
  def main(argv: Array[String]): Unit = {
    val x = readInt()
    println(x * x * x)
  }
}
```

標準入力は`scala.io.StdIn`以下にあるらしい

変数宣言については`var`と`val`があって、`var`が変数、`val`が定数になる



### ITP1_1_C

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    val ab = readLine().split(" ").map(str => str.toInt)
    val a = ab(0)
    val b = ab(1)

    println(s"${a * b} ${2 * (a + b)}")
  }
}
```

scalaの`readInt()`は改行を無視してくれないので、1行受け取ってそれを空白で区切って整数に変換という処理が必要になる

また、配列のインデックスを指定するときは`()`演算子を使う



文字列に変数を埋め込む、加工文字列リテラルを使うことができる（JavaScriptのテンプレート文字列みたいなやつ）

`s"${1 + 2} = 3"`

ダブルクォーテーションの先頭に`s`をつけるとそれになる



あと、同パッケージから複数importするときは`{}`で囲むと簡略化できる

```scala
import scala.io.StdIn.readInt
import scala.io.StdIn.readLine

// 上だと長いので
import scala.io.StdIn.{readInt, readLine}
```



### ITP1_2_A

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def compare(a: Int, b: Int): String = {
    if (a < b) "<"
    else if (a > b) ">"
    else "=="
  }

  def main(argv: Array[String]): Unit = {
    val Array(a, b) = readLine().split(" ").map(_.toInt)
    println(s"a ${compare(a, b)} b")
  }
}

```

関数を宣言するには`def`

そもそも、`{}`が無名関数の役割を担うのでそれを代入している

あと、main関数の返り値に`Unit`という型があるが、C++の`void`とは違って、値を返すがその値は使われることはない

じゃあ何も返さなくていいじゃん、と感じたら[ここ](https://qiita.com/alucky0707/items/a677e5c9850aa765dd55)を見よう



### ITP1_2_C

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    println(readLine().split(" ").map(_.toInt).sorted.mkString(" "))
  }
}
```

1行きもちえー

`mkString`で配列から文字列を生成できる



### ITP1_3_A

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    for (_ <- 1 to 1000) {
      println("Hello World")
    }
  }
}
```

for式を使うだけ



### ITP1_3_B

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    var i = 1
    var x = 1
    while (x != 0) {
      x = readInt()
      if (x != 0) {
        println(s"Case ${i}: ${x}")
      }
      i += 1
    }
  }
}
```

手続きっぽく書いたやつ



```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    Iterator
      .continually(readInt())
      .takeWhile(_ != 0)
      .toList
      .zipWithIndex
      .map { case (n, idx) => (n, idx + 1) }
      .foreach { case (n, idx) => println(s"Case ${idx}: ${n}") }
  }
}
```

関数っぽく書いたやつ

関数のように書くと、処理手順がとてもわかりやすくていいと思った



### ITP1_3_C

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    Iterator
      .continually(readLine()
        .split(" ")
        .map(_.toInt)
        .sorted
        .mkString(" "))
      .takeWhile(_ != "0 0")
      .foreach(println)
  }
}
```

たのしくなってきた

`_`がとても便利



### ITP1_3_D

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    val Array(a, b, c) = readLine().split(" ").map(_.toInt)
    println((a to b).count(c % _ == 0))
  }
}
```

なんと分割代入ができてしまう





### ITP1_4_C

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    Iterator
      .continually(readLine())
      .map(_.split(" "))
      .takeWhile {
        case Array(_, "?", _) => false
        case _                => true
      }
      .map {
        case Array(a, "+", b) => a.toInt + b.toInt
        case Array(a, "-", b) => a.toInt - b.toInt
        case Array(a, "*", b) => a.toInt * b.toInt
        case Array(a, "/", b) => a.toInt / b.toInt
        case _                => -1
      }
      .foreach(println)
  }
}
```

パターンマッチ、すごい



パターンマッチ部分はある程度省略したものを使っている

```scala
.takeWhile(
  match {
    case Hoge => HogeResult
    case _    => HogeHogeResult
  }
)

// ↑を省略すると
.takeWhile {
  case Hoge => HogeResult
  case _    => HogeHogeResult
}
```



### ITP1_4_D

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    readLine()
    val a = readLine().split(" ").map(_.toLong)
    println(s"${a.min} ${a.max} ${a.sum}")
  }
}
```

最小値、最大値、和が簡単に求められてかなりうれしい

`n`は使わないので`readLine()`で読み飛ばしている



### ITP1_6_A

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    readLine()
    println(readLine().split(" ").map(_.toLong).reverse.mkString(" "))
  }
}
```

反転させるだけ



### ITP1_6_B

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    val n = readInt()
    val set = (for (_ <- 1 to n) yield readLine()).toSet
    (for {
      mark <- "SHCD"
      num <- 1 to 13
    } yield s"${mark} ${num}")
    .filterNot(set.contains(_))
    .foreach(println)
  }
}
```

`yield`を使うとうれしくなれる

右辺値を左辺値にしてそう...?（詳しくは知らない）



### ITP1_7_C

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def readMap[T](f: String => T): List[T] = readLine().split(" ").toList.map(f)

  def main(argv: Array[String]): Unit = {
    val List(h, w) = readMap(_.toInt)

    var table = for (i <- 1 to h) yield {
      val row = readMap(_.toInt)
      row ++ List(row.sum)
    }

    (table :+
      (
        table.reduce(
         (_, _)
          .zipped
          .map {
            case (a, b) => a + b
          }
        )
      )
    )
    .map(_.mkString(" "))
    .foreach(println)
  }
}
```

`readMap`を作って使ってみたやつ

`:+`でpush操作ができるっぽい

行の畳み込みを行うことで、総和がかなり簡単に計算できてしまう



### ITP1_8_B

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    Iterator
      .continually(readLine())
      .takeWhile(_ != "0")
      .map(
        _.split("")
        .map(_.toInt)
        .sum)
      .foreach(println)
  }
}
```

総和を計算するだけ



### ITP1_8_C

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    val table = (Iterator
      .continually(readLine())
      .takeWhile(_ != null)
      .flatMap(a => a)
      .toList
      .map(_.toLower)
      .groupBy(ch => ch)
      .map { case (ch, set) => (ch, set.length) })

    (for (ch <- 'a' to 'z') yield {
      s"${ch} : ${table.getOrElse(ch, 0)}"
    })
      .foreach(println)
  }
}
```

`getOrElse`で辞書の中になかった場合の値を指定できる

これほかの言語でもあったら重宝しそう（`std::map`とか）



### ITP1_9_A

```scala
import scala.io.StdIn.{readInt, readLine}

object Main {
  def main(argv: Array[String]): Unit = {
    val w = readLine()

    val ans = (Iterator
      .continually(readLine())
      .takeWhile(_ != "END_OF_TEXT")
      .map(_.toLowerCase())
      .map(_.split(" "))
      .map(_.count(_ == w))
      .sum)

    println(ans)
  }
}
```

とても、いいと思った





## あとがき

うーん、たのしい