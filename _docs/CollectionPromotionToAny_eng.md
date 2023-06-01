---
title: Wrong list append
category: ""
order: 0
---

## 1. Vulnerability Description
* When you want to join the list using the :+ (append) operator, the entire list behind is added as one element.


## 2. Vulnerability Countermeasure
* Check if the action is intended and use "++" to join the list.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   val a = List(1, 2, 3) 
   val b = List(4, 5, 6)
   val c = a :+ b
   c: List[Any] = List(1, 2, 3, List(4, 5, 6))
}
```

* Safe Code

```SCALA
class Test {
   val a = List(1, 2, 3) 
   val b = List(4, 5, 6)
   val c = a ++ b
   c: List[Int] = List(1, 2, 3, 4, 5, 6)
}

```
