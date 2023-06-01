---
title: Buffer overflow
category: ""
order: 0
---

## 1. Vulnerability Description
* This is a vulnerability in a program that operates incorrectly due to an error in handling memory. The buffer overflow occurs in various forms, usually caused by recording data larger than the declared size.
* When buffer overflow occurs, adjacent memory is overwritten, and it can cause memory access errors, program shutdowns, or system information disclosure, resulting in security vulnerabilities.

## 2. How to check vulnerability
* Pass a large number of arguments to the parameter input value to see if an error page occurs.
* Pass many strings to the ID/PW field of the login window
* Pass many strings to the membership registration and edit page
* Pass many strings to site search field
* Enter more strings than allowed when writing a post
* Pass many argument values to the Web application

## 3. Vulnerability Countermeasure
* Check the range before setting the parameter type.
* Verify the range of external parameter input values entered in the variable to ensure that the error page is not returned if the input value is outside the acceptable range.
