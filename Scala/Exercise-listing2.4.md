
```scala
object Exercise2 {
  def main(args: Array[String]): Unit = {
      val arr = Array(1, 2, 4)
      println(findFirst(arr, (a: Int)=> a==4))
  }

  // Find the first value
  def findFirst[A](as: Array[A], p: A => Boolean): Int = {
    def loop(n: Int): Int =
      if (n >= as.length) -1
      else if (p(as(n))) n
      else loop(n + 1)

    loop(0)
  }
}

```
