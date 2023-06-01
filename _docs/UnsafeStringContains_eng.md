---
title: Unsafe String contains
category: ""
order: 0
---

## 1. Vulnerability Description
* Comparing unrelated variables using Contain can cause unintended behavior.


## 2. Vulnerability Countermeasure
* When using Contain, it is necessary to verify that the types are compatible type.

## 3. Sample Code
* Vunlerable Code

```SCALA
class Test {
    "abcdefgh".contains(2)
}
```

* Safe Code

```SCALA
class Test {
    "abcd".contains("abc")
}
```
