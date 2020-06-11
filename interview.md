# Interview

## Topics

### SQL injection

* SQL injection is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database
* Injection attacks stem from a lack of strict separation between program instructions \(i.e., code\) and user-provided \(or external\) input. This allows an attacker to inject malicious code into a data snippet.

  _SQL injection_ is one of the most common types of injection attack. To carry it out, an attacker provides malicious SQL statements through the application.

  How to prevent:

  * **Prepared statements with parameterized queries**
  * **Stored procedures**
  * **Input validation** - blacklist validation and whitelist validation
  * **Principle of least privilege** - Application accounts shouldn’t assign DBA or admin type access onto the database server. This ensures that if an application is compromised, an attacker won’t have the rights to the database through the compromised application.

* [https://portswigger.net/web-security/sql-injection\#retrieving-hidden-data](https://portswigger.net/web-security/sql-injection#retrieving-hidden-data)

### Webpack

**Webpack** is a build tool that puts all of your assets, including Javascript, images, fonts, and CSS, in a dependency graph. Webpack lets you use `require()` in your source code to point to local files, like images, and decide how they're processed in your final Javascript bundle, like replacing the path with a URL pointing to a CDN.

If you're building a complex Front End application with many **non-code static assets** such as CSS, images, fonts, etc, then yes, Webpack will give you great benefits.

If your application is fairly small, and you don't have many static assets and you only need to build one Javascript file to serve to the client, then Webpack might be more overhead than you need.

### **strict mode**

### **What is Cross-Site Scripting \(XSS\)?**

### API design

* Platform Independent
* Consistent, robust, efficient, secure, easy to scale
* Naming

### HTTP/HTTPS

### REST

* is a [software architectural](https://en.wikipedia.org/wiki/Software_architecture) style that defines a set of constraints to be used for creating [Web services](https://en.wikipedia.org/wiki/Web_service). Web services that conform to the REST architectural style, called RESTful Web services. RESTful Web services allow the requesting systems to access and manipulate textual representations of [Web resources](https://en.wikipedia.org/wiki/Web_resource) by using a uniform and predefined set of [stateless](https://en.wikipedia.org/wiki/Stateless_protocol) operations
* [https://restfulapi.net/](https://restfulapi.net/)

### SOAP

* messaging [protocol](https://en.wikipedia.org/wiki/Protocol_%28computing%29) specification for exchanging structured information in the implementation of [web services](https://en.wikipedia.org/wiki/Web_service) in [computer networks](https://en.wikipedia.org/wiki/Computer_network)

