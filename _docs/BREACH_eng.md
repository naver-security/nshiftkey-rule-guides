---
title: BREACH
category: ""
order: 0
---

## 1. Vulnerability Description
* BREACH(Browser Reconnaissance & Exfiltration via Adaptive Compression of Hypertext)
* If the input given by an attacker appears in the response of http, the attacker can change the input and size the http response to predict the string in the response.
* Attackers can repeatedly guess and extract plaintext confidential information from the SSL stream by inserting plaintext into HTTPS requests and observing the length of compressed HTTPS responses.

## 2. Vulnerability Countermeasure
* Because this attack is attempted through user input, a restriction on user input is required.
* Disables HTTP compression. (This can lead to poor performance and increased bandwidth usage.)
* A separation of user input and confidential information or a speed limit of requests to the server is required.
* Continuous monitoring of inputs is required.
