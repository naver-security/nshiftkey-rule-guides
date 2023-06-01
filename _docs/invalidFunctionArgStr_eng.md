---
title: String parameter not terminated with null
category: ""
order: 0
---

## 1. Vulnerability Description
If a non-null terminated string is used as an input value of a string library function, buffer overflow can occur inside the function.

## 2. Vulnerability Countermeasure
Do not use a non-null terminated string as an input value of the string library function.

## 3. Sample Code
* Vulnerable Code

```c
#include <stdio.h>
  
void func(void) {
  char c_str[3] = ""abc"";
  printf(""%s\n"", c_str);
}
```

* Safe Code

```c
#include <stdio.h>  

void func(void) {
  char c_str[] = ""abc"";
  printf(""%s\n"", c_str);
}
```
