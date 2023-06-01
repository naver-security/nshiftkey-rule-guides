---
title: Generate predictable random values
category: ""
order: 0
---

## 1. Vulnerability Description
* When creating predictable random values and using them as security elements such as session IDs and tokens, an attacker can predict random values and attack the system. 
* Since rand() has a constant base number, it can reproduce a random number that returns a value corresponding to the seed value and can generate predictable random values.

## 2. How to check vulnerability
* Check that you use rand().


## 3. Vulnerability Countermeasure
* Instead of rand(), make sure to use random().


## 4. Sample Code
* Vulnerable Code

```c
#include <stdio.h>
#include <stdlib.h>
  
enum { len = 12 };
  
void func(void) {
  /*
   * id will hold the ID, starting with the characters
   *  ""ID"" followed by a random integer.
   */
  char id[len]; 
  int r;
  int num;
  /* ... */
  r = rand();  /* Generate a random integer */
  num = snprintf(id, len, ""ID%-d"", r);  /* Generate the ID */
  /* ... */
}
```


* Safe Code

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
enum { len = 12 }; 
 
void func(void) {
  /*
   * id will hold the ID, starting with the characters
   *  ""ID"" followed by a random integer.
   */
  char id[len]; 
  int r;
  int num;
  /* ... */
  struct timespec ts;
  if (timespec_get(&ts, TIME_UTC) == 0) {
    /* Handle error */
  }
  srandom(ts.tv_nsec ^ ts.tv_sec);  /* Seed the PRNG */
  /* ... */
  r = random();  /* Generate a random integer */
  num = snprintf(id, len, ""ID%-d"", r);  /* Generate the ID */
  /* ... */
}
```
