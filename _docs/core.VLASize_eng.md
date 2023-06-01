---
title: Set size of VLA(Variable-Length Array) to valid range
category: ""
order: 0
---

## 1. Vulnerability Description
* If you use zero or uninitialized variables as the size of the array variable, you may overuse memory or access unintended addresses.

## 2. Vulnerability Countermeasure
* Set size of Array to valid range


## 3. Sample Code
* Vulnerable Code

```c
#include <stddef.h>
 
extern void do_work(int *array, size_t size);
  
void func(size_t size) {
  int vla[size];
  do_work(vla, size);
}
```

* Safe Code

```c
#include <stdint.h>
#include <stdlib.h>
  
enum { MAX_ARRAY = 1024 };
extern void do_work(int *array, size_t size);
  
void func(size_t size) {
  if (0 == size || SIZE_MAX / sizeof(int) < size) {
    /* Handle error */
    return;
  }
  if (size < MAX_ARRAY) {
    int vla[size];
    do_work(vla, size);
  } else {
    int *array = (int *)malloc(size * sizeof(int));
    if (array == NULL) {
      /* Handle error */
    }
    do_work(array, size);
    free(array);
  }
}
```