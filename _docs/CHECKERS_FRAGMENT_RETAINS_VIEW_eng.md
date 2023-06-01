---
title: Fragment retains view
category: ""
order: 0
---

## 1. Vulnerability Description
* If the onDestroyView() method on Android does not nullify the View object in Fragment, the View object remains undestructed until the Fragment is resummed or destroyed.


## 2. Vulnerability Countermeasure
* View objects must be destroyed in the onDestroyView() method.

## 3. Sample Code
* Vulnerable Code

```java
@Override
    public void onDestroyView() {
    }
```

* Safe Code

```java
@Override
    public void onDestroyView() {
        super.onDestroyView();
    }
```
