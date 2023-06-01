---
title: Loosely Scoped Cookie
category: ""
order: 0
---

## 1. Vulnerability Description
* If Cookie's scope is not Fully Qualified Domain Name, attacker can use this cookie to connect to other domains, such as subdomain.
* An attacker can gain access to pages in the subdomain group by taking one cookie from anywhere.

## 2. Vulnerability Countermeasure
* Cookie scope must be set to Fully Qualified Domain Name.
* If there is a subdomain that is not in use, you must delete it.
* Cookie must always set the HttpOnly and Secure properties.
* Make sure that the validity period of the cookie is not set too long.
