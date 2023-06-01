---
title: Use of deprecated API
category: ""
order: 0
---

## 1. Vulnerability Description
* Using the deprecated API does not guarantee proper behavior.

## 2. How to check vulnerability
* Verify that you use bcmp, bcopy, bzero, getpw methods.

## 3. Vulnerability Countermeasure
* It is recommended to use the API as shown below.

deprecated | recommend |
-- | --|
bcmp | memcmp |
bcopy  | memcpy |
bzero | memset |
getpw | getpwuid |
