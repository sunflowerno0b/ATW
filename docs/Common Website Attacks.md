## Intro 
Hosting a site that has tons of users at any given moment will undoubtably be tested by curious , malicious individuals. Web security is not something I am the most versed on but below are some notes I gathered. 

## Attack Types
### Cross Site Scripting
Cross-site scripting (XSS) is an exploit where the attacker attaches code onto a legitimate website that will execute when the victim loads the website. That malicious code can be inserted in several ways. Most popularly, it is either added to the end of a url or posted directly onto a page that displays user-generated content. In more technical terms, cross-site scripting is a client-side code injection attack.

#### Client Side Code
I will have to investigate this a bit further but client-side code is Javascript that runs on the users machine. 

The reason client side code is important is because it's usefulness with interactive webpages; interactive content runs faster and more reliably since the user’s computer doesn’t have to communicate with the web server every time there is an interaction. Browser-based games are one popular platform for client-side code, since the client-side code can ensure the game runs smoothly regardless of connectivity issues.

Malicious actors can wrap code in `<script> </script>` tags which tells the web browser to run it as Javascript code.

#### Cookies (yum)
Cookies are temporary login credentials saved on a user’s computer. For example when a user logs onto a site like Facebook, the site gives them a cookie so that if they close the browser window and go back to Facebook later that day, they are automatically authenticated by the cookie and won’t need to login again. 

#### Prevention
Some of the options available to prevent the above attack include but are not limited to:
* avoiding HTML inputs
* validating inputs (prevent users from posting data that doesnt meet criteria)
* block cookies 
* Set WAF rules

### Cross Site Forgery
Cross-Site Request Forgery (XSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they’re currently authenticated. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker’s choosing. If the victim is a normal user, a successful XSRF attack can force the user to perform state changing requests like transferring funds, changing their email address, and so forth. If the victim is an administrative account, XSRF can compromise the entire web application.

### Differences
Both attack types sound similar in nature, and they are. Key differences are:

#### XSS:
 * has the user trusting a badly implemented website 
 * attacker injects a script to the trusted website
 * users browser executes the attackers script

 #### XSRF
 * a badly implemented website trusts the user
 * attacker tricks web browser into issuing requests
 * website executes attackers requests

### SQL Injection
SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. It generally allows an attacker to view data that they are not normally able to retrieve. This might include data belonging to other users, or any other data that the application itself is able to access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

In some situations, an attacker can escalate a SQL injection attack to compromise the underlying server or other back-end infrastructure, or perform a denial-of-service attack. 

To put it simply, an attacker can leverage certain commands against the URL that the database queries in order to show database content that is meant to be hidden.
### File Inclusion 
This is one I understand in theory but here is what I have gathered. Web applications are written to request access to files on a given system, including images, static text, and so on via parameters. Parameters are query parameter strings attached to the URL that could be used to retrieve data or perform actions based on user input. The following graph explains and breaking down the essential parts of the URL.

And because we addresses work like file paths, an attacker could manipulate the URL to the path for passwords on a given site to then have those credentials displayed.