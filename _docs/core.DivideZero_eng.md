---
title: Divide By Zero
category: ""
order: 0
---

## 1. Vulnerability Description
* Dividing a value by 0 can cause a crash.


## 2. Vulnerability Countermeasure
* Do not divide a value by 0


## 3. Sample Code
* Vulnerable Code

```c++
double divide(double x, double y){
  return x/y;
}
```

* Safe Code

```c++
const int DivideByZero = 10;
double divide(double x, double y) {
  if ( 0 == y ) {
     throw DivideByZero;
  }
  return x/y;
}
...
try {
  divide(10, 0);
} catch( int i ) {
  if(i==DivideByZero) {
     cerr<<""Divide by zero error"";
  }
}
```
