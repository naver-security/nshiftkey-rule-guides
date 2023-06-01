---
title: Zero Size Memory Allocation
category: ""
order: 0
---

## 1. Vulnerability Description
* If the size is 0 when memory is allocated dynamically, a crash can occur because there is no fixed result in the operation.


## 2. Vulnerability Countermeasure
* Do not allocate memory allocation size value to zero


## 3. Sample Code
### When using the malloc() function
* Vulnerable Code
  * The code below may cause heap-buffer overflow.

```c
size_t size;
 
/* Initialize size, possibly by user-controlled input */
 
int *list = (int *)malloc(size);
if (list == NULL) {
  /* Handle allocation error */
}
else {
/* Continue processing list */
}
```

* Safe Code

```c
size_t size;
 
/* Initialize size, possibly by user-controlled input */
 
if (size == 0) {
  /* Handle error */
}
int *list = (int *)malloc(size);
if (list == NULL) {
  /* Handle allocation error */
}
/* Continue processing list */
```

### When using the realloc() function
* Vulnerable Code

```c
size_t nsize = /* Some value, possibly user supplied */;
char *p2;
char *p = (char *)malloc(100);
if (p == NULL) {
  /* Handle error */
}
 
/* ... */
 
if ((p2 = (char *)realloc(p, nsize)) == NULL) {
  free(p);
  p = NULL;
  return NULL;
}
p = p2;
```

* Safe Code

```c
size_t nsize;
/* Initialize nsize */
char *p2;
char *p = (char *)malloc(100);
if (p == NULL) {
  /* Handle error */
}
 
/* ... */
 
p2 = NULL;
if (nsize != 0) {
  p2 = (char *)realloc(p, nsize);
}
if (p2 == NULL) {
  free(p);
  p = NULL;
  return NULL;
}
p = p2;
```