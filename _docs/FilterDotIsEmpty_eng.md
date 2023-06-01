---
title: Use fliter().isEmpty
category: ""
order: 0
---

## 1. Vulnerability Description
* filter(.isEmpty scans the entire collection, which is likely to slow performance.

## 2. Vulnerability Countermeasure
* If you change it to !exists(), it is more advantageous for performance.

## 3. Sample Code
* Vulnerable Code

```SCALA
seq.filter(p).isDefined
seq.find(p).isDefined

seq.filter(p).isEmpty
seq.find(p).isEmpty
```

* Safe Code

```SCALA
seq.exists(p)
!seq.exists(p)
```
