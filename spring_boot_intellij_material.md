

## How to open browser automatically in intellij

To make the browser start automatically when you run the Spring Boot app in IntelliJ Community Edition, you can follow these steps:

1. Open the Run/Debug Configuration dialog by clicking on the drop-down arrow next to the green Run button in the toolbar and selecting "Edit Configurations".

2. In the dialog, select the Spring Boot configuration you want to modify.

3. In the "Before Launch" section, click the "+" button and select "Run External Tool".

4. In the "Tool Settings" dialog, click the "+" button to add a new tool.

5. In the "Create Tool" dialog, enter a name for the tool (e.g. "Open Browser") and select "Browser" as the tool type.

6. In the "Browser Settings" section, enter the URL you want to open in the browser (e.g. "http://localhost:8080/") and select the browser you want to e.

7. Click "OK" to save the tool and close the dialog.

8. Back in the "Run/Debug Configuration" dialog, move the new "Run External Tool" item to the top of the list by clicking the up arrow button.

9. Click "OK" to save the configuration.

Now, when you run the Spring Boot app, IntelliJ will automatically open the specified URL in the selected browser.



## Add Json pretty print addon to see json in the best way!

## Important maven commands

1.mvn package => To create the package of maven project i.e its going to create jar / war file based on pom file config. its going to keep this file in target/name.jar

### Run spring app using java jar file 
  java -jar jar_file_name  => To run spring boot project from command line.
   1. move to the target folder by using cd command  i.e cd target
   2.  Now run jar file by using above command
   3.  ctrl+c to stop the server
 
 ### Run app using spring boot maven plugin 
from the project root folder execute this command
mvn spring-boot:run => its going to start the server



## Spring-boot-starter-actuator -> its useful for checking health of your application

1. Add spring-boot-startor-actuator dependency in your pom.xml file
2. management.endpoints.web.exposure.include=health,info,mappings (to expose health, info, mappings)
3. To expose all end points management.endpoints.web.exposure.include=*
4. To access health check localhost:8080/actuator/health
5. To check complete info details localhost:8080/actuator/info -> by default its going to show empty json.
   You need to information from application.properties file
   info.app.name=springboot three app
   info.app.description=its good app
   info.app.version=0.0.1
7. 
Add Json Formatter plugin in chrome


## How does Spring boot link the jars with my code?

Whatever these different functionalities spring boot has, ultimately everything is made up of java code right. Now whatever dependencies we include in our pom.xml, maven will download all those dependency jars for our project. Now when I  run my application, the main method will be executed. But I have just downloaded the jars, my code will still be the same, so how does the linking happen between my code & the jars that are downloaded i.e I want to know that just by downloading the dependency jars, how these different functionalities are added to my code?

Answer :-

So your question was never related to maven but to how does Spring applies security to the actuator just by adding a dependency without us writing any code, or similar situations.
Since Spring is a big framework, you are getting a lot of things preconfigured.

For example, you do not need to define with code InternalView resolver to display HTML, you will get it for free.

You do not need to define component scanning for beans, you will get it for free.
You do not need to write HTML for the login form for security, you will get it for free.

That "free", is not without code, it is simply preconfigured, and all those configurations that you get for free come from Spring library.
If you would try to implement any other InternalResolver, Security or component scanning, that is not from Spring ecosystem, it would not work.
The same goes for applying security to actuators, once you add a security dependency, HTTPSecurity class will be initiated from this package

    package org.springframework.security.config.annotation.web.builders;

And it will run authorization on all HTTP requests, which includes all requests the same as actuator.
Unless you decide to turn that off through application.properties file, that will be forwarded to this class

    UserDetailsServiceAutoConfiguration 

from this package

    package org.springframework.boot.autoconfigure.security.servlet;

So to answer your question, how it runs without any code.
A lot of things in Spring Boot is already preconfigured, and it is already set in the source code/jars of the Spring.
All these preconfigured features will work only with jars from the Spring ecosystem, it does not apply to anything external.

### Hi Chad. What's the use-case of IOC - or why do we have to externalize the construction and management of objects? Why is this configuration necessary? Why is DI not sufficient?

>> What's the use-case of IOC - or why do we have to externalize the construction and management of objects?

Yes, IoC is for externalizing the construction and management of objects.

Normally in your code, you create objects like:

TrackCoach myCoach = new TrackCoach();

But using Spring ... it will handle the creation of objects for you. It is like outsourcing. instead of you doing the work ... outsource it and someone will do the work. this is handled by spring's object factory.

So the Spring Framework does IOC for you.

>> Why is this configuration necessary?

To make your application flexible. When using Spring's XML based configuration, you can swap in new implementations without having to recompile your source code.

>> Why is DI not sufficient?

IoC and DI form a good partnernship. In order to get full power of DI you need a foundation of IoC.

---

If you'd like more details on IoC, check out these resources:

Spring IOC

- http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html

The IOC Design Pattern

- https://en.wikipedia.org/wiki/Inversion_of_control


## what is the use of IOC ?
 IOC (inversion of control) does several things for us:

    1. Decouples components and layers in the system
    2. Alleviates a component from being responsible for managing it's dependencies
    3. Enables us to swap dependency implementations in different environments w/o breaking our code.
    4. Allows a component be tested through mocking of dependencies.
    5. Provides a mechanism for sharing resources throughout an application.


You can read more about IOC here: https://en.wikipedia.org/wiki/Inversion_of_control

and here: *** https://stackoverflow.com/questions/3058/what-is-inversion-of-control?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa

## https://stackoverflow.com/questions/6550700/inversion-of-control-vs-dependency-injection
