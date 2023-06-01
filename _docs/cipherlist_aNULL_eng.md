---
title: Weak Cryptographic Algorithm (cipherlist_aNULL)
category: ""
order: 0
---

## 1. Vulnerability Description
* aNULL is vulnerable to Man-In-The-Middle (MITM) attacks because there is no authentication feature in aNULL.

## 2. Vulnerability Countermeasure

#### When use apache
* Add the !aNULL option to SSLCipherSuite in the ssl.conf. 

#### When use nginx
* Add the !aNULL option to ssl_ciphers in the setting file.
