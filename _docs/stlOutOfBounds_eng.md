---
title: Out of bound pointer variable reference
category: ""
order: 0
---

## 1. Vulnerability Description
* If you refer to the abnormal range, important information may be leaked or a crash may occur.


## 2. Vulnerability Countermeasure
* If you use array variables, you must refer to them within their normal range.


## 3. Sample Code
* Vulnerable Code
  * For the code below, if the index variable is negative, the if statement may be executed, causing unexpected behavior.

```c
enum { TABLESIZE = 100 };
 
static int table[TABLESIZE];
 
int *f(int index) {
  if (index < TABLESIZE) {
    return table + index;
  }
  return NULL;
}
```

* Safe Code

```c
enum { TABLESIZE = 100 };

static int table[TABLESIZE];

int *f(int index) {
  if (index >= 0 && index < TABLESIZE) {
    return table + index;
  }
  return NULL;
}
```
