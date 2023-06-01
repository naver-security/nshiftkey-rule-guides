---
title: Use pointer variable as Condition extension
category: ""
order: 0
---

## 1. Vulnerability Description
* If the pointer variable is used as Condition extension, the condition will always be True, which can lead to unintended behavior.

## 2. How to check vulnerability
* For the code below, it might be always true.
```
if (p+1) {
  /* ... */
}
```

## 3. Vulnerability Countermeasure
* Do not use pointer variable as Condition extension