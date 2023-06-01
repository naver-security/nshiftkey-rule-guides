---
title: Deadlock
category: ""
order: 0
---


## 1. Vulnerability Description
* Deadlock may occur when two or more threads occupy each other's lock and wait until the lock is released.

## 2. Vulnerability Countermeasure
* Make sure that different threads do not occupy each other's locks and minimize the use of locks. <br>
If the threads inevitably have to occupy each other's lock, the critical section should be minimized, lock timeout should be set, or the priority of the lock should be clearly set.

## 4. Sample Code
* Vulnerable Code
   * If instances of the following types are called at the same time, a deadlock may occur:

```java
  public void lockAThenB() {
    synchronized(lockA) {
      synchronized(lockB) {
       // do something with both resources
      }
    }
  }

  public void lockBThenA() {
    synchronized(lockB) {
      synchronized(lockA) {
       // do something with both resources
      }
    }
  }
```
