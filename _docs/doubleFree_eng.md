---
title: Double-released of dynamically allocated memory
category: ""
order: 0
---

## 1. Vulnerability Description
* If the dynamically allocated memory is double-released, a memory leak may occur.

## 2. Vulnerability Countermeasure
* Do not release the memory twice and set the released memory variable to NULL

## 3. Sample Code
* Vulnerable Code

```c
#include <stdio.h>
#include <unistd.h>

#define BUFSIZE1    512
#define BUFSIZE2    ((BUFSIZE1/2) - 8)

int main(int argc, char **argv) {
  char *buf1R1;
  char *buf2R1;
  char *buf1R2;

  buf1R1 = (char *) malloc(BUFSIZE2);
  buf2R1 = (char *) malloc(BUFSIZE2);

  free(buf1R1);
  free(buf2R1);

  buf1R2 = (char *) malloc(BUFSIZE1);
  strncpy(buf1R2, argv[1], BUFSIZE1-1);

  free(buf2R1);
  free(buf1R2);
}
```

* Safe Code

```c
#include <stdio.h>
#include <unistd.h>

#define BUFSIZE1    512
#define BUFSIZE2    ((BUFSIZE1/2) - 8)

int main(int argc, char **argv) {
  char *buf1R1 = NULL;
  char *buf2R1 = NULL;
  char *buf1R2 = NULL;

  buf1R1 = (char *) malloc(BUFSIZE2);
  buf2R1 = (char *) malloc(BUFSIZE2);

  if(buf1R1 != NULL) {
     free(buf1R1);
     buf1R1= NULL;
  }
  if(buf2R1 != NULL) {
     free(buf2R1);
     buf2R1= NULL;
  }

  buf1R2 = (char *) malloc(BUFSIZE1);
  strncpy(buf1R2, argv[1], BUFSIZE1-1);
  if(buf1R2 != NULL) {
     free(buf1R2);
     buf1R2 = NULL;
  }
```
