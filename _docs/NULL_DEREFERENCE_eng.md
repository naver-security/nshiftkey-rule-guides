---
title: Null pointer Dereference
category: ""
order: 0
---

## 1. Vulnerability Description
* In the following cases, referencing null can cause NPE (NullPointerException).
  * When using object is NULL
  * When not checking NULL pointer

## 2. Vulnerability Countermeasure
* Check for NULL before referencing object
* Don't use NULL as return value

## 3. Sample Code
* Vulnerable Code

```c
p = foo(); // foo() might return null   
stuff();   
p.goo();   // dereferencing p, potential NPE

```

* Safe Code

```c
p = foo(); // foo() might return null   
stuff();   
if (p != null) {
    p.goo(); 
}
```
