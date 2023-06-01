---
title: Returns a variable type that is different from the definition
category: ""
order: 0
---

## 1. Vulnerability Description
If the method that returns the mutable type returns an immutable collection and that value is used, a runtime error may occur.

## 2. Vulnerability Countermeasure
You must change the return value to immutable or copy the collection to use.

## 3. Sample Code
* Vulnerable Code

```java
  public List<String> getSomeList() {
    ImmutableList<String> l = foo(...);
    return l;
  }
```

* Safe Code

```java
  public ImmutableList<String> getSomeList() {
    ImmutableList<String> l = foo(...);
    return l;
  }
```
