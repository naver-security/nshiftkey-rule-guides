---
title: Determine whether or not it is empty using size, length
category: ""
order: 0
---

## 1. Vulnerability Description
* When determining the empty of data structure, using size or length, O(n) time complexity may be required and performance may be reduced.

## 2. Vulnerability Countermeasure
* Use nonEmpty if you are using isEmpty, non-empty to determine empty.

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
