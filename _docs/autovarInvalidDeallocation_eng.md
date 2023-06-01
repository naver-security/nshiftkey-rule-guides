---
title: Bad free of a variable not dynamically allocated
category: ""
order: 0
---

## 1. Vulnerability Description
* If you force release memory of a variable that is not dynamically allocated, an error such as heap corruption may occur.


## 2. How to check vulnerability
* Errors can occur when using free() or realloc() to a variable not dynamically allocated.


## 3. Vulnerability Countermeasure
* Do not use a function such as free() to release memory for variables other than those allocated using the standard memory allocation function.


## 4. Sample Code
#### Case of using the free() function to release memory.
* Vulnerable Code

```c
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
  
enum { MAX_ALLOCATION = 1000 };
 
int main(int argc, const char *argv[]) {
  char *c_str = NULL;
  size_t len;
 
  if (argc == 2) {
    len = strlen(argv[1]) + 1;
    if (len > MAX_ALLOCATION) {
      /* Handle error */
    }
    c_str = (char *)malloc(len);
    if (c_str == NULL) {
      /* Handle error */
    }
    strcpy(c_str, argv[1]);
  } else {
    c_str = "usage: $>a.exe [string]";
    printf("%s\n", c_str);
  }
  free(c_str);
  return 0;
}
```

* Safe Code

```c
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
  
enum { MAX_ALLOCATION = 1000 };
 
int main(int argc, const char *argv[]) {
  char *c_str = NULL;
  size_t len;
 
  if (argc == 2) {
    len = strlen(argv[1]) + 1;
    if (len > MAX_ALLOCATION) {
      /* Handle error */
    }
    c_str = (char *)malloc(len);
    if (c_str == NULL) {
      /* Handle error */
    }
    strcpy(c_str, argv[1]);
  } else {
    printf("%s\n", "usage: $>a.exe [string]");
    return EXIT_FAILURE;
  }
  free(c_str);
  return 0;
}
```


#### Case of using the realloc() function to release memory.
* Vulnerable Code

```c
#include <stdlib.h>
  
enum { BUFSIZE = 256 };
  
void f(void) {
  char buf[BUFSIZE];
  char *p = (char *)realloc(buf, 2 * BUFSIZE);
  if (p == NULL) {
    /* Handle error */
  }
}
```

* Safe Code

```c
#include <stdlib.h>
  
enum { BUFSIZE = 256 };
  
void f(void) {
  char *buf = (char *)malloc(BUFSIZE * sizeof(char));
  char *p = (char *)realloc(buf, 2 * BUFSIZE);
  if (p == NULL) {
    /* Handle error */
  }
}
```
