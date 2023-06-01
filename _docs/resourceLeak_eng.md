---
title: Skip dynamic memory release
category: ""
order: 0
---

## 1. Vulnerability Description
* If the allocated memory is not released, a memory leak may occur.


## 2. Vulnerability Countermeasure
* After using the allocated memory, you must release the memory.


## 3. Sample Code
* Vulnerable Code

```c++
#include <stdlib.h>
  
enum { BUFFER_SIZE = 32 };
 
int f(void) {
  char *text_buffer = (char *)malloc(BUFFER_SIZE);
  if (text_buffer == NULL) {
    return -1;
  }
  ...
  return 0;
}
```

* Safe Code

```c++
#include <stdlib.h>
 
enum { BUFFER_SIZE = 32 };
 
int f(void) {
  char *text_buffer = (char *)malloc(BUFFER_SIZE);
  if (text_buffer == NULL) {
    return -1;
  }
  ...
  free(text_buffer);
  return 0;
}
```