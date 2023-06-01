---
title: SSL/TLS fallback attack
category: ""
order: 0
---

## 1. Vulnerability Description
* When SSL/TLS protocol negotiation fails, it attempts to negotiate using a lower version of the protocol. 
The use of lower protocols leads to security compromise and allows attackers to steal or do packet tampering.

## 2. How to check vulnerability
* You can check if it has a vulnerability with the command below.
<pre>
$ openssl s_client -connect www.example.com:443 -fallback_scsv -no_tls1_2

If not vulnerable, not connected with the message alert initial fallback.
$ openssl s_client -connect www.google.com:443 -fallback_scsv -no_tls1_2
140735103538016:error:1407743E:SSL routines:SSL23_GET_SERVER_HELLO:tlsv1 alert inappropriate fallback:s23_clnt.c:770:

If vulnerable, connect successful
$ openssl s_client -connect www.example.com:443 -fallback_scsv -no_tls1_2
CONNECTED(00000003)
...
SSL-Session:
Protocol  : TLSv1.1
Cipher    : ECDHE-RSA-AES128-SHA 
</pre>

## 3. Vulnerability Countermeasure
* Use TLSv1.3 or later, or use the latest OpenSSL version.
<pre>
OpenSSL 1.0.1 users should upgrade to 1.0.1j.
OpenSSL 1.0.0 users should upgrade to 1.0.0o.
OpenSSL 0.9.8 users should upgrade to 0.9.8zc.
</pre>
* Use SSL_MODE_SEND_FALLBACK_SCSV extension of OpenSSL
* Example of setting SSL_MODE_SEND_FALLBACK_SCSV
<pre>
const SSL_METHOD* method = TLSv1_2_method();
if(method == NULL)) handleFailure();

SSL_CTX* ctx = SSL_CTX_new(method);
if(ctx == NULL) handleFailure();

#ifdef SSL_MODE_SEND_FALLBACK_SCSV
    SSL_CTX_set_mode(ctx, SSL_MODE_SEND_FALLBACK_SCSV)
#endif
</pre>
