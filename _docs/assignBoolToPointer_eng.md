---
title: Assignment of bool type variable value to pointer variable
category: ""
order: 0
---

## 1. Vulnerability Description
* If you assign a bool type variable value to a pointer variable, a crash may occur.


## 2. Vulnerability Countermeasure
* Do not assign a bool type variable value to a pointer variable


## 3. Sample Code
* Vulnerable Code

```c
void f(void) {
  bool bTmp = false;
  char *ptr = (char*)bTmp;
  /* ... */
}
```

* Safe Code

```c
#include <stdint.h>
  
void f(void) {
  char *ptr = NULL;
  /* ... */
  uintptr_t number = (uintptr_t)ptr; 
  /* ... */
}
```