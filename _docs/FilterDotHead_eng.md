---
title: Exception can occur on filter.Head
category: ""
order: 0
---

## 1. Vulnerability Description
* filter().head can cause through when collection is empty.

## 2. Vulnerability Countermeasure
* If the collection is empty, replace it with ffind() match {..} .

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test {
   List(1,2,3).filter(_ < 0).head
}
```

