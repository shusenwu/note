

```scala
trait IterableOnceOps[+A, +CC[_], +C] extends Any { this: IterableOnce[A] =>
  def reduce[B >: A](op: (B, B) => B): B = reduceLeft(op)

  def reduceLeft[B >: A](op: (B, A) => B): B = {
    val it = iterator
    if (it.isEmpty)
      throw new UnsupportedOperationException("empty.reduceLeft")

    var first = true
    var acc: B = 0.asInstanceOf[B]

    while (it.hasNext) {
      val x = it.next()
      if (first) {
        acc = x
        first = false
      }
      else acc = op(acc, x)
    }
    acc
   }
  }
  ```
  
  `B` is the type of AnyRef, but Why? 
  Why we need to init acc like this way? 
   ![Scala Type](https://media.geeksforgeeks.org/wp-content/uploads/20190401170602/ScalaTypeHierarchy.png)
