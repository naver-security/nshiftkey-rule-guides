---
title: Potential Command Injection using exec()
category: ""
order: 0
---

## 1. Vulnerability Description
* If the input value is insufficient when using child_process.exec() in Nodejs, an attacker may perform arbitrary code.
* In particular, exec() does not directly execute a process, but passes execution arguments to /bin/sh and delegates execution, so command injection through the shell is possible.

## 2. Vulnerability Countermeasure
* Steps are required to verify that the parameters are secure, and we recommend using execFile() or spawn() instead of exec().
* execFile() and spawn() perform the process directly, unlike exec().

## 3. Sample Code
* Vulnerable Code

```js
var path = ""user input"";
child_process.exec('ls -l ' + path, function (err, data) {
  console.log(data);
});
```


* Safe Code

```js
var child_process = require('child_process');

var path = "".""
child_process.execFile('/bin/ls', ['-l', path], function (err, result) {
  console.log(result)
});
```
