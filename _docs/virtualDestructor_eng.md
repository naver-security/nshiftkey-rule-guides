---
title: Delete polymorphic object without virtual destructor
category: ""
order: 0
---

## 1. Vulnerability Description
* If the Base class destructor is not declared as virtual, a memory leak may occur when the derived class is released.

## 2. Vulnerability Countermeasure
* Base class destructor must be declared as virtual.

## 3. Sample Code
* Vulnerable Code

```c++
struct Base {
  virtual void f();
};
  
struct Derived : Base {};
  
void f() {
  Base *b = new Derived();
  // ...
  delete b;
}
```

* Safe Code

```c++
struct Base {
  virtual ~Base() = default;
  virtual void f();
};
 
struct Derived : Base {};
 
void f() {
  Base *b = new Derived();
  // ...
  delete b;
}
```
