---
title: A comparison for extraneous type 
category: ""
order: 0
---

## 1. Vulnerability Description
* If there is an unparalleled type of comparison, it can cause bugs.


## 2. Vulnerability Countermeasure
* Make sure that the variables you want to compare are comparable.

## 3. Sample Code
* Vulnerable Code

```SCALA
object Main {
  def main(args: Array[String]): Unit = {
    val stringOption: Option[String] = Some("1")
    val intOption: Option[Int] = Some(1)
    stringOption == intOption
  }
}
```

