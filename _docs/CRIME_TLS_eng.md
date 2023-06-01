---
title: CRIME 
category: ""
order: 0
---

## 1. Vulnerability Description
CRIME(Compression Ratio Info-leak Made Easy) is an attack that takes advantage of vulnerabilities in how data is compressed and encrypted to uncover confidential information about encrypted data. 
An attacker can replicate this attack to decrypt data and restore cookie data from an HTTP session.

## 2. Vulnerability Countermeasure
* Disable SSL compression in the server configuration and make sure that it is disabled (not to be confused with HTTP compression)
* If SSL compression is enabled in the server configuration, disable it (do not confuse with "HTTP compression")

### Countermeasures by Component
#### How to change the mod_ssl setting in Apache 2.4
* Set the SSLCompression flag as follows:
<pre>
SSLCompression off
</pre>

#### How to change the mod_gnutls setting in Apache
* In mod_gnutls, set as follows:
<pre>
GnuTLSPriorities flag = “!COMP-DEFLATE""
</pre>

#### IIS
* Microsoft IIS does not support SSL Compression. (Included IIS 7.5/Server 2008 R2)
