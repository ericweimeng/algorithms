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

