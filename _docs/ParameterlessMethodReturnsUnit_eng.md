---
title: Returning Unit with Parameterless Method
category: ""
order: 0
---

## 1. Vulnerability Description
* In Scala's convention, methods without parentheses must ensure that there are no side-effects, but side-effects may exist if they return Unit.


## 2. Vulnerability Countermeasure
* Define the method by generating empty parentheses.

## 3. Sample Code
* Vulnerable Code

```SCALA
object Test {
   def paramless: Unit = ()
}
```

* Safe Code

```SCALA
object Test {
   def params(): Unit = ()
}
```
