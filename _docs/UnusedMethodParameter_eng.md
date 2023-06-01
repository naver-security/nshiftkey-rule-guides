---
title: Unused  method parameter
category: ""
order: 0
---

## 1. Vulnerability Description
* Unused method parameters must be deleted.


## 2. Vulnerability Countermeasure
* Delete unused method parameters.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   val init="naver"
   def foo(a:String, b:Int, c:Int) {
      println(b)
      foo(a,b,b)
   }
}
```

