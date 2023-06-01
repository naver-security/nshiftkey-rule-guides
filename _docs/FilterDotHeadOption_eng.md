---
title: Use fliter().headOption
category: ""
order: 0
---

## 1. Vulnerability Description
* When trying to get the result of one of the filters, filter().headOption checks while visiting all collections, which may reduce performance.

## 2. Vulnerability Countermeasure
* Use find() instead of filter().headOption
* find() returns only the first one found.

## 3. Sample Code
* Vulnerable Code

```SCALA
seq.filter(p).headOption
```

* Safe Code

```SCALA
seq.find(p)
```
