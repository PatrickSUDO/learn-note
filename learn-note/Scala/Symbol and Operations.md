---
tags: 
  - scala
---



## :: and :::

:: \- adds an element at the beginning of a list and returns a list with the added element (append)
::: \- concatenates two lists and returns the concatenated list (extend)

## \[+A <:B\]

Q\[A <: B\] means that class Q can take any class A that is a subclass of B.

Q[B >: A] is a lower type bound. It means that B is constrained to be a supertype of A.

Q\[+B\] means that Q can take any class, but if A is a subclass of B, then Q\[A\] is considered to be a subclass of Q\[B\].

Q\[+A <: B\] means that class Q can only take subclasses of B as well as propagating the subclass relationship.

The first is useful when you want to do something generic, but you need to rely upon a certain set of methods in B. For example, if you have an Output class with a toFile method, you could use that method in any class that could be passed into Q.

The second is useful when you want to make collections that behave the same way as the original classes. If you take B and you make a subclass A, then you can pass A in anywhere where B is expected. But if you take a collection of B, Q\[B\], is it true that you can always pass in Q\[A\] instead? In general, no; there are cases when this would be the wrong thing to do. But you can say that this is the right thing to do by using +B (covariance; Q covaries--follows along with--B's subclasses' inheritance relationship).

## =\> and ->

-\> it used to associate key with a value by using implicit conversion for example tuple, map etc.

```bash
scala> 1 -> 2
res0: (Int, Int) = (1,2)
```

scala> val map = Map("x" -> 12, "y" -> 212)
Its basically just take the item on the left and map it to the item on the right

It converts any type into an instance of "ArrowAssoc" using implicit conversion

```scala
implicit def any2ArrowAssoc[A](x: A): ArrowAssoc[A] = new ArrowAssoc(x)
class ArrowAssoc[A](x: A) {
    def -> [B](y: B): Tuple2[A, B] = Tuple2(x, y)
}
```

=\> is a syntax provided by the language itself to create instance of function using call-by-name. It passes value name inside the method for example:

```scala
`def f(x:Int => String) {}` function take argument of type Int and return String
```

You can also pass no argument like below

() =\> T means it doesn't take any argument but return type T.