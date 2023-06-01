---
title: CORS (Cross Origin Resource Sharing)
category: ""
order: 0
---

## 1. Vulnerability Description
* In order to save development costs and time lately, many sites have been developed to import content or data from information-providing sites and reuse them to create services.
However, web browsers enforce the Same Origin Policy (SOP), which restricts JavaScript from accessing other domains, making it challenging to develop these types of services..<br>
To overcome this limitation, browsers often utilize CORS (Cross-Origin Resource Sharing), a feature that enables cross-origin requests using XHR (XMLHttpRequest).<br>
CORS allows the sharing of resources between different domains (web servers), which can be configured through the 'Access-Control-Allow-Origin: domain' header during server setup.<br>
However, the use of CORS can introduce additional vulnerabilities, such as exposing the victim's cookies and enabling Cross-Site Request Forgery (CSRF) attacks, if proper permission requests are not implemented when accessing other domains.<br>
If we examine the scenario, the vulnerability is demonstrated as follows:<br>

![](../images/CORS (Cross Origin Resource Sharing)/1_eng.png)
 [ picture 1. Attack Scenario]

#### (1) An attacker attempts to exploit a CSRF vulnerability in the target server to steal victim privacy, but the server is not vulnerable to XSS and CSRF.
In addition, all attempts are blocked by a web firewall.
However, the target server verifies that there is a trust relationship for a particular Web server (vulnerable) and CORS.

##### (2) An attacker uploads a file containing malicious scripts to a specific Web server.
The victim server then uploads a post that links files that are uploaded to a specific web server.

##### (3) Victims access the victim's server, perform logins, and click on the link to the post that the attacker uploaded in (2) (the link contains the content that induces the click).
The user's Web Browser tab will run after importing a malicious script uploaded to a specific Web server (HTML5 Server).


#### (4) The victim's web browser exposed to malicious scripts sends his personal information to the attacker.
In fact, the vulnerable web server B server was responsible for generating the traffic that captured the victim's personal information through CSRF. This attack was possible because there was a trust relationship between the B server (vulnerable web server) and the A server (safe server) (Access-Control-Allow-Origin: www.B.com)


## 2. How to identify vulnerabilities
* Request GET with random URL in Origin

```
GET /test/test HTTP/1.1

Host: test.naver.com
...omission...
Origin: http://attacker.com
...omission...
```

* Vulnerable if response is as follows for any Origin request:
Access-Control-Allow-Origin: arbitrarily inserted URL

![](../images/CORS (Cross Origin Resource Sharing)/2_eng.png)


## 3. How to Prevent and Respond to Vulnerabilities
* Do not use code patterns such as "Access-Control-Allow-Origin : \*" or "Access-Control-Allow-Credentials : true".
Instead of using Asterisk (*) meaning you trust all if you need CORS functions, specify and use the WhiteList site to allow only the specified Origin.


## 4. Sample Code
#### Using Default Interceptor filter
* SimpleCORSFilter.java

```java
package com.company.project.util.domain;
  
import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletResponse;
import org.springframework.stereotype.Component;
  
@Component
public class SimpleCORSFilter implements Filter {
  
    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
        HttpServletResponse response = (HttpServletResponse) res;
 
        response.setHeader(""Access-Control-Allow-Methods"", ""POST, GET, OPTIONS, DELETE"");
        response.setHeader(""Access-Control-Max-Age"", ""3600"");
        response.setHeader(""Access-Control-Allow-Headers"", ""x-requested-with"");
         
        response.setHeader(""Access-Control-Allow-Origin"", ""http://domain1.com"");
        response.setHeader(""Access-Control-Allow-Origin"", ""http://domain2.com"");
      
 
        chain.doFilter(req, res);
    }
    public void init(FilterConfig filterConfig) {}
    public void destroy() {}
}
```

#### Apache Settings
* Apache(.htaccess)

```
Header set Access-Control-Allow-Origin ""http://domain1.com""
```


#### web.xml Settings
* web.xml

```xml
<filter>
    <filter-name>CORS</filter-name>
    <filter-class>com.thetransactioncompany.cors.CORSFilter</filter-class>
    <init-param>
        <param-name>cors.allowOrigin</param-name>
        <param-value>http://domain1.com</param-value>
    </init-param>
</filter>
```

#### Nginx Settings
* conf/nginx.conf

```js
set $cors '';
if ($http_origin ~ '^https?://(localhost|www\.yourdomain\.com|www\.yourotherdomain\.com)') {
        set $cors 'true';
}
 
if ($cors = 'true') {
        add_header 'Access-Control-Allow-Origin' ""$http_origin"" always;
        add_header 'Access-Control-Allow-Credentials' 'true' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
        add_header 'Access-Control-Allow-Headers' 'Accept,Authorization,Cache-Control,Content-Type,DNT,If-Modified-Since,Keep-Alive,Origin,User-Agent,X-Requested-With' always;
        # required to be able to read Authorization header in frontend
        #add_header 'Access-Control-Expose-Headers' 'Authorization' always;
}
```

#### Spring
* (1) Setting the CORS on the Controller Method
  * Specify a trusted site for origin. (Add using , in multiple cases)

```java
* Setting CORS in Controller Method

@CrossOrigin(origins = ""http://domain1.com, http://domain2.com"")
@RestController
@RequestMapping(""/account"")
public class AccountController {
 
    @RequestMapping(""/{id}"")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }
 
    @RequestMapping(method = RequestMethod.DELETE, value = ""/{id}"")
    public void remove(@PathVariable Long id) {
        // ...
    }
}
```

* (2) Setting up global CORS through java config
  * Specify a trusted site for .allowOrigins (add using , in multiple cases)

```java
* java config

@Configuration
@EnableWebMvc
public class WebConfig extends WebMvcConfigurerAdapter {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping(""/api/**"")
            .allowedOrigins(""http://domain2.com"")
            .allowedMethods(""PUT"", ""DELETE"")
            .allowedHeaders(""header1"", ""header2"", ""header3"")
            .exposedHeaders(""header1"", ""header2"")
            .allowCredentials(false).maxAge(3600);
    }
}

```

* (3) Setting CORS to mvc XML Namespace
  * Specify a trusted site for allowed-origins. (add using , in multiple cases)

```xml
* xml namespace

<mvc:cors>
    <mvc:mapping path=""/api/**""
        allowed-origins=""http://domain1.com, http://domain2.com""
        allowed-methods=""GET, PUT""
        allowed-headers=""header1, header2, header3""
        exposed-headers=""header1, header2"" allow-credentials=""false""
        max-age=""123"" />
  
    <mvc:mapping path=""/resources/**""
        allowed-origins=""http://domain1.com"" />
</mvc:cors>
```
