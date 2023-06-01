---
title: Use weak SSL/TLS block password
category: ""
order: 0
---

## 1. Vulnerability Description
* SWEET32 vulnerability is a vulnerability that can cause collision in a specific setting environment during block ciphers SSL/TLS.
* If CBC mode is used among the existing 64bit block ciphers, collision may occur.
* All SSL/TLS protocols that support 3DES symmetric cipher suites (eg ECDHE-RSA-DES-CBC3-SHA) may be affected by this vulnerability.

## 2. How to check vulnerability
* Verify that the server allows 3DES or blowfish.

<pre>
$ openssl s_client -cipher 3DES -connect example.com:443
</pre>


## 3. Vulnerability Countermeasure
* Please stop using DES and 3DES in the TLS protocol.
* For Apache, open the httpd.conf file stored in the Apache Server Tasks folder.

<pre>
"SSLCipherSuite ALL:!3DES:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL"
To prohibit the use of 3DES cipher suites considered vulnerable in the above string, remove 3DES:! from the string.

after editing 
"SSLCipherSuite ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL"
</pre>
