---
title: Public finalizer
category: ""
order: 0
---

## 1. Vulnerability Description
* If declare the finalizer as public, the encapsulation is broken by being able to call the Finalizer from anywhere.


## 2. Vulnerability Countermeasure
* Do not declare the finalizer as public.

## 3. Sample Code
* Vulnerable Code

```SCALA
Class Test {
    override def finalize : Unit = ()
}
```

* Safe Code

```SCALA
class Test {
    override protected def finalize : Unit = ()
}
```
