---
title: CCS
category: ""
order: 0
---

## 1. Vulnerability Description
* Man-in-The-Middle Attack on encrypted connections can be executed.
* The ChangeCipherSpec (CCS) message informs the other party that they will use the encryption specifications that have been discussed in advance between the server and client.
  * It is normal for CCS messages to be sent and received by clients and servers during handshaking before sending Finish messages.
  * However, receiving CCS messages before sending and receiving cryptographic information creates a vulnerable cryptographic key, which can be easily inferred by an attacker.

## 2. How to check vulnerability
* Check that you are using the openssl version below.
<pre>
all versions before OpenSSL 0.9.8y
OpenSSL 1.0.0 through 1.0.0l
OpenSSL 1.0.1 through 1.0.1g
</pre>

## 3. Vulnerability Countermeasure
* Users of the affected version of the vulnerability update to the version below.
<pre>
OpenSSL 0.9.8 : update to 0.9.8za version
OpenSSL 1.0.0 : update to 1.0.0m version
OpenSSL 1.0.1 : update to 1.0.1h version
</pre>
