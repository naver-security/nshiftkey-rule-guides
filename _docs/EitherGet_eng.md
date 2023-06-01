---
title: Using get of Either projection
category: ""
order: 0
---

## 1. Vulnerability Description
* Either's Left, Right projection get can throw NoSuchElementException when the value doesn't exist. In particular, get has been deprecate from Scala 2.13.0.


## 2. Vulnerability Countermeasure
* Use getOrElse to handle when the value doesn't exist.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
  val l = Left("l")
  l.left.get
  val r = Right("r")
  r.right.get
}
```

