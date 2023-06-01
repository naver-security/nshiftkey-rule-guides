---
title: Unsafe traversable method
category: ""
order: 0
---

## 1. Vulnerability Description
* When Collection is empty, throw can occur if the following method is used.

```
"head",
"tail",
"init",
"last",
"reduce(_+_)",
"reduceLeft(_+_)",
"reduceRight(_+_)",
"max",
"maxBy(x => x)",
"min",
"minBy(x => x)"
```

## 2. Vulnerability Countermeasure
* Processing is required when Collection is empty.

