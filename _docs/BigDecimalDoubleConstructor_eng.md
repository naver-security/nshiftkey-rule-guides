---
title: Use double type in BigDecimal constructor
category: ""
order: 0
---

## 1. Vulnerability Description
* Unintentional results may occur when using double type value as a parameter of BigDecimal constructor.


## 2. Vulnerability Countermeasure
* To safely create a BigDecimal variable of double type, use String as a parameter of the constructor.

## 3. Sample Code

```SCALA

BigDecimal b = new BigDecimal(13.9);
BigDecimal b2 = new BigDecimal("13.9");
println("%s %s %d%n", b, b2, b.compareTo(b2));

// output
13.9000000000000003552713678800500929355621337890625 13.9 1
```


