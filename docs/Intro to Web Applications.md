## What are web applications?

Web applications are interactive applications that run on web browsers. Normally they adopt the client-server architecture to run and handle interactions.

They have the website interface which is what the user see's and engages with, then there's the back end where the source code that runs on the servers live.

## Historic
### Past
In web 1.0 it was static pages for everyone and appeared the same for everyone. 

### Now
Contrast to today where web pages are dynamic, improved interoperability and heavier emphasis on user experience (UX). 

Deeper reading found [here](https://websitebuilders.com/how-to/glossary/web1/) & [here](https://en.wikipedia.org/wiki/Web_2.0#Web_1.0)

## Traits 

Web applications are platform-independent and can run on any browser on any operating system. The functions of a web application are executed remotely on the remote server (leaving the users hard drive free). This also improves version roll out, all users no matter where have access to all the applications because updates are stored on the web server. 

Native Operating systems are another type of web applications. IT allows to create custom experiences that go further than just the web browsers capabilities. 

## Web Application Distribution 

THere are open source web applications used world wide. But there are other that are closed source and normally sent through a subscription plan. 

### open source web applications
[Joomla](https://www.joomla.org/about-joomla.html), [Wordpress](https://wordpress.com/). Will attempt to find more at another time. 

### closed source web applications

[Wix](https://www.wix.com/),[Shopify](https://www.shopify.com/),[DotNetNuke](https://www.dnnsoftware.com/
). 

### Security 
Because a web application can is accessed  by many in around the world, its essential to make sure the web application is secure. A deeper reading in web application security testing can be found [here](https://github.com/OWASP/wstg/tree/master/document/4-Web_Application_Security_Testing). 

Front end trinity vulnerabilities are: 


+ HTML
+ CSS
+ JavaScript

Another vulnerability type is SQL injections that are typically tied to Active Directory.

## Common Flaws

[SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection): allowing attackers to spoof identities, tamper with data or disclose / destroy system data.

[File Inclusion](https://owasp.org/www-community/attacks/SQL_Injection): allowing attackers to include a file that if modified correctly could lead to cross site scripting, denial of service and more.


[Unrestricted File Upload](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload): files that have executable code into systems.

[Indirect Object Reference](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html): allow an attacker to find a pattern to then extort.


## Web Application Layout

| Category                       | Description |
|--------------------------------|-------------|
| Web Application Infrastructure |the structure of required components such as a database needed for the application to run as intended.  |
| Web Application Components     |represents all the components that the web application might interact with. Divided into the UI/UX,Client and Server. |
|Web Application Architecture   |Architecture comprises all the relationships between the various web application components. |


Web application infrastructure can be split into 4 main models:


+ Client-Server
+ One server 
+ Many Servers - One Database 
+ Many Servers - Many Databases 


Client-Server: the server hosts the web application and distributes it to any client that accesses it. 

### Breakdown
A client will visit a web URL, the server uses the main web application interface UI. The user will click a button or request a specific function, think adding an item to a cart, logging in, etc. The browser sends an HTTPS/HTTP request to the server which then takes that request and performs the necessary tasks. When the server has the required data it sends the results back to the client browser displaying the results in a human-readable way. 

One Server:
Considered the riskiest design- the web application and their components including the database are hosted on a single server.If the server becomes compromised or goes down for any reason, all hosted web applications become entirely inaccessible until resolved. 

Many Servers - One Database: 
This model can allow several web applications to access a single database and to have access to the same data without syncing the data between them. The web applications can be replicated from one of the main applications (backup/primary) or they can be separate web applications that share common data. 


Many Servers-Many Databases:
Databases hold different web application data. The web application can only access private data and only common data that is shared across web applications. It's also possible to host each web applications database on its separate database server. This method is best used for redundancy purposes. This requires the use of load balancers because it offers access control measures and proper asset segmentation. 

## Web Application Architecture

| Layer              | Description                                                                                                                                                                                 |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Presentation Layer | UI process components that enable communication with the application and the system. Client accesses via web browser and are returned to the server in the form of HTML,Javascript and CSS. |
| Application Layer  | All web requests by the client are correctly processed. Criteria's are checked, includes authorization, privileges and data passed on to the client.                                        |
| Data layer         | Works with the application later to determine where the required data is stored and can be processed.                                                                                       |

### Microservices
Normally these are independent components of the web application that are typically programmed for one task only. These services can range to the following:

+ registrations
+ searching
+ payments 
+ ratings 
+ reviews 

Microservices use what would be considered stateless, the request and response are independent. The reason for this is that the data is stored separately from its respective microservice. 

Microservices have easier scaling, faster development of applications , agility, reusable code & resilience. 

### Serverless 
Cloud providers like Azure, AWS and GCP allow serverless architectures for paid fees. The web applications are stateless, running on computing containers like Docker. This allows for companies to have the flexibility to build and deploy applications and services without having to manage the infrastructure.

### Front End & Back End
Front end refers to everything that the user is going to interact with on a website, this also goes hand in hand with the UX or user experience. Languages for front end are normally HTML, CSS, & Javascript.

Back end of a web application drives the core web application functionalities which are executed on the back end server that then processes everything required for the web application to run correctly. 

| Component              | Description                                                                          |
|------------------------|--------------------------------------------------------------------------------------|
| Back end server        | hardware and OS's  that host the components like Linux,Windows or containers         |
| Web server             | handles all the HTTP requests and connections like APache & NGINX                    |
| Databases              | store and retrieve the web application data like MySQL MSSQL                         |
| Development frameworks | development frameworks are used to develop core web application, like PHP, C#,Python |


# HTML
 URL Encoding, or percent-encoding. For a browser to properly display a page's contents, it has to know the charset in use. In URLs, for example, browsers can only use ASCII encoding, which only allows alphanumerical characters and certain special characters. Therefore, all other characters outside of the ASCII character-set have to be encoded within a URL. URL encoding replaces unsafe ASCII characters with a % symbol followed by two hexadecimal digits.

For example, the single-quote character ''' is encoded to '%27', which can be understood by browsers as a single-quote. URLs cannot have spaces in them and will replace a space with either a + (plus sign) or %20.

The World Wide Web Consortium (W3C) defines DOM as:

"The W3C Document Object Model (DOM) is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document."

The DOM standard is separated into 3 parts:

    Core DOM - the standard model for all document types
    XML DOM - the standard model for XML documents
    HTML DOM - the standard model for HTML documents



## CSS
CSS defines the style of each HTML element or class between curly brackets {}, within which the properties are defined with their values (i.e. element { property : value; }).


# JavaScript


JavaScript is usually used on the front end of an application to be executed within a browser. 

While HTML and CSS are mainly in charge of how a web page looks, JavaScript is usually used to control any functionality that the front end web page requires.

JavaScript is also used to automate complex processes and perform HTTP requests to interact with the back end components and send and retrieve data, through technologies like Ajax.

## Sensitive Data Exposure

On the client-side if attacked, they put the end-user in danger of being attacked and exploited if they do have any vulnerabilities. If a front end vulnerability is leveraged to attack admin users, it could result in unauthorized access, access to sensitive data, service disruption, and more.

Sensitive Data Exposure refers to the availability of sensitive data in clear-text to the end-user. 

Source code is of a web page or the page source on the front of web application is the HTML source code not to be confused with the back end code that is typically only accessible on the server itself. You can view any websites page source by either right clicking and selecting page source or pressing `ctrl + u`. IF those options do not work you could use a web proxy like Burp suite. 


## HTML Injection 
It is critical to validate and sanitize user input on both the front end and the back end of the user input.

HTML Injection occur when unfiltered user input is displayed on the page. This can be either through retrieving previously submitted code, think a user comment from the back end of the database or directly displaying the unfiltered input through JavaScript on the front end.

Web page defacing consists of injecting new HTML code to change the web pages appearance. 

Injecting a malicious link  could be something like inserting the following line into the web page `<a href="evil website">Click Me</a>`. This would direct the user to press click me which would take them else where to obtain their credentials.

## Cross-Site Scripting (XSS)
 However, XSS involves the injection of JavaScript code to perform more advanced attacks on the client-side, instead of merely injecting HTML code. There are three main types of XSS:


| Type           | Description                                                                                                                |   |   |   |
|----------------|----------------------------------------------------------------------------------------------------------------------------|---|---|---|
| Reflected XSS  | happens when user input is displayed on the page after processing (think search result/ error message)                     |   |   |   |
| Stored XSS     | happens when user input is stored on the back end database and then displayed upon retrieval (think posts/comments)        |   |   |   |
| DOM XSS        | happens when user input is directly shown in the browser and is written to an HTML DOM (vulnerable username or page title) |   |   |   |



if you're able to input your payload into a web site to, for example, obtain a cookie value. That value can then be used to attempt to authenticate to the victims account.

## Cross-Site Request Forgery(CSRF)
Utilizes front end vulnerability that is caused by unfiltered user input. It performs certain queries and API calls on a web application that the victim is currently authenticated to, allowing the attacker to perform actions as the authenticated user.

| Type         | Description                                                                                           |   |
|--------------|-------------------------------------------------------------------------------------------------------|---|
| Sanitization | remove special characters and non-standard characters from user input before displaying or storing it |   |
| Validation   | ensuring that submitted user niput matches the expected format, think email matching email format     |   |

Web application firewall (WAF) filters, monitors and blocks HTTP traffic to and from a web service. 


## Back End Servers
A back end server is the hardware and operating system on the back end that hosts all of the applications necessary to run the web application. It's the real system running all of the processes and carrying all of the tasks that make up the entire web application. The back end server fits in the data access layer. There are 3 back end components:

1) web server 

2) database 

3) development frame work 