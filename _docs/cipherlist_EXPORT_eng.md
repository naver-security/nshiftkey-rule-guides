---
title: Weak Cryptographic Algorithm (cipherlist_EXPORT)
category: ""
order: 0
---

## 1. Vulnerability Description
* Under U.S. export laws, encryption algorithms with encryption keys less than 56bit in length can be vulnerable to security.

## 2. Vulnerability Countermeasure

#### When use apache
* Add the !EXPORT option to SSLCipherSuite in the ssl.conf.

#### When use nginx
* Add the !EXPORT option to ssl_ciphers in the setting file.