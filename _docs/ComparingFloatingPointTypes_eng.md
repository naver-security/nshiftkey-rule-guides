---
title: Wrong real number comparison
category: ""
order: 0
---

## 1. Vulnerability Description
* Comparing values in the form of FloatingPointType to == or != may result in different comparison results due to error.

## 2. Vulnerability Countermeasure
* Comparison should be made considering Precision.

## 3. Sample Code
* Vulnerable Code

```SCALA
scala> val a = 0.3
a: Double = 0.3

scala> val b = 0.1 + 0.2
b: Double = 0.30000000000000004

scala> a == b
res4: Boolean = false
```

* Safe Code

```SCALA
def ~=(x: Double, y: Double, precision: Double) = {
  if ((x - y).abs < precision) true else false
}

scala> val a = 0.3
a: Double = 0.3

scala> val b = 0.1 + 0.2
b: Double = 0.30000000000000004

scala> ~=(a, b, 0.0001)
res0: Boolean = true

```
