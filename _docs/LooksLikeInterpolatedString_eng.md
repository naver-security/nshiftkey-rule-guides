---
title: Missing prefix in InterpolatedString
category: ""
order: 0
---

## 1. Vulnerability Description
* If interpolatedString is used, prefix must be set.


## 2. Vulnerability Countermeasure
* If you intend to use InterpolatedString, make sure that s,f or raw is attached to the prefix and that prefix is not missing.

## 3. Example Code
* Vulnerable code

```SCALA
class Test {
    val str = "this is my $interpolated string lookalike"
    val str2 = "this is my ${interpolated.string} lookalike"
}
```

* Safe code

```SCALA
class Test {
    val a = "hello"
    val str = s"${a}"
}

```
