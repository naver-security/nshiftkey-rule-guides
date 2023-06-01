---
title: Unnecessary variable type conversion.

category: ""
order: 0
---

## 1. Vulnerability Description
* Making unnecessary transformations is pointless and can degrade performance.

## 2. Vulnerability Countermeasure
* Do not do unnecessary convert the type of variable.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   val i = "sam"
   val j = i.toString
   
   val k = 4
   val l = i.toInt
}
```
