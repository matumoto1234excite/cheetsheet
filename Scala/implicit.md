# implicit

はい

https://qiita.com/miyatin0212/items/f70cf68e89e4367fcf2e



以下、IndexedSeq[T]型に対する tapEach の実装

```scala
object Main{
  implicit class tapEachable[T](vs: IndexedSeq[T]) {
    def tapEach[U](f: (T) => U): IndexedSeq[T] = {
      vs.foreach(f)
      vs
    }
  }
  
  def main(argv: Array[String]): Unit = {
    Iterator
      .con
  }
}
```

