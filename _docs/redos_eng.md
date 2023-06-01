---
title: ReDoS(regular expression denial of service) Vulnerability
category: ""
order: 0
---

## 1. Vulnerability Description
* DOS attack may occur by exploiting a vulnerability that takes a lot of time to analyze a specific string according to the definition of regular expression.

## 2. Vulnerability Countermeasure
* When using regular expressions, all input values need to be considered. By using the safe-regex package, you can check in advance whether the expression has a problem with DOS attack.

* safe-regex 
   * https://www.npmjs.com/package/safe-regex


## 3. Sample code
* Vulnerable Code
   * Assuming that there is a regex that checks for valid format as shown below, it takes 8 seconds to test as follows

```js
validateEmailFormat: function( string ) {
  var emailExpression = /^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/;

  return emailExpression.test( string );
}
```

```js
start = process.hrtime();
console.log(validateEmailFormat(""jjjjjjjjjjjjjjjjjjjjjjjjjjjj@ccccccccccccccccccccccccccccc.555555555555555555555555555555555555555555555555555555{""));
console.log(process.hrtime(start));

output>
false
[ 8, 487126563 ]
```


* Sample Code
   * Use safe-regex to check if it is safe

```js
var safe = require('safe-regex');
module.exports = function(context) {
  ""use strict"";

  return {
    ""Literal"": function(node) {
      var token = context.getTokens(node)[0],
          nodeType = token.type,
          nodeValue = token.value;

      if (nodeType === ""RegularExpression"") {
        if (!safe(nodeValue)) {
          context.report(node, ""Possible Unsafe Regular Expression"");
        }
      }
    }
  };
};
```
