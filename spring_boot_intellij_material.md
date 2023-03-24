

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


## when to use singelton scope and when to use prototype scope when building enterprise Application?

In general, most apps tend to use singleton scope since they want to share a single instance of a backend object. For example a data access object (DAO). One single DAO to be used by all beans in the application. Singleton scope is the most common scope you will see used in real-world applications

Prototype scope is making use of objects that have unique values and must maintain state. Prototype is rarely used in real-world applications. Here is an online discussion of some who developers who had use cases for prototype scope. The discussion also includes a post from a former SpringSource employee on this thoughts of prototype scope.

Please visit these links below for more informations

https://stackoverflow.com/questions/9664810/spring-prototype-scope-use-cases

https://stackoverflow.com/questions/21969044/when-to-use-spring-prototype-scope

https://stackoverflow.com/questions/16058365/what-is-difference-between-singleton-and-prototype-bean


## What's the difference between using @Autowired and new object creation?

Autowired vs New Keyword
0 upvotes
Hello · Lecture 33
· 3 years ago


What's the difference between using

@Autpwired

private MyClass myclass ;


and


MyClass  myClass = new MyClass  ();

I found the clue here
https://stackoverflow.com/questions/30908648/spring-autowired-vs-using-new-keyword-to-create-object


But what does this statement means?

The typical use of @Autowire is to automatically fill a property, when initializing a bean, with a singleton dependency.

Answer :-

Behind the scenes, the @Autowired annotation will inject the dependency. The difference between @Autowired and the "new" keyword is the @Autowired annotation honors the scope of the bean. In Spring, all beans are singleton by default. As a result, with singleton scope, Spring will not create a "new" instance every time. Instead it will share the singleton reference.

It may be hard to see the benefit of @Autowired and dependency injection in small examples. The real power of @Autowired and dependency injection is noticeable when working on real-time projects. We create multiple real-time projects in the course and you will get to see @Autowired and dependency injection in action.

Let me know if that clears your doubt.


## Difference between @Component and @RestController ?

What does @RestController annotation do ?

Hello Akhil, it marks a class that will be a bean but it also marks it that it will be responsible for triggering methods on specific URLs.
So it is basically @Component + URL trigger of methods.

and is @Component annotation is what we call IOC i.e. whichever class uses @Component it's object will be created automatically. Am I correct here?

Correct. Any annotation will create those beans automatically @Bean, @Service, @Controller, @Component, @Repository.

Also you mentioned we do not need @Autowired when we have single constructor then if we have multiple constructor can we add @Autowired on all of the constructor?

Correct.

## Daily useful spring libraries in pom.xml

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
     
      <groupId>io.playground</groupId>
      <artifactId>SpringAndHibernate</artifactId>
      <version>1.0-SNAPSHOT</version>
     
      <properties>
        <spring-security.version>5.1.5.RELEASE</spring-security.version>
        <spring.version>5.3.9</spring.version>
      </properties>
     
      <dependencies>
        <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <version>1.18.20</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>org.apache.commons</groupId>
          <artifactId>commons-lang3</artifactId>
          <version>3.12.0</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-core</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-orm</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-web</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webflux</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework.security</groupId>
          <artifactId>spring-security-core</artifactId>
          <version>${spring-security.version}</version>
        </dependency>
        <dependency>
          <groupId>org.junit.jupiter</groupId>
          <artifactId>junit-jupiter</artifactId>
          <version>5.7.2</version>
          <scope>test</scope>
        </dependency>
        <dependency>
          <groupId>org.mockito</groupId>
          <artifactId>mockito-core</artifactId>
          <version>3.11.2</version>
          <scope>test</scope>
        </dependency>
        <dependency>
          <groupId>org.mockito</groupId>
          <artifactId>mockito-junit-jupiter</artifactId>
          <version>3.11.2</version>
          <scope>test</scope>
        </dependency>
      </dependencies>
     
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
              <source>8</source>
              <target>8</target>
            </configuration>
          </plugin>
          <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
              <excludes>
                <exclude>
                  <groupId>org.projectlombok</groupId>
                  <artifactId>lombok</artifactId>
                </exclude>
              </excludes>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    
    ### How does spring know that it needs to build a cricketcoach here?
    
    WHat I am wondering is how Spring is able to know that we wanted to make a cricketcoach object here. We defined in the constructor that we can make Coach objects, but how does Spring know, in this case, that we want to make a CricketCoach object and use it's method of getDailyWorkout? We did not specify that we wanted a cricketCoach so it just seems to me that Spring had to guess as that was the only viable class that was implementing Coach. But what if you had more classes that implemented Coach?
    
    Answer :-
    
    Spring will scan for all Spring Beans (classes that have @Component annotation). It will determine if any of these classes implement the Coach interface. If Spring finds one then it will inject the bean. In our example, we only have one class CricketCoach that is annotated with @Component and implements the Coach interface. Hence, Spring will select the CricketCoach and then inject it.

