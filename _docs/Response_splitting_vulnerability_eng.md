---
title: CRLF (HTTP Response Splitting)
category: ""
order: 0
---

## 1. Vulnerability Description
* When parameters in HTTP Request are passed back to the response header of HTTP Response, the HTTP response header is detached when the opening character CR (%0D) or LF (%0A) within the parameter is present.
* An attacker can manipulate the response header value using the opening character (%0D %0A) if the parameter does not validate the user's input value.
* HTTP Response Splitting attacks can be exploited to compromise XSS attacks and cache by injecting malicious code into response messages.

![](../images/CRLF (HTTP Response Splitting)/1_eng.png)
[picture 1. CRLF Vulnerability]


## 2. How to check vulnerability
* Insert the opening character (%0D %0A) into the parameter to verify that the HTTP response is detached.

![](../images/CRLF (HTTP Response Splitting)/2_eng.png)
[picture 2. Example of vulnerability checking]


## 3. Vulnerability Countermeasure
* Do not insert user-entered values into HTTP headers returned from the application.
* If you are forced to insert the user-entered value into the HTTP header, validate the value entered in the HTTP response header.
If an external input value is inserted in the response header, such as setting the Cookie value, setting the response header value, or inserting location information to re-direct the page, the character CR (%0D) or LF (%0A) that can cause HTTP response segmentation must be filtered.

## 4. Sample Code
* The example below sets the value of the cookie returned using an external input value.
However, if an attacker sets "Hacker\r\nHTTP/1.1 200 OK\r\n" to the value of the authorName,
Two unintended pages are delivered, as shown in the following example. In addition, the second response page can be modified at the discretion of the attacker.
  * (ex: HTTP/1.1 200 OK...Set-Cookie: author=Hacker HTTP/1.1 200 OK ...)

* Vulnerable Code

```JAVA
throws IOException, ServletException
{
    response.setContentType("text/html");
    String author = request.getParameter("authorName");Cookie cookie = new Cookie("replidedAuthor", author);
    cookie.setMaxAge(1000);
    response.addCookie(cookie);
    RequestDispatcher frd = request.getRequestDispatcher("cookieTest.jsp");
    frd.forward(request, response);
}
```

* The example below checks for NULL for externally entered values and removes the opening characters \r and \r using "replaceAll" to prevent the header values from being divided.

* Safe Code

```JAVA
throws IOException, ServletException
{
    response.setContentType("text/html");
    String author = request.getParameter("authorName");
    if (author == null || "".equals(author)) return;
    String filtered_author = author.replaceAll("\r", "").replaceAll("\n", "");
    Cookie cookie = new Cookie("replidedAuthor", filtered_author);
    cookie.setMaxAge(1000);
    cookie.setSecure(true);
    response.addCookie(cookie);
    RequestDispatcher frd = request.getRequestDispatcher("cookieTest.jsp");
    frd.forward(request, response);
}
```
