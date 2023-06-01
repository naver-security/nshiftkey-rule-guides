---
title: Interface is not thread-safe
category: ""
order: 0
---

## 1. Vulnerability Description
* Detect if @ThreadSafe Annotation is not set in the Thread-safe context.

## 2. Vulnerability Countermeasure
* Set up @ThreadSafe Annotation on the interface or interface method to specify what is called a Thread-safe context.

## 3. Example Code
* Vulnerable code

```java
interface I {
  void bar();
}

@ThreadSafe
class C {
  void foo(I i) {
    i.bar(); // RacerD warns here
  }
}
```

* Safe code

```java
@ThreadSafe
interface I {
  void bar();
}

@ThreadSafe
class C {
  void foo(I i) {
    i.bar();
  }
}
```
