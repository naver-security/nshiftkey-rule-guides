---
title: Server Side JS Injection
category: ""
order: 0
---

## 1. Vulnerability Description
* If the Web server does not validate the input values when using the functions eval(), setTimeout(), setInterval(), and Function() to process user input values, the server can execute malicious JavaScript code.

## 2. How to check vulnerability
* In the case of web servers that use the functions eval(), setTimeout(), setInterval(), and Function() and do not verify the input value, malicious behavior is possible by inserting the value below into the user input value.

### 2.1. DoS Aattack
* While (1) : DoS Attack
* process.exit() : process exit
* process.kill(process.pid) : Exit process

### 2.2. Accessing the File System
* In the case of vulnerable servers, attacker can list the contents of the current directory and the parent directory using the two commands below.

```
res.end(require('fs').readdirSync('.').toString())
res.end(require('fs').readdirSync('..').toString()) 
```

* Using the file name obtained with the command above, an attacker can check the actual contents of the command file below.

```
res.end(require('fs').readFileSync(filename))
```

* Attackers can also write and execute malicious binary files using fs and child_process modules.


## 3. Vulnerability Countermeasure
* Validate user input values before using them.
* Do not use the function eval(), setTimeout(), setInterval(), and Function() to parse user input values
* Use a safe alternative function such as JSON.parse() instead of an eval() function to parse JSON input values
* To activate strict mode by declaring "use strict" on the start of JavaScript or the start routine of a function
