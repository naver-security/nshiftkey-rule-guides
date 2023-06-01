---
title: Insufficient HTTP security header 
category: ""
order: 0
---

## 1. Vulnerability Description
* Setting up HTTP security headers on a web server can add security headers to HTTP responses to improve security.
However, if the client-side browser does not support this option, it may not work.
Below is a description of each security header.

### X-Frame-Options
* Depending on the X-Frame-Options filter option, you can replace some of the problematic scripts with , #, or change the entire page's response to # characters to show you.
* Prevent malicious sites from creating malicious ActiveX installations or displaying specific areas by disguising them as arbitrary sites.

Option | Function
-- | --
DENY | You cannot include the page on any site
SAMEORIGIN | You can only include these pages in the same domain
Allow-From | You can only include these pages in the same domain, but different as browser setting

### HTTP Strict-Transport-Security(HSTS)
* Once you receive that header, your browser will allow your web browser to connect to https even if you don't attach "https:\/\/" the next time you access the site.
You can defend against SSL Strip attacks by applying HSTS security headers.
* If there is an HTTP request that an attacker inserted into MITM on a site using HTTPS, the HTTP request will not work on the site using that header.

Option | Function
-- | --
Max-age | The header will operate for that amount of time. Unit is seconds
includeSubdomain | Decide whether to include sub domains (optional settings)

### Content-Security-Policy
* Option to set the URL (trusted URL) in the header to allow the script.

### X-Content-Type-Options
* Header preventing the method of uploading js file with the jpg extension, bypassing it, and then src in the script tag.
Inserting the header prevents it from being used differently from the MIME TYPE. It is activated by inserting a noseniff.

### Cashe control
* Option to disable browser caching of webpage content because malicious users can exploit browser history.


## 2. How to check vulnerability
* **Check HTTP Responce header**
  * X-Frame-Options: DENY(Deny All)
  * X-Frame-Options: SAMEORIGIN(Allow only if same origin)
  * X-Frame-Options: ALLOW FROM https:\/\/sample.com(Allow only for specified origin)
  * Strict-Transport-Security: max-age=31536000; includeSubDomains: preload
  * Content-Security-Policy: script-src https:\/\/test.com
  * X-Content-Type-Options: nosniff
  * Cache-Control: no-cache


## 3. Vulnerability Countermeasure

### X-Frame-Options
#### Spring
````
<http>
    <headers>
        <frame-options policy="SAMEORIGIN" />
    </headers>
</http>
````

#### Apache
````
/* Allow only if same origin */
Header always set X-Frame-Options SAMEORIGIN
/* Deny All */
Header set X-Frame-Options DENY
/* Allow only for specified origin */
Header set X-Frame-Options "ALLOW-FROM https://example.com/"
````

#### Nginx
````
add_header X-Frame-Options SAMEORIGIN;
add_header X-Frame-Options DENY;
````

### HTTP Strict-Transport-Security(HSTS)
#### Spring
````
<http>
    <headers>
        <hsts include-subdomains="true" max-age-seconds="31536000" />
    </headers>
</http>
````

#### Apache
````
Header always set Strict-Transport-Security "max-age=15552000; preload"
````

#### Nginx
````
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
````
