---
title: Shift Negative
category: ""
order: 0
---

## 1. Vulnerability Description
* If negative numbers are used as operands of bit operation or if shift left operand is greater than number of bits in the operand type, the correct operation is not guaranteed.


## 2. Vulnerability Countermeasure
* Use positive numbers as operand values.
* Do shift left operation using less than the number of bits in the operand type.


## 3. Sample Code
* Vulnerable Code

```c
void func(unsigned int ui_a, unsigned int ui_b) {
  unsigned int uresult = ui_a << ui_b;
  /* ... */
}
```

* Safe Code

```c
#include <limits.h>
#include <stddef.h>
#include <inttypes.h>
 
extern size_t popcount(uintmax_t);
#define PRECISION(x) popcount(x)
  
void func(unsigned int ui_a, unsigned int ui_b) {
  unsigned int uresult = 0;
  if (ui_b >= PRECISION(UINT_MAX)) {
    /* Handle error */
  } else {
    uresult = ui_a << ui_b;
  }
  /* ... */
}
```
