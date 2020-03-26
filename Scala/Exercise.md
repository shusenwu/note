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

## Somewhere on the book
 

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

## EXERCISE 2.2
 
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
When we define a function literal, what is actually being defined in Scala is an object
with a method called apply. Scala has a special rule for this method name, so that
objects that have an apply method can be called as if they were themselves methods.
When we define a function literal like (a, b) => a < b, this is really syntactic
sugar for object creation:
val lessThan = new Function2[Int, Int, Boolean] {
def apply(a: Int, b: Int) = a < b
}

## Return type B => C 
return a function input type B return Type C,  like convert B to C

```scala
  object Exercise2 {
  def main(args: Array[String]): Unit = {
    val f = (a: Int, b: String) => 'c'
    val re = partial1[Int, String, Char](1, f)
    print(re("ab"))
  }

    def partial1[A,B,C](a: A, f: (A,B) => C): B => C =
      b => f(a, b)
}
```

## Exercise 2.3
Let’s look at another example, currying,9 which converts a function f of two arguments
into a function of one argument that partially applies f. Here again there’s only one
implementation that compiles. Write this implementation.
def curry[A,B,C](f: (A, B) => C): A => (B => C)

```scala
  object Exercise2 {
  def main(args: Array[String]): Unit = {
    val f = (a: Int, b: String) => a+b
    val re = curry[Int, String, String](f)(123)("abc")
    println(re)
  }

    def curry[A,B,C](f: (A, B) => C): A => (B => C) = {
       a => b => f(a, b)
    }
}
```
令人发指。。

```
functional programs don’t update variables or modify mutable data structures. 
Remember, a pure function must not change data in place or perform other
side effects. Therefore, functional data structures are by definition immutable. 
Doesn’t this mean we end up doing a lot of extra copying of the data? Perhaps
surprisingly, the answer is no```
```

```SCALA
// : _* is a special instance of type ascription which tells the compiler to treat a single argument of a sequence type as a variable argument sequence, i.e. varargs.
def apply[A](as: A*): List[A] =
if (as.isEmpty) Nil
else Cons(as.head, apply(as.tail: _*))
```

