---
title: Vulnerable TLS configuration
category: ""
order: 0
---

## 1. Vulnerability Description
* TLS is currently 1.0, 1.1, 1.2, 1.3 (latest), with a total of four versions present. Older versions of TLS 1.0 and 1.1 are vulnerable to attacks such as POODLE and BEAST.

#### Vulnerabilities
* POODLE(Padding Oracle On Downgraded Legacy Encryption)
  * Vulnerabilities in Downgrading Protocols by exploiting outdated encryption algorithms
* BEAST(Browser Exploit Against SSL/TLS)
  * Vulnerabilities that can decrypt cookies in HTTPS and hijack sessions in a browser

## 2. How to check vulnerability
* Vulnerable if server certificate uses weak CipherSuites below

CipherSuite | Description
-- | --
ADH | No authentication
NULL | No encryption
Export Key exchange | Easily break
Weak cipher(40-56bits) | Easily break
3DES | support 108bits or 112bits only
RC4 | Some security issues exist (must be avoided as much as possible)


## 3. How to Prevent and Respond to Vulnerabilities
* Safe Cipher Suites
  * Starting in 2020, HTTPS will become inaccessible if the web server does not support TLS 1.2 and TLS 1.3.

Protocol | Recommendation | Description
-- | -- | --
SSL 2.0 | X | Must not be used
SSL 3.0 | X | Use is not recommended, but may need to be provided by IE 6 users
TLS 1.0 | X | End of Chrome, Firefox, IE, Edge, Safari browser support from 2020
TLS 1.1 | X | End of Chrome, Firefox, Edge, Safari browser support from 2020
TLS 1.2 | O | Recommend to use
TLS 1.3 | O | Recommend to use (August 2018 Standard Announcement)

*  Server private key length should be greater than 2048bit
* Private key protection
  * The private key must be stored safely.
  * After the certificate expires, you must discard the private key and generate a new key with the new certificate, and renew the server private key.
* Support for 'Forward Secrecy' protocol
* Disable unsafe renegotiation setting value
* Disable TLS compression setting value

### Reissue Server Private Key
* If the certificate key of the server providing SSL/TLS is less than RSA 2048 bits, you need to be reissued to RSA 2048 bits in accordance with the in-house SSL purchase application procedure.

### Setting up Ciphersuits in Apache
* Apache httpd 2.2 version has been End-of-Life since December 2017, making it difficult to respond to vulnerabilities. We recommend upgrading to the latest version (2.4.X) to respond to new vulnerabilities.
* You can add the following setting to the SSL Settings section of Apache in the httpd.conf file.
(Depending on server settings, other files may have SSL settings.)
After you set it up, you must restart Apache.

#### SSL CipherSuite Settings
* The SSL CipherSuite setting is most secure when set to Modern, but considering client compatibility, it may be set to the Intermediate level or the department in charge may need to make a decision. The encryption order below does not cause problems communicating with the client's web browser, but please check availability first if your service uses Server to Server communication internally over SSL/TLS.

#### Settings in Apache 2.2.26 and later (Intermediate)
* SSL security settings can be used by specifying the TLSv1.2 version, but compatibility issues can occur if the browser is not up-to-date with only setting TLSV1.2 because different versions of the browser support different versions. For this reason, you should consider your environment and the scope of service support when setting up SSL, and make the appropriate settings.

```
<httpd.conf> SSL Settings Part of the File

SSLEngine On
SSLProtocol all –SSLv2 –SSLv3 # If the service does not use SSL3.0, add '–SSLv3'.
SSLHonorCipherOrder on # Turn on ordering function for SSLCipher
SSLCipherSuite    ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS
```

#### Refer here for SSL CipherSuite (https://wiki.mozilla.org/Security/Server_Side_TLS)

Configuration | Oldest compatible client | SSL CipherSuite
-- | -- | --
Modern | Firefox 27, Chrome 30, IE 11 on Windows 7, Edge, Opera 17, Safari 9, Android 5.0, Java 8 | ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256
Intermediate | Firefox 1, Chrome 1, IE 7, Opera 5, Safari 1, Windows XP IE8, Android 2.3, Java 7 | ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS

* Reference Site:
  * https://mozilla.github.io/server-side-tls/ssl-config-generator
  * https://testssl.sh/openssl-rfc.mappping.html


### OpenSSL Upgrade
* OpenSSL is an open-source library with continuous security vulnerabilities.
* After you upgrade OpenSSL using the command(ex : "sudo yum update openssl"), you must restart the process.
* Reminder based on Apache version (Problem with Apache version and JDK version when using SSL)
  * If a client program using less than Java7 connects to Apache Httpd 2.2.31 with HTTPS, "Could not generate DH key pair" exception might occur. We recommend that you upgrade the Client Program to JDK8.

## Setup Results Test
* You can perform tests on servers that provide SSL/TLS on the QUALYS SSL LABS site.
* The results of the test must be at least 'B' and the Critical elements with 'F' rating (Oracle Padding, Heartbleed, FREAK, etc.) should be removed. Legacy servers (low Apache or less than 1.0.0 OpenSSL versions) should be patched according to plan.
  * URL: "https://www.ssllabs.com/ssltest/analyze.html?d=[test domain]&hideResults=on"
  * Examples: "https://www.ssllabs.com/ssltest/analyze.html?d=note.naver.com &hideResults=on"

* **The inspection result may be exposed to the outside when checking the setup result, so please check and test.**

### Reference Document
* https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices
* https://community.qualys.com/blogs/securitylabs/2013/06/25/ssl-labs-deploying-forward-secrecy
* https://community.qualys.com/blogs/securitylabs/2011/10/31/tls-renegotiation-and-denial-of-service-attacks
* https://community.qualys.com/blogs/securitylabs/2013/09/10/is-beast-still-a-threat
* https://mozilla.github.io/server-side-tls/ssl-config-generator/
* https://wiki.mozilla.org/Security/Server_Side_TLS
