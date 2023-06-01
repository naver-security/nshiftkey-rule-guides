---
title: Cookie Poisoning
category: ""
order: 0
---


## 1. Vulnerability Description
* Cookie Poisoning is a vulnerability that can be disguised and elevated by other users through cookie value modulation, such as cookie injection, using improperly protected cookies.<br>
Cookies contain various information, including session information of users using the website. If used without proper cookie verification, malicious actions such as gaining unauthorized access to another user's valid session by manipulating the cookie value can be performed.<br>
Furthermore, if cookies are compromised, sensitive information stored internally may be exposed to an attacker."

## 2. How to check vulnerability
#### Make sure the cookie contains important status information and features
* Ensure that sensitive status information, authentication, or information used to determine permissions should not be sent in cookies and that information is encrypted and sent if it is inevitably sent.<br>
If you are using cookies as a factor in a function that performs a critical function, perform a verification of the input values and verify that they are being used on a limited basis.

#### Perform validation
* Ensure that the client is performing a verification of the information passed in.<br>
Filter the client input values and verify that the server logic is performing validation.

## 3. Vulnerability Countermeasure
#### Using Session
* We recommend using sessions rather than cookies because session-based is relatively safe from attacks.<br>
Set the time to destroy sessions on the server and ensure that all pages that require authentication are authenticated on the server side.

#### When inevitable, use encryption
* When setting up cookies, sensitive information should not be sent in plain language, and cookies cannot be added or changed on the client side.<br>
Information used for critical status information, authentication or authorization decisions shoule not be sent to cookies and, if necessary, be encrypted and sent.

#### Using Secure Cookie
* Option that Web browser sends cookies to the server only if the web browser and the web server communicate with HTTPS.

##### How to Set Secure Options
* Java 6 or later, Servlet 3.0 supported
* Settings in WEB-INF/web.xml

```xml
<session-config>
	<cookie-config>
		<secure>true</secure>
	</cookie-config>
</session-config>
```

* PHP

```PHP
session.cookie_secure = True
```

## 4. Sample Code
* The code below uses the value assigned to the role of the cookie in the user's web browser when setting the user's permissions. If this value is changed by the user, the user's role value may be assigned an unintended value.

* Vulnerable  Code

```java
public void CookieFile(HttpRequest request, HttpResponse response)
{
    HttpCookieCollection cookies = request.Cookies;
    for(int i = 0; i < cookies.Count; i++)
    {
        HttpCookie c = cookies[i];
        if(c.Name.Equals(""role""))
        {
            userRole = c.Value;
        }
    }
}
```

* As the code below shows, values used to determine security, such as user rights, authentication, etc., do not use user input values but utilize internal session values.
* Safe Code

```java
if (!IsPostBack &&(Request.Cookies[""__LOGINCOOKIE__""] == null || Request.Cookies[""__LOGINCOOKIE__""].Value == """"))
{
    Session.Abandon();
    Response.Cookies.Add(new HttpCookie(""ASP.NET_SessionId"", """"));
 
    AddRedirCookie();
    Response.Redirect(Request.Path);
}
```
