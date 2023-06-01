---
title: Freed memory reference
category: ""
order: 0
---

## 1. Vulnerability Description
* Returning or referencing memory freed variables can cause a crash by referring to an unintended value.

## 2. Vulnerability Countermeasure
* Do not use memory freed variables


## 3. Sample Code
* Vulnerable Code 1

```c
#include <stdlib.h>
  
struct node {
  int value;
  struct node *next;
};
  
void free_list(struct node *head) {
  for (struct node *p = head; p != NULL; p = p->next) {
    free(p);
  }
}
```

* Safe Code

```c
#include <stdlib.h>
  
struct node {
  int value;
  struct node *next;
};
  
void free_list(struct node *head) {
  struct node *q;
  for (struct node *p = head; p != NULL; p = q) {
    q = p->next;
    free(p);
  }
```

* Vulnerable Code 2

```c
#include <stdlib.h>
#include <string.h>
 
int main(int argc, char *argv[]) {
  char *return_val = 0;
  const size_t bufsize = strlen(argv[0]) + 1;
  char *buf = (char *)malloc(bufsize);
  if (!buf) {
    return EXIT_FAILURE;
  }
  /* ... */
  free(buf);
  /* ... */
  strcpy(buf, argv[0]);
  /* ... */
  return EXIT_SUCCESS;
}
```

* Safe Code 2

```c
#include <stdlib.h>
#include <string.h>
 
int main(int argc, char *argv[]) {
  char *return_val = 0;
  const size_t bufsize = strlen(argv[0]) + 1;
  char *buf = (char *)malloc(bufsize);
  if (!buf) {
    return EXIT_FAILURE;
  }
  /* ... */
  strcpy(buf, argv[0]);
  /* ... */
  free(buf);
  return EXIT_SUCCESS;
}
```
