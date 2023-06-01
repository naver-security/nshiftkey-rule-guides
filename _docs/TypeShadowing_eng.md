---
title: Type shadowing
category: ""
order: 0
---

## 1. Vulnerability Description
* Unintentional behavior can occur if Class and Method share a type parameter with the same name.

## 2. Vulnerability Countermeasure
* Type parameter names are defined differently.

## 3. Sample Code
* Vulnerable Code

```SCALA
class Test[T, U] {
    def foo[T] = {}
    def boo[A, U] = {}
}
```

* Safe Code

```SCALA
class Test[T,U] {
   def foo[B] = {}
   def goo[C >: U] = {}
   def boo[D <: T] = {}
}
```
