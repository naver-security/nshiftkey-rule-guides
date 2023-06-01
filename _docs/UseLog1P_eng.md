---
title: Incorrect calculation results
category: ""
order: 0
---

## 1. Vulnerability Description
* If a formula is configured arbitrarily, significant loss of accuracy may occur.


## 2. Vulnerability Countermeasure
* Use a funtion that fits your purpose.

## 3. Sample Code
### (1) Cbrt
* Vulnerable Code

```SCALA
class Test {
  scala.math.pow(x, 1/3d)
  math.pow(x, 1/3d)
}
```

* Safe Code

```SCALA
class Test {
    math.cbrt(x)
}
```

### (2) ExpM1
* Vulnerable Code

```SCALA
class Test {
  math.exp(x) - 1
}
```

* Safe Code

```SCALA
class Test {
  math.expm1(x)
}
```

### (3) Log10
* Vulnerable Code

```SCALA
class Test {
  math.log(x)/math.log(10)
}
```

* Safe Code

```SCALA
class Test {
  math.log10(x)
}
```

### (4) Log1P
* Vulnerable Code

```SCALA
class Test {
  math.log(x + 1)
}
```

* Safe Code

```SCALA
class Test {
  math.log1p(x)
}
```

### (5) Sqrt
* Vulnerable Code

```SCALA
class Test {
  scala.math.pow(2, 0.5)
}
```

* Safe Code

```SCALA
class Test {
  math.sqrt(x)
}
```
