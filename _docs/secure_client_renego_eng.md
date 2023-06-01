---
title: Insufficient renegotiation restrictions
category: ""
order: 0
---

## 1. Vulnerability Description
* When performing secure communication, insufficient renegotiation restrictions may allow an attacker to cause DoS attacks.

## 2. How to check vulnerability
* You can check this vulnerability using the OpenSSL binary.
<pre>
$ openssl s_client -connect www.example.com:443
</pre>
* If you enter the above command --- appears and you see it's paused, and you can try to renegotiate it by entering the upper case R.
* At that time, if an error occurs and no action occurs, it is not vulnerable.
![image](https://github.com/naver-security/nshiftkey-rule-guides/assets/133747927/bdc3ddd7-6e63-43b1-9062-7297c1fd3659)
* If RENEGOTIATING is successful, there has the vulnerability.
![image](https://github.com/naver-security/nshiftkey-rule-guides/assets/133747927/641d166a-6149-481b-a378-de568a0b1574))

## 3.  Vulnerability Countermeasure
* It is recommended to upgrade to the latest OpenSSL version.
   * (Recommend OpenSSL version 0.9.8m or higher.)
