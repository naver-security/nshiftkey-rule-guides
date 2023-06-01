---
title: Dead code
category: ""
order: 0
---

## 1. Vulnerability Description
* Unimplemented blocks are considered dead codes.


## 2. Vulnerability Countermeasure
* If not used, delete it, and complete the implementation.

## 3. Sample Code
* Vulnerable Code

```SCALA
object Test {
  for (k <- 1 to 100) {
  }
  
  if (true) {
  }
}
```

