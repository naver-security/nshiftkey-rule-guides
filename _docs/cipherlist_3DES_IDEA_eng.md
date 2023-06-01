---
title: Weak Cryptographic Algorithm (cipherlist_3DES_IDEA)
category: ""
order: 0
---

## 1. Vulnerability Description
* Triple DES algorithm is vulnerable to security, and there is a possibility that an attacker can decrypt the ciphertext.

## 2. Vulnerability Countermeasure

#### When use apache
* Add the !3DES option to SSLCipherSuite in the ssl.conf.

#### When use nginx
* Add the !3DES option to ssl_ciphers in the setting file.
