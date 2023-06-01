---
title: Use a weak CGI library
category: ""
order: 0
---

## 1. Vulnerability Description
* When using a CGI version that is vulnerable to attack, an attacker can manipulate the proxy header to attack MITM(Man-In-The-Mirror).

## 2. How to check vulnerability
* Check that your current version of Go is less than or equal to 1.6.3

## 3. Vulnerability Countermeasure
* Blocking a proxy header, or upgrading to version 1.6.3 or later.

## 4. Sample Code
* Examples of codes that might be affected

```go
cgi.Serve(
    http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        res, _ := http.Get(""http://api.internal/?secret=foo"")
        // [...]
```
