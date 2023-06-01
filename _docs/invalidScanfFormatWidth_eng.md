---
title: Invalid scanf format width
category: ""
order: 0
---

## 1. Vulnerability Description
* If the width is set as "%100s" by the format string of the scanf and the input variable does not have as much space as the width, a buffer overflow may occur.

## 2. Vulnerability Countermeasure
* Width must be allocated less than the allocated memory size of the input variable.

## 3. Sample Code
* Vulnerable Code
  * Buffer overflow can occur if more than 9 characters are entered in a variable with array size set to 10.
```c
char buffer[10];
scanf("%s", buffer);
```

* Safe Code
  * Set width to read up to 9 characters
```c
char buffer[10];
scanf("%9s", buffer);
```