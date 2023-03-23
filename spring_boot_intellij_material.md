

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

## https://jenkov.com/tutorials/dependency-injection/dependency-injection-replacing-factory-patterns.html


## Spring Singleton scope  vs java single tone pattern.. clarification

Here's a discussion on this topic: https://stackoverflow.com/a/48052897/1998950

https://stackoverflow.com/questions/15252284/what-is-the-difference-between-a-spring-singleton-and-a-java-singeletondesign-p


## What is the difference between @Bean and @Component
Here is a real-time use case of using @Bean: You can use @Bean to make an existing third-party class available to your Spring framework application context.

For example, I was recently working on a global real-time project using Amazon Web Services. The project made use of the Amazon Simple Storage Service (AWS S3). This is remote service that provides object storage in the cloud. You can think of AWS S3 at a high-level as a remote file server for storing files (pdfs, pngs etc).

Our Spring application needed to integrate with AWS S3 and store pdf documents. Amazon provides an AWS SDK for integrating with AWS S3. Their API provides a class, S3Client. This is a regular Java class that provides a client interface to the AWS S3 service. We needed to share the S3Client object in various services in our Spring application. However, the S3Client does not have the @Component annotation. The S3Client does not use Spring.

Since the S3Client is part of the AWS framework, we can't modify the source code for the S3Client directly. We can't simply add the @Component annotation to the S3Client source code. As a result, we need an alternative solution.

But no problem, by using the @Bean annotation, I can wrap this third-party class, S3Client, as a Spring bean. And then once it is wrapped using @Bean, it is as a singleton object and available in our Spring framework application context. I can now easily share this bean in my app using dependency injection and @Autowired. So think of the @Bean annotation was a wrapper / adapter for third-party classes. You want to make the third-party classes available to your Spring framework application context.


Here's a real-time example

Here is a snippet from our @Configuration class. We create an instance of the S3Client and wrap it as a Spring bean. The default scope is singleton. It is now available in our application context and we can inject it to other parts of our Spring application using @Autowired.

        @Bean
        public S3Client remoteClient() {
            
                // Create an S3 client to connect to AWS S3
                S3Client s3Client = S3Client.builder().region(Region.of(region))
                        .credentialsProvider(StaticCredentialsProvider.create(awsCreds)).build();
         
                return s3Client;    
        }

---

In the code below, this is a Spring service that uses the S3Client. The service @Service annotation is a subclass of @Component. This code uses @Autowired to inject the bean named "remoteClient". This bean was created in the configuration code above using @Bean.

Once the bean is injected, then our method can use this to interact with the Amazon S3 service. In this real-time project, we were processing insurance claims. We store the PDF invoices in the cloud using the AWS S3 service.

        @Service
        public class InsuranceClaimsServiceImpl implements ClaimsService {
            
            @Autowired
            private S3Client remoteClient;
         
            ...
         
            public void processClaim(Claim theClaim) {
         
         
                // read claim data
                FileData fileData = theClaim.getFileData("payerInvoice");
                String fileName = theClaim.getSubmittedFileName();    
         
                // get the input stream and file size
                    InputStream fileInputStream = fileData.getInputStream();
                        long contentLength = fileData.getSize();
         
                    //
                // store claim data in AWS S3 
                //
         
                // Create a put request for the object
                PutObjectRequest putObjectRequest = PutObjectRequest.builder()
                                    .bucket(bucketName)
                                    .key(subDirectory + "/" + fileName)
                                    .acl(ObjectCannedACL.BUCKET_OWNER_FULL_CONTROL).build();
                
                // perform the putObject operation to AWS S3 ... using our autowired bean
                remoteClient.putObject(putObjectRequest, RequestBody.fromInputStream(fileInputStream, contentLength))
            }
        }


As you can see, I was able to wrap a third-party class as a Spring bean. The AWS S3Client object was not originally annotated with @Component. The S3Client is not aware of Spring. But I could manually wrap it using @Bean. By doing this, the object is now available in our Spring application context. We can now share/reuse this bean in other areas of our Spring app by using dependency injection and @Autowired.

For other services in our application, if they need access to the S3client (singleton) then they can simply inject it using @Autowired. No need for each service to create a new instance of the S3Client every time. This keeps the application efficient in terms of memory and performance.

---

In summary: You can use @Bean to make an existing third-party class available to your Spring framework application context.

That is a real-time use case of @Bean.

Let me know if this clears your doubt.

