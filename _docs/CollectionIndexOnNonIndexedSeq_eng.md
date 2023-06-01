---
title: Access from Non-indexedseq to index
category: ""
order: 0
---

## 1. Vulnerability Description
* "Non-indexedSeq" data structure access to "index" takes O(n) time complexity.

## 2. Vulnerability Countermeasure
* "IndexedSeq" may be an alternative if "Seq" data structures are frequently accessed via "index".
* "IndexedSeq" takes O(1) time complexity to access the data structure via "index".

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
    val idx = 2
    Seq(1,2,3)(idx)
}
```

* Safe Code

```SCALA
class Test {
    val idx = 2
    IndexedSeq(1,2,3)(idx)
}

```
