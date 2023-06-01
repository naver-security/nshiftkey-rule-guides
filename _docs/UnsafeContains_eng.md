---
title: Unsafe contains
category: ""
order: 0
---

## 1. Vulnerability Description
* Comparing unrelated variables using Contain can cause unintended behavior.


## 2. Vulnerability Countermeasure
* When using Contain, make sure that it is compatible with each other.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
    def f2[A <: AnyRef](xs: Seq[A], y: Int)                            = xs contains y
    def f5[CC[X] <: Seq[X], A <: AnyRef, B <: AnyVal](xs: CC[A], y: B) = xs contains y 
}
```

* Safe Code

```SCALA
class Test {
    def f1[A](xs: Seq[A], y: A)                                        = xs contains y
    def f4[CC[X] <: Seq[X], A](xs: CC[A], y: A)                        = xs contains y
}
```
