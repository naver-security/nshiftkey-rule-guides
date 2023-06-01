---
title: Weak Cryptographic Hash
category: ""
order: 0
---

## 1.Vulnerability Description
* Information (Financial information, personal information, authentication information, etc..) can be exposed when using weak encryption algorithms that cannot ensure confidentiality.
* Weak cryptographic hash algorithm
  * MD5
  * SHA-1
  * RC4
  * DES


## 2. Vulnerability Countermeasure
* Use a secure encryption algorithm as shown below.
  * SHA-224
  * SHA-256
  * SHA-384
  * SHA-512


## 3. Sample Code
* Vulnerable Java Code

```JAVA
public String getCryptedPassword(String salt, String password) {
    return new MD5HashGenerator().getValue(password);
}
```

* Safe Java Code

```JAVA
public String getSalt(String userId, String password) {
    return SHA256HashGenerator.getInstance().getValue("--" + Calendar.getInstance().getTime().toString() + "--" + userId + "--");
}

public String getCryptedPassword(String salt, String password) {
    return SHA256HashGenerator.getInstance().getValue("nest--" + salt + "--" + password + "--");
}
```