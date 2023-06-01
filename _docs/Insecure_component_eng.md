---
title: Use of Vulnerable Open Source
category: ""
order: 0
---

## 1. Vulnerability Description
* In general, open-source development and management involve a large number of developers, so code quality is perceived to be higher and more secure.
However, open source has a much larger number of security vulnerabilities than usual,
Yyou should pay attention to use of open source as it may increase security threats.

#### Threats from open source code
* The biggest reason for the many vulnerabilities in open source software (ex. GIT) is that the source code is exposed.
As the source code has been exposed, it is very easy for attackers to select targets and reverse engineering.
That's why we find more vulnerabilities on Android, whose source code is exposed compared to Apple's iOS.

#### Managed Security Threats
* Many developers participate in the open source community and the code is opened, so it's true that solutions such as security patches are available quickly. However, only if there are many community participants or if there is a technical support professional. Otherwise, the security becomes more vulnerable due to mismanagement.
In addition, even if the security patch is done quickly, it is vulnerable because the user does not manage the version systematically or the user does not apply the patch due to concerns about compatibility issues caused by the version change.


## 2. How to Prevent and Respond to Vulnerabilities
* Before applying open source, check security.
* Download open source codes only through famous code repositories such as Github and SourceForge, or through package installers such as PIP and Maven.
* Use NVD(National Vulnerability Database) to determine if there is a vulnerable open source.

