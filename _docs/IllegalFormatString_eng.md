---
title: Illegal use of  format string
category: ""
order: 0
---

## 1. Vulnerability Description
* If an invalid format string is used, throw may occur.


## 2. Vulnerability Countermeasure
* Verify that format string is correct.

## 3. Example code
* Vulnerable code

```SCALA
object Test {
  "%5.5q".format("sam")
  "% s".format("sam")
  "%.s".format("sam")
  "%<s %s".format("sam", "sam")

  "%s %.2f".format("sam")
}
```
