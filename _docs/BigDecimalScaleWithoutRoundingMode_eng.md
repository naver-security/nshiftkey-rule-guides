---
title: Missing RoundingMode in use of BigDecimal.setScale
category: ""
order: 0
---

## 1. Vulnerability Description
* When using the setScale() of BigDecimal, if you do not provide a RoundingMode, it can result in an exception being thrown.


## 2. Vulnerability Countermeasure
* Provide a RoundingMode value when using the setScale() method to ensure proper rounding behavior and avoid exceptions.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
    val b = BigDecimal(10)
    b.setScale(2)
}
```

* Safe Code

```SCALA
class Test {
    import scala.math.BigDecimal.RoundingMode
    val b = BigDecimal(10)
    b.setScale(2, RoundingMode.HALF_UP)
}

```
