---
title: Using weak cipher algorithms
category: ""
order: 0
---

## 1. Vulnerability Description
* If you use weak encryption algorithms that can not ensure the confidentiality of sensitive information (financial information, personal information, credentials, etc.), the information may be exposed.
* Vulnerable Encryption Algorithm
  * MD5
  * SHA-1
  * RC4
  * DES


## 2. Vulnerability Countermeasure
* Use the following secure encryption algorithm :
  * SHA-224
  * SHA-256
  * SHA-384
  * SHA-512


## 3. Sample Code
* Vulnerable Code

```JAVA
public String getCryptedPassword(String salt, String password) {
    return new MD5HashGenerator().getValue(password);
}
```

* Safe Code

```JAVA
public String getSalt(String userId, String password) {
    return SHA256HashGenerator.getInstance().getValue("--" + Calendar.getInstance().getTime().toString() + "--" + userId + "--");
}

public String getCryptedPassword(String salt, String password) {
    return SHA256HashGenerator.getInstance().getValue("nest--" + salt + "--" + password + "--");
}
```
