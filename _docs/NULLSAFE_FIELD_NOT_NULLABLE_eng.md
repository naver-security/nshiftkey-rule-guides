---
title: Field is not @Nullable
category: ""
order: 0
---

## 1. Vulnerability Description
* Detect if the field is set to Null without @Nullable Annotation.


## 2. Vulnerability Countermeasure
* If a Null value is allowed, set @Nullable Annotation.

## 3. Sample Code
* Vulnerable Code

```java
  private List<String> idList;
  public void reset() {
    idList = null;
    ...
  }
```

* Safe Code

```java
  import javax.annotation.Nullable;
  ...
  private @Nullable List<String> idList;
  public void reset() {
    idList = null;
    ...
  }
```
