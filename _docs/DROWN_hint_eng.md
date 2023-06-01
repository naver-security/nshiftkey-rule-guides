---
title: Vulnerable SSL/TLS settting (DROWN)
category: ""
order: 0
---

## 1. Vulnerability Description
* DROWN attack decrypts HTTPS connection by sending malicious packet specially designed by attacker to server, or MITM attack can be executed if certificate is shared with other server

## 2. How to check vulnerability
* Check the usage component version.

#### Apache
* Any version other than 2.4.x

#### Nginx
* 0.7.64, 0.8.18, and earlier versions

#### Postfix
* 2.9.14, 2.10.8, 2.11.6, 3.0.2, and earlier versions

#### OpenSSL
* 1.0.2a, 1.0.1m, 1.0.0r, 0.9.8zf, and earlier versions

## 3. Vulnerability Countermeasure

### OpenSSL
* Upgrade OpenSSL to latest version
* How to upgrade
<pre>
- In case of CentOS, Redhat
# yum clean
# yum update openssl

- In case of Ubuntu
# apt-get upgrade openssl
</pre>

#### IIS / NSS 
* Disable SSLv2.

#### Apache
* Disable SSLv2.
* Change the Apache configuration file (httpd.conf)
<pre>
# vi httpd.conf

......
SSLProtocol -all +TLSv1.2

SSLCipherSuite HIGH:!aNULL:!MD5:!SSLv2:!SSLv3:!TLSv1
......
# service httpd restart
</pre>

#### Nginx
* Disable SSLv2.
<pre>
ssl_protocols TLSv1.2;
</pre>
* Restart nginx

## 4. Reference
### SSL/TLS usage recommendations (as of December 2019)

![image](../images/DROWN/1_eng.png)
