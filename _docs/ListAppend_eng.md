---
title: Use of append in List
category: ""
order: 0
---

## 1. Vulnerability Description
* If you use ":+" to apply to a list with an imputable attribute, performance may be compromised.


## 2. Vulnerability Countermeasure
* If you frequently use append, you should use the ListBuffer, which has an Append cost of O(1).

## 3. Example Code
* Vulnerable code

```SCALA
class Test {
   val a = List("list")
   a :+ "oh no"
}
```

* Safe code

```SCALA
import scala.collection.mutable.ListBuffer 
class Test {
   var name = ListBuffer[String]()   
   name += "good"
   name += "oh good"
}
```

