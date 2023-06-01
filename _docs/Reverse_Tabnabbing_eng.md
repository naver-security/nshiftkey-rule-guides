---
title: Reverse Tabnabbing
category: ""
order: 0
---

## 1. Vulnerability Description
* When you click a link within an HTML document (a_blank Anchor tag) there is a vulnerability that allows you to steal information by changing the location of an existing document from a newly opened tab (or page) to a phishing site.

## 2. Vulnerability Countermeasure
* Use the keywords nooper and noferrer to prevent this vulnerability.
* An attacker can access window.opener and change the address of a cage to a malicious site. If the value indicated by window.opener is set to null using nooper and noferrer, the attacker cannot change it.

### HTML
* Grant the property rel="nooper noferrer" to the html link.
### JavaScript
```javascript
function openPopup(url, name, windowFeatures){
  //Open the popup and set the opener and referrer policy instruction
  var newWindow = window.open(url, name, 'noopener,noreferrer,' + windowFeatures);
  //Reset the opener link
  newWindow.opener = null;
}
```
### HTTP response
* Set the referrer-Policy: no-referrer in the HTTP response header.