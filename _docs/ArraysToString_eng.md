---
title: Incorrect Serialize
category: ""
order: 0
---

## 1. Vulnerability Description
* If you serialize the Array by using String.format, you cannot receive a correct String value.


## 2. Vulnerability Countermeasure
* Use the mkString method of the Array class to serialize.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
    val array = Array("sam")
    "%s".format(array)

    "%s".format(Array("inline"))
}
```

* Safe Code
  * Use mkString.

```SCALA
class Test {
    Array("aa", "bb", "cc").mkString("")
}

```
