---
title: Ignore GuardedBy Annotation
category: ""
order: 0
---

## 1. Vulnerability Description
* Accessing @GuardedBy annotated fields or methods without acquiring the specified lock can cause problems.

## 2. Vulnerability Countermeasure
* After the specified lock has been obtained, you must use the @GuardedBy annotated fields or methods.

## 3. Sample Code
* Vulnerable Code

```java
import com.google.errorprone.annotations.concurrent.GuardedBy;

class Account {
  @GuardedBy(""this"")
  private int balance;

  public synchronized int getBalance() {
    return balance; // OK: implicit 'this' lock is held.
  }

  public synchronized void withdraw(int amount) {
    setBalance(balance - amount); // OK: implicit 'this' lock is held.
  }

  public void deposit(int amount) {
    setBalance(balance + amount); // ERROR: access to 'balance' not guarded by 'this'.
  }

  @GuardedBy(""this"")
  private void setBalance(int newBalance) {
    checkState(newBalance >= 0, ""Balance cannot be negative."");
    balance = newBalance; // OK: 'this' must be held by caller of 'setBalance'.
  }
}
```


* Safe Code

```java
import com.google.errorprone.annotations.concurrent.GuardedBy;

class Account {
  @GuardedBy(""this"")
  private int balance;

  public synchronized int getBalance() {
    return balance; // OK: implicit 'this' lock is held.
  }

  public synchronized void withdraw(int amount) {
    setBalance(balance - amount); // OK: implicit 'this' lock is held.
  }

  public synchronized void deposit(int amount) {
    setBalance(balance + amount);
  }

  @GuardedBy(""this"")
  private void setBalance(int newBalance) {
    checkState(newBalance >= 0, ""Balance cannot be negative."");
    balance = newBalance; // OK: 'this' must be held by caller of 'setBalance'.
  }
}
```
