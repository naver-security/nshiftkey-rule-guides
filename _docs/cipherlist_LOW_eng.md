---
title: Weak Cryptographic Algorithm (cipherlist_LOW)
category: ""
order: 0
---

## 1. Vulnerability Description
* If weak encryption algorithms(RC5,RC6,MD5,SHA1,DES, etc.) are used, security vulnerabilities may occur.

## 2. Vulnerability Countermeasure

#### When use apache
* Add the !LOW option to SSLCipherSuite in the ssl.conf. 

#### When use nginx
* Add the !LOW option to ssl_ciphers in the setting file.
