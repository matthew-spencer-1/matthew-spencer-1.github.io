# Spring Boot & MongoDB
Spring has been a strong framework, in various implementations, in Java for well over a decade. Spring Boot refine many of the problems with Spring MVC, primarily that applications start quickly and no longer require being deployed to an external web-server. This capability allows for applications to adopt a more modular mindset, implementing micro-services.  
This project is an overview of a web application leveraging a MongoDB back end for storing data. The application utilizes role base security for access to various functionality.  

Development for the final version of this application came in two phases. 
- First was the build out of the SpringBoot application framework, and Java objects, and the connection to the MongoDB backend. 
	- This process is outlined in more detail in the [Development Narrative](/ProjectNarratives/Milestone4Narrative.pdf) for this section.
- Second was the build out of the full security layer including user sign up and login functionality. Along with the security implementation came configuration of access based on user roles
	- This process is outlined in more detail in the [Development Narrative](/ProjectNarratives/Milestone3Narrative.pdf) for this section.

#### A quick note about Microservices
In a true microservices implementation, the HTML based web application would be a separate implementation from a REST based web application. However, this codebase implements both. The REST and HTML portions of the application act separately, for example, there are two different controller classes. While the implementation is in a single repository, the behavior is a microservices mindset. For example, where the HTML side of the house can easily import and upload a JSON file to the database, instead, it simply pushes the file over to the REST interface as though it were running on a separate server. Similarly, interfaces for updating, deleting, and inserting new records use the REST interfaces rather than make calls directly to the database to reflect a microservices mindset.

## Functionality
The application is meant to allow a user to have an overview of stock performance, provide the ability to look up top performers in the industries represented in the data set, and get full details of the individual stocks. The usefulness of the data is non-existent, this is an overview of performing operations in a database in a secure role based environment. 

## Configuration
- By default the application is pointed to a MongoDB implementation running on the default port on localhost. Default settings are easily changed via the application.properties file. 
- Security has three roles by default
	- ADMIN
		- The administration level. Can update access to other user security levels, write to stock records, use REST interface as well as HTML
	- USER
		- Standard User access. Read only access to stock records, can access HTML pages only
	- RESTFul
		- Provide access to REST interface methods capable of writing to the database (Read-only REST methods are open access). Has no access to HTML pages.

## Code Base
Please feel free to review the implementation code base [here](https://github.com/matthew-spencer-1/Java_SpingBoot_MongoDb_Login)  
A few notes:
- By default, any user signed up through the sign-up page will have USER access, the first ADMIN must be created at the database
- Stock data for the app is [here](/projectDataFiles/bootMongoSecurity/Stocks.csv) (.csv) and can be pushed to the app through the web page
- There is no security configured for the MongoDB in application.properties
- MongoDB database and collections will generate when the application is run for the first time, including necessary default data such as roles
