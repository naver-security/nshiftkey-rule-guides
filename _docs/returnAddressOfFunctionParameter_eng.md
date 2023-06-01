---
title: Bad local variable reference
category: ""
order: 0
---

## 1. Vulnerability Description
* When returning the address value of a local variable, the value cannot be referenced when the function is terminated.
* Accessing outside the valid range of the variable may result in abnormal behavior or malicious code execution.


## 2. Vulnerability Countermeasure
* Consider the lifetime of a variable to declare and use.


## 3. Sample Code
#### Reference between variables with different lifetime
* Vulnerable C Code

```c
#include <stdio.h>
  
const char *p;
void dont_do_this(void) {
  const char c_str[] = "This will change";
  p = c_str; /* Dangerous */
}
 
void innocuous(void) {
  printf("%s\n", p);
}
 
int main(void) {
  dont_do_this();
  innocuous();
  return 0;
}
```

* Safe C Code

```c
void this_is_OK(void) {
  const char c_str[] = "Everything OK";
  const char *p = c_str;
  /* ... */
}
/* p is inaccessible outside the scope of string c_str */
```

#### reference a variable with expired lifetime
* Vulnerable C Code

```c
void squirrel_away(char **ptr_param) {
  char local[10];
  /* Initialize array */
  *ptr_param = local;
}
 
void rodent(void) {
  char *ptr;
  squirrel_away(&ptr);
  /* ptr is live but invalid here */
}
```

* Safe C Code

```c
char local[10];
  
void squirrel_away(char **ptr_param) {
  /* Initialize array */
  *ptr_param = local;
}
 
void rodent(void) {
  char *ptr;
  squirrel_away(&ptr);
  /* ptr is valid in this scope */
}
```
