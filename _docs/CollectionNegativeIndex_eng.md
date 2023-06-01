---
title: Abnormal index range reference 
category: ""
order: 0
---

## 1. Vulnerability Description
* If abnormal range is referenced, sensitive information may be leaked or crash may occur.


## 2. Vulnerability Countermeasure
* If array variables are used, reference should be made within normal range.


## 3. Sample Code
* Vulnerable Code
  * For the code below, the index is negative, which can cause unexpected behavior.

```SCALA
object Test 
{
    List(1,2,3)(-2)
}
```
