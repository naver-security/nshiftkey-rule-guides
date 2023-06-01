---
title: Use of JavaConvention
category: ""
order: 0
---

## 1. Vulnerability Description
* If Java Conversion does not occur explicitly, unexpected errors can occur.


## 2. Vulnerability Countermeasure
* Use JavaConverters to explicitly enable Java Conversion, and you must use CollectionConverters after Scala 2.13.

## 3. Example Code
* Vulnerable code

```SCALA
import scala.collection.JavaConversions._
object Test {
   val jul = new java.util.ArrayList[String]
   val jum = new java.util.HashMap[String,String]
   val a = jul.exists(_ == "sammy")
   val b = jum.toSeq
}
```

* Safe code

```SCALA
import scala.jdk.CollectionConverters._
object Test {
    val s = collection.mutable.Set("one")
    val js = s.asJava
    js.add("two")
```
