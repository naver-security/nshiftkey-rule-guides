---
title: Vulnerable SSL/TLS Configuration (LOGJAM)
category: ""
order: 0
---

## 1. Vulnerability Description
* Logjam vulnerabilities can be exploited by launching MITM(man-in-the-middle) attack to downgrade vulnerable TLS connections to 512-bit export-grade encryption.
* An attacker can downgrade a connection and access any data that passes through that connection.

## 2. How to check vulnerability
* Check the OpenSSL library you are using.

## 3. Vulnerability Countermeasure
* Apply OpenSSL 1.0.2f, 1.0.1r version, or higher version of the library.
