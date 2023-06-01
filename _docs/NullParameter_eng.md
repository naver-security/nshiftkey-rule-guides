---
title: Use of Null value
category: ""
order: 0
---

## 1. Vulnerability Description
* Null is not recommended in functional programming, and Scala is also not recommended.
* link: https://docs.scala-lang.org/overviews/scala-book/no-null-values.html

## 2. Vulnerability Countermeasure
* Do not use Null.
* Use Option/Some/None, which allows exception handling without using null.
