---
title: Declare empty collection explicitly
category: ""
order: 0
---

## 1. Vulnerability Description
* When defining an empty collection, it is better performance to declare it explicitly.


## 2. Vulnerability Countermeasure
* Most immutable collections implement empty as a singleton.
* If you explicitly create a collection using empty, you can reuse empty to reduce the use of heap space, and there is an advantage in operation performance as there is no runtime length check.

## 3. Sample Code
* Before

```SCALA
Map[K,V]()
Seq[T]()
Set[T]()

```

* After

```SCALA
Map.empty[K,V]
Seq.empty[T]
Set.empty[T]
```
