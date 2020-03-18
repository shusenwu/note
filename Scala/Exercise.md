Functional Programming in Scala
==
## Tail resursive function:  
A call is said to be in tail position if the caller does nothing other than return the value
of the recursive call. For example, the recursive call to go(n-1,n*acc) we discussed
earlier is in tail position, since the method returns the value of this recursive call directly
and does nothing else with it. On the other hand, if we said 1 + go(n-1,n*acc), go
would no longer be in tail position, since the method would still have work to do when
go returned its result (namely, adding 1 to it).
## Exercise 2.1
Write a recusive function to get the nth Fibonacci number (http://mng.bz/C29s).
The first two Fibonacci numbers are 0 and 1. The nth number is always the sum of the
previous two—the sequence begins 0, 1, 1, 2, 3, 5. Your definition should use a
local tail-recursive function.
```Scala
object Exercise {
  def main(args: Array[String]): Unit = {
    val re = fib(5)
    println(re)
    val re2 = fib2(5)
    println(re2)
    val re3 = fib3(5)
    println(re3)
  }

  //Recursion only works well if n is small, otherwise you get a stack overflow exception.
  def fib(n: Int): Int = {
    if (n == 0) 0
    else if (n == 1) 1
    else fib(n-2) + fib(n-1)
  }

  def fib2(n: Int): Int = n match {
    case 0 | 1 => n
    case _ => fib2(n-2) + fib(n-1)
  }
// tail recursion 
  def fib3(n:Int): Int = {
    if (n == 0) 0
    // bottom up
    def fib_up(n:Int, cur: Int, pre: Int): Int = n match {
      case 0 => cur
      case _ => fib_up(n-1, cur+pre, cur)
    }

    fib_up(n-1, 1, 0)
  }

}

```



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

EXERCISE 2.2
==
Implement isSorted, which checks whether an Array[A] is sorted according to a
given comparison function:
```scala
object Exercise3 {
  def main(args: Array[String]): Unit = {
    val ordered = (a: Int, b: Int) => a > b
    val arr = Array(1, 5, 6, 7)
    val arr2 = Array(5, 4, 2)

    println(isSorted(arr, ordered))
    println(isSorted(arr2, ordered))
  }

  def isSorted[A](as: Array[A], ordered: (A,A) => Boolean): Boolean = {
    var i = 1
    while (i < as.length){
      if(ordered(as(i), as(i-1))) i = as.length + 1
      else i += 1
    }
    if (i == as.length) true else false
  }
}
```
