---
title: Variable shadowing
category: ""
order: 0
---

## 1. Vulnerability Description
* If a variable with the same name declared outside is used inside a function, the code readability is degraded and unintended results may occur.

## 2. Vulnerability Countermeasure
* Do not use Variable shadowing.

## 3. Sample Code
* Vulnerable Code

```SCALA
Class Test {
  def foo = {
    val a = 1
    def boo = {
      val a = 2
      println(a)
    }
  }
}
```