If there were no matches, then Spring will throw an exception and fail to start. You can test this scenario by commenting out the @Component annotation on the CricketCoach class.

Also, you may wonder what happens if there are multiple matches (for example multiple Coach implementations: CricketCoach, TrackCoach, TennisCoach etc). Then Spring will not know which one to use ... it will throw an exception ... and fail to start. We cover this exact scenario a bit later in the videos and make use of a solution using @Qualifier annotation.

## Bean Scopes

https://docs.spring.io/spring-framework/docs/3.0.0.M3/reference/html/ch04s04.html


##  Singleton scope VS Prototype Scope ?

    Prototype scope = A new object is created each time it is injected/looked up. It will use new SomeBean() each time.

    Singleton scope = The same object is returned each time it is injected/looked up. Here it will instantiate one instance of SomeBean and then return it each time.

Prototype bean is created at the time of usage. So when you would like to have statefull beans there is strong need sometimes to have prototypes scope or when you don't wont to cache any values in beans. Prototype bean can be associated with one session or some call.

Example:

A data access object (DAO) is not typically configured as a prototype, because a typical DAO does not hold any conversational state; it was just easier for this author to reuse the core of the singleton diagram.

So depending of how you want your beans to behave, you will use specific scope. Singleton is great for database connection ( you need to create only one ), and it would be pointless to create new bean each time using prototype.

You can find more examples of them here

## Why does bean instantiation happens before dependencies injection?

I think bean instantiation is like building a car, and dependencies injection is like putting different car parts (engine, tire ...) together.

How can you build a car before you got all the needed parts?

The bean is created first. Then we inject the dependencies.

In simple terms, here is a real world analogy

You want to move your family into a brand new house built from scratch. This is the process

Step 1:  Construct the house (build the house from scratch ... from the ground up. This is instantiating/constructing the object)

Step 2: Move your furniture and family into the house (inject your dependencies)


The key point is that you have to instantiate/construct the object first before injecting dependencies. The same as you have to build a house first before you can move in your furniture.

>> How can we create an object without supplying its constructor arguments?

Spring can create an object using the no-argument constructor.

Coach myCoach = new TrackCoach();


Then Spring will inject the dependencies using either field injection or setter/method injection. Here's an example using setter injection

myCoach.setFortuneService(new HappyFortuneService());


If you are using constructor injection, then Spring will pass the dependencies during construction.

Coach myCoach = new TrackCoach(new HappyFortuneService());

## Why do we destroy the bean ?
Hi, I want to know why is there a need to close the context at very first place. What happens if we keep it open.?

Ans:- Since the app context is a ResourceLoader (i.e. I/O operations) it consumes resources that need to be freed at some point. It is also an extension of AbstractApplicationContext which implements Closable.

Therefore if you leave it open at some point you will run out of resources and your application will crash.
