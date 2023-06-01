---
title: check emptiness by size, length
category: ""
order: 0
---

## 1. Vulnerability Description
* When you check if the data structure is empty, the size and length methods may require O(n) time complexity, and performance may be reduced.


## 2. Vulnerability Countermeasure
* Use the isEmpty or nonEmpty methods.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   seq.length > 0
   seq.length != 0
   seq.length == 0
}
```

* Safe Code

```SCALA
class Test {
   seq.nonEmpty
   seq.nonEmpty
   seq.isEmpty
}

```
