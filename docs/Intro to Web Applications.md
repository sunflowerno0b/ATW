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


