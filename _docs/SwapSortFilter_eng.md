---
title: Use sort.filter
category: ""
order: 0
---

## 1. Vulnerability Description
* Performing sorting after filtering을 is more advantageous than performing filtering after sorting.

## 2. Vulnerability Countermeasure
* Perform sorting after reducing the result set by filtering.

## 3. Sample Code
* Unsafe code 

```SCALA
class Test {
  List(1, 2, 3).sorted.filter(_ < 3)
}
```

* Safe Code 

```SCALA
class Test {
  val a = List(1, 2, 3).filter(_ < 3).sorted
}

```
