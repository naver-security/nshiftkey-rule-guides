---
title: Improper release of Dynamic Memory Allocation
category: ""
order: 0
---

## 1. Vulnerability Description
* Memory leakage can occur if allocated memory is not released properly.


## 2. Vulnerability Countermeasure
* You must properly release the allocated memory.


## 3. Sample Code
#### placement new()
* Vulnerable Code
  * For the code below, program saved the address of the s1 variable to the s2 pointer (do not dynamically allocate memory), so deleting s2 may cause unexpected behavior.

```c++
#include <iostream>
  
struct S {
  S() { std::cout << "S::S()" << std::endl; }
  ~S() { std::cout << "S::~S()" << std::endl; }
};
  
void f() {
  S s1;
  S *s2 = new (&s1) S;
  
  // ...
  
  delete s2;
}
```

* Safe Code
  * For the code below, memory is automatically released when the f() function ends, so ::operator delete() function call is not required.

```c++
#include <iostream>
  
struct S {
  S() { std::cout << "S::S()" << std::endl; }
  ~S() { std::cout << "S::~S()" << std::endl; }
};
  
void f() {
  S s1;
  S *s2 = new (&s1) S;
  
  // ...
}
```


#### Uninitialized delete
* Vulnerable Code
  * Deleting an uninitialized pointer may lead to unexpected behavior.

```c++
#include <new>
  
void f() {
  int *i1, *i2;
  try {
    i1 = new int;
    i2 = new int;
  } catch (std::bad_alloc &) {
    delete i1;
    delete i2;
  }
}
```

* Safe Code
  * Pointer should be initialized before use.
  
```c++
#include <new>
  
void f() {
  int *i1 = nullptr, *i2 = nullptr;
  try {
    i1 = new int;
    i2 = new int;
  } catch (std::bad_alloc &) {
    delete i1;
    delete i2;
  }
}
```