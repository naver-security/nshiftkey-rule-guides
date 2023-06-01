---
title: Using the var in the Closure
category: ""
order: 0
---

## 1. Vulnerability Description
* In case of capturing var in the Closure, the value may fluctuate according to the change of var, resulting in unintended results.

## 2. Vulnerability Countermeasure
* Check whether the use of var in the closure definition is done correctly, and it is recommended to use val to become a pure function.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   var a = 1
   val b = List(1,2,3)
   val c = b.filter(_ < a)
}
```

* Safe Code
  * Use mkString

```SCALA
class Test {
   val a = 1
   val b = List(1,2,3)
   val c = b.filter(_ < a)
}

```
