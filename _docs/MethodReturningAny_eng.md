---
title: Method Returning Any
category: ""
order: 0
---

## 1. Vulnerability Description
* If the method returns Any, the type is not explicitly defined, resulting in unintended result.


## 2. Vulnerability Countermeasure
* Returns a variable of explicit type.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   def foo : Any = 1
}
```

* Safe Code

```SCALA
class Test {
   def foo : Int = 1
}
```
