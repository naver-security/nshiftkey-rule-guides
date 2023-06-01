---
title: Use parameter of invalid type
category: ""
order: 0
---

## 1. Vulnerability Description
* If you enter a parameter that is incompatible with the declared type in a function, the value may be changed and unintended behavior may occur.


## 2. Vulnerability Countermeasure
* Input function parameters with valid type.


## 3. Sample Code
* Vulnerable Code

```c
/* In another source file */
long f(long x) {
  return x < 0 ? -x : x;
}
 
/* In this source file, no f prototype in scope */
long f();
  
long g(int x) {
  return f(x);
}
```

* Safe Code

```c
/* In another source file */
long f(long x) {
  return x < 0 ? -x : x;
}
 
/* f prototype in scope in this source file */
long f(long x);
 
long g(int x) {
  return f((long)x); 
}
```