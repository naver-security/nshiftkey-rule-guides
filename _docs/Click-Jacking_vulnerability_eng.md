---
title: HTTP security header insufficient
category: ""
order: 0
---

## 1. Vulnerability Description
* Setting up HTTP security headers on a web server can increase security by adding them to HTTP responses.
However, if the client-side browser does not support this option, it may not work.
Below is a description of each security header.

#### X-Frame-Options
* Depending on the X-Frame-Options filter option, some of the problematic scripts can be replaced with , #, or the responses on the entire page can be changed to # characters to show.
* Prevent malicious sites from disguising themselves as arbitrary sites to induce users to install malicious ActiveX or display specific areas.

Option | Function
-- | --
DENY | Cannot contain the page at any site
SAMEORIGIN | Can only contain pages in the same domain
Allow-From | The page can only be included in a defined domain.   Different browsers have different support

#### HTTP Strict-Transport-Security(HSTS)
* When browser receive that header, your browser will be able to connect to https without attaching "https:\/\/" the next time you access the site.
You can defend against SSL Strip attacks by applying HSTS security headers.
* If there is an HTTP request inserted using MITM by an attacker on a site using HTTPS, the HTTP request will not work on the site using that header.

Option | Function
-- | --
Max-age | The header will operate at that time. (unit : seconds)
includeSubdomain | Determine if subdomain is included (optional setting)

#### Content-Security-Policy
* Option to set the URL (trusted URL) in the header to allow the script.

#### X-Content-Type-Options
* Header to prevent typing as "src" of a script tag after raising the js file with the jpg extension and bypassing it,
Inserting the header prevents it from being used differently from the MIME TYPE. It is activated by inserting a "noseniff".

#### Cashe control
* Option to disable browser caching of web page content because malicious users can exploit browser history.

## 2. How to check vulnerability
* **Check HTTP Responce header**
  * X-Frame-Options: DENY(Deny Show All)
  * X-Frame-Options: SAMEORIGIN(Allow only if same origin)
  * X-Frame-Options: ALLOW FROM https:\/\/sample.com(Allow only for specified origin)
  * Strict-Transport-Security: max-age=31536000; includeSubDomains: preload
  * Content-Security-Policy: script-src https:\/\/test.com
  * X-Content-Type-Options: nosniff
  * Cache-Control: no-cache


## 3. Vulnerability Countermeasure

### X-Frame-Options
#### Spring setting
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
/* Deny Show All */
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
#### Spring setting
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
