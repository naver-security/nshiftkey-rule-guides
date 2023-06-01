---
title: Integer Overflow
category: ""
order: 0
---

## 1. Vulnerability Description
* An integer overflow is a type of an arithmetic overflow error when the result of an integer operation does not fit within the allocated memory space. Instead of an error in the program, it usually causes the result to be unexpected.

## 2. Vulnerability Countermeasure
* After checking the available range of type, you should use the correct type of variable.

## 3. Sample Code
* Vulnerable Code

```c
#include <stdlib.h>
#include <stdint.h>  /* For SIZE_MAX */
  
enum { BLOCK_HEADER_SIZE = 16 };
 
void *AllocateBlock(size_t length) {
  struct memBlock *mBlock;
 
  if (length + BLOCK_HEADER_SIZE > (unsigned long long)SIZE_MAX)
    return NULL;
  mBlock = (struct memBlock *)malloc(
    length + BLOCK_HEADER_SIZE
  );
  if (!mBlock) { return NULL; }
  /* Fill in block header and return data portion */
 
  return mBlock;
}
```


* Safe Code

```c
#include <stdlib.h>
#include <stdint.h>
 
 
enum { BLOCK_HEADER_SIZE = 16 };
  
void *AllocateBlock(size_t length) {
  struct memBlock *mBlock;
 
  // Avoid overflowing through the upcast.
  if ((unsigned long long)length + BLOCK_HEADER_SIZE > SIZE_MAX) {
    return NULL;
  }
  mBlock = (struct memBlock *)malloc(
    length + BLOCK_HEADER_SIZE
  );
  if (!mBlock) { return NULL; }
  /* Fill in block header and return data portion */
 
  return mBlock;
}
```
