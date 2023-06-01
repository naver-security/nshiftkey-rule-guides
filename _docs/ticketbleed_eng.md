---
title: Ticketbleed
category: ""
order: 0
---

## 1. Vulnerability Description
* Ticketbleed is a software vulnerability in the TLS/SSL stack of F5 BIG-IP appliances allowing a remote attacker to extract up to 31 bytes of uninitialized memory at a time.

## 2. How to check vulnerability
* You can check with the script in the link below.
   * [link](https://gist.github.com/FiloSottile/fc7822b1f5b475a25e58d77d1b394860)
* The full list of affected versions is available on the F5 website. 
   * [link](https://support.f5.com/csp/article/K05121675)

## 3. Vulnerability Countermeasure
* You should upgrade to a version that is not vulnerable.
* Disabling Session Tickets is a complete mitigation.
   * How to disable:
<pre>
(1) Log in to the Configuration utility
(2) Navigate on the menu to Local Traffic > Profiles > SSL > Client
(3) Toggle the option for Configuration from Basic to Advanced
(4) Uncheck the Session Ticket option to disable the feature
(5) Click Update to save the changes
</pre>
