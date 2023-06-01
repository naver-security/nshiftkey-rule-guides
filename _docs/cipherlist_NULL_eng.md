---
title: Weak Cryptographic Algorithm (NULL)
category: ""
order: 0
---

## 1. Vulnerability Description
* Encryption results using Null Cipher are the same as the plaintext, so it is inappropriate to use them for real environment.

## 2. Vulnerability Countermeasure

#### When use apache
* Add the !NULL option to SSLCipherSuite in the ssl.conf. 

#### When use nginx
* Add the !NULL option to ssl_ciphers in the setting file.