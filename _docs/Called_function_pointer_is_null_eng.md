---
title: NULL Pointer Reference
category: ""
order: 0
---

## 1. Vulnerability Description
* Crash may occur in the following cases:
  * If the function pointer or object you want to call is NULL
  * To enter NULL values for cstring function parameters or function parameters that are nonnull attribute
  * If NULL pointer is not checked

## 2.  Vulnerability Countermeasure
* To check for NULL before referencing a pointer

## 3. Sample Code
* Vulnerable Code

```c
#include <string.h>
#include <stdlib.h>
  
void f(const char *input_str) {
  size_t size = strlen(input_str) + 1;
  char *c_str = (char *)malloc(size);
  memcpy(c_str, input_str, size);
  /* ... */
  free(c_str);
  c_str = NULL;
  /* ... 
```

* Safe Code

```c
#include <string.h>
#include <stdlib.h>
  
void f(const char *input_str) {
  size_t size;
  char *c_str = NULL;
  
  if (NULL == input_str) {
    /* Handle error */
  }
   
  size = strlen(input_str) + 1;
  c_str = (char *)malloc(size);
  if (NULL == c_str) {
    /* Handle error */
  }
  memcpy(c_str, input_str, size);
  /* ... */
  free(c_str);
  c_str = NULL;
  /* ... */
}
```
