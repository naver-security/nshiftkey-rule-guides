---
title: Self-assignment
category: ""
order: 0
---

## 1. Vulnerability Description
* Self-assignment means that an object computes itself.
* There is a risk of multiple references that refer to one object in several places and may cause a crash.

## 2. Vulnerability Countermeasure
* If you have a function with multi-parameter, It is necessary to check whether the function works normally when each parameter is the same.

## 3. Sample Code
* Vulnerable Code

```c++
Window& Window::operator=(const Window& rhs)
{
    delete sb;
    sb = new ScrollBar(*rhs.sb);
    return *this;
}
```

* Safe Code

```c++
Window& Window::operator=(const Window& rhs)
{
    // Check that it is self-assignment
    if (this == &rhs;)
	return *this;
    // Make sure to copy it because throw can occur after delete.
    ScrollBar *sbOld = sb;
    sb = new ScrollBar(*rhs.sb);
    delete sbOld;
    return *this;
}
```
