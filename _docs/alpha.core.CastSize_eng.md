---
title: Improper buffer size allocation
category: ""
order: 0
---

## 1. Vulnerability Description
* If you set a negative value to a dynamic allocation size, a large size is allocated and memory shortage may occur.
Also, if the memory allocation size is not calculated correctly, buffer overflow or memory overuse may occur.

## 2. Vulnerability Countermeasure
* Checks whether the value for allocating dynamic memory is negative.
* Checks whether the value for allocating dynamic memory is within an acceptable range.


## 3. Sample Code
* Vulnerable Code

```c
public static void main(String[] args) {
   int size = new Integer(args[0].intValue());
   size += new Integer(args[1].intValue());
   MyClass[] data = new Myclass[size];
   ...
}
```

* Safe Code

```c
public static void main(String[] args) {
   int size = new Integer(args[0].intValue());
   size += new Integer(args[1].intValue());
   if (size < 0) return;
   MyClass[] data = new Myclass[size];
   ...
}
```