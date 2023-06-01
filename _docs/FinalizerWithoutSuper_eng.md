---
title: Missing finalizer behavior in Superclass 
category: ""
order: 0
---

## 1. Vulnerability Description
* finalize of superclass must be enabled.


## 2. Vulnerability Countermeasure
* Call super.finalize()

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
  override def finalize {
    println("naver")
  }
}
```

* Safe Code

```SCALA
class Test {
  override def finalize {
    super.finalize()
    println("naver")
  }
}
```
