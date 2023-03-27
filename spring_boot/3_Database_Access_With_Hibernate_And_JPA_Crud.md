## Why we need to import javax.persistence.* why not hibernate

Why we need to import javax.persistence.* why not org.hibernate.* ?
Please share some detail if there is no use of org.hibernate.* then why they created ??

The package javax.persistence is provided by Java Persistence API (JPA) whereas org.hibernate.annotations is provider by Hibernate. **JPA is a specification which defines a set of rules, syntax and symantics to manage the relational data. It defines programming interfaces, lifecycle rules for persistent objects and query features. Whereas Hibernate is a real implementation of JPA**. There are other JPA implementations as well such as TopLink, OpenJPA, DataNucleus, EclipseLink. Hibernate is supposed to be more powerful and use-voted selection though. I would recommend to go with javax.persistence. That's because **if you wanted to switch to other implementations than Hibernate, you would be able to do that with no changes or very less changes in the POJO classes. This ensures the "loose coupling" design**.


**The @Entity annotation is the modern replacement for “ to connect each class to their respective table in database”.

The annotation based approach is the modern approach and it minimizes the configuration.

**its called plugin pattern**, we only used it for specific use and we have more freedom when it comes from migration from one framework to other from list that I wrote above.

**Connect to the database in the DAO class and also saving objects to database is main purpose of hibernate in our application**

The javax.persistence.api **is the standard API for Java Persistence (JPA). JPA is a standard specification from Oracle. Hibernate provides an implementation of the JPA specification.**

**The recommendation from the Hibernate team is to leverage the JPA API as much as possible. When there are cases that are not covered by the JPA API then fallback and use the Hibernate API.**

---

Also here is some additional reading that you may find useful

What is the difference between JPA and Hibernate?

https://stackoverflow.com/questions/9881611/whats-the-difference-between-jpa-and-hibernate

https://www.quora.com/What-is-the-difference-between-Hibernate-and-JPA

---

## Is no-arg constructor always required for hibernate?

yes, it is required when using the Hibernate framework.

Hibernate needs the no-arg constructor because **it will create an instance of your entity using the new keyword**. So, if you have an entity class named "Student", then Hibernate will attempt to create it using the no-arg constructor with "new Student()".

This happens behind the scenes by Hibernate.

This requirement is documented in the Hibernate Users Guide.

If your class doesn't have any constructors with arguments, then jvm will give  you default no-arg constructor for free. in that case, you don't need to add one.

**certainly jvm creates default constructor if you have not defined any constructor in your class. but if you have defined any argument constructor in your class then jvm will not automatically add default constructor. constructor allocates memory for object when it calls super class or object class constructor so here jvm knows class already have one constructor so it doesn't add new**.

here we have added no argument constructor so if you create object without passing any argument then it will not be able to call constructor to create object and throw error.


Hibernate requires a no-arg constructor. Either one you create or the free one.

Here are the rules regarding constructors in relationship to Hibernate.

1. If your class does not define any constructors, Java will give you a no-arg constructor for free. There is no need to explicitly declare a no arg constructor.

2. **If your class defines a constructor with arguments, then Java will NOT give a no-arg constructor. In this case, you MUST explicitly define a no-arg constructor in your class.**

## What is the difference between @Entity(name="student") and @Table(name="student"). Are the performing the same result?

@Entity: Specifies that the class is an entity. This annotation is applied to the entity class.

Source: http://docs.oracle.com/javaee/7/api/javax/persistence/Entity.html


@Table: Specifies the primary table for the annotated entity. 

Source: http://docs.oracle.com/javaee/7/api/javax/persistence/Table.html

## which is the best approach for deleting objects among HQL and other?

Delete using the HQL is most efficient. with this approach, you do not have to load object into memory first ... saves you a step.

For efficiency and performance, I'd recommend deleting using HQL. This will cover the case if the object id exists or not.
In  case of deleting directly using HQL .... it works similar to regular SQL .... no exceptions for non-existent objects.

Now, if you tried to retrieve a non-existent object, you will encounter errors.

If you tried to retrieve a non-existent: 

Student tempStudent = session.get(Student.class, 99999);    // this returns a null object



Student tempStudent = session.load(Student.class, 99999);    // returns a proxy object ... the proxy object will throw exception on first access

Details on retrieving non-existent objects can be found here:

https://www.mkyong.com/hibernate/different-between-session-get-and-session-load/

## How / When does Hibernate call setters and getters?

When we call 
Employee employee = session.get(Employee.class, 2);
It calls the default constructor, so I think Hibernate then calls setters behind the scene to set all the fields retrieved from the database. Is this correct? If so, why I can't see the output from System.out.println in console? (I have added System.out.println in every setter method so as to track the progress).

**Answer :-**

Hibernate has two ways to access data for an entity

1. field access

2. method access (getter/setter)

---

1. field access:
This is the default. Hibernate will access the fields directly using introspection and reflection. Hibernate can directly update the fields regardless of visibility (public, private protected). In this case, the getter/setter methods are not called. That's why you never see the sysout println statements in your code.

2. method access (getter/setter)
In this case, Hibernate will only access data via the getter/setter methods in the entity.

---

Here's a good example that shows how to set this up

@Access in Hibernate Annotation

https://www.concretepage.com/hibernate/access-hibernate-annotation

---

This is discussed in Section 2.5.2 of Hibernate User Guide

https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#entity-pojo-accessors

And section 2.5.12
https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#access


## How can i create a parameterized update or delete statement in hibernate?

How can i create a parameterized update or delete statement in order to avoid sql injection in case of using string concatenation?

**Ans :-**

A common misconception is to think that since you are using JPA or Hibernate you are automatically safe.

This post from stack overflow contains some examples of using bind parameters: https://stackoverflow.com/questions/14102334/how-to-prevent-sql-injection-with-jpa-and-hibernate/54122517 and should be helpful to you.

Also check:

https://vladmihalcea.com/a-beginners-guide-to-sql-injection-and-how-you-should-prevent-it/

and

https://www.baeldung.com/sql-injection

## Session lifecycle
In which situations do we need a new session? In which cases should we commit a session and ask for the other from session factory?

We are not creating new sesion in this example. We are just getting the session instance reference from the Session Factory.

The Session object is lightweight and designed to be instantiated each time an interaction is needed with the database

**The session objects should not be kept open for a long time because they are not usually thread safe and they should be created and destroyed them as needed.**

commit is to end your current transaction and make permanent all changes performed in the transaction.

Here's a discussion on the commit: https://www.udemy.com/spring-hibernate-tutorial/learn/lecture/5117020#questions/2030708

## Warnings in QueryStudentDemo.class

Is there any possibility to avoid warnings in QueryStudentDemo.class? 

This warning appear always when I create new query:
````
Type safety: The expression of type List needs unchecked conversion to 
 conform to List<Student>
  
  Ans :-
  
  You can add Student.class argument to the method call, like:  session.createQuery("from Student", Student.class).getResultList();
 ````
## Who is responsible for creating the JDBC?

t's obvious that it's not mySQL who creates the JDBC. It's also not Spring Boot since Spring Boot only detects the JDBC based on the given URL. Then how is the Java database connectivity created in the first place? Who's responsible for doing that?

**Ans**-
Actually, it is Spring Boot that is responsible for creating the JDBC connection. In simple terms, Spring Boot will autoconfigure the JDBC connection based on the application.properties file and entries in the pom.xml file.

If you'd like more details on how this works behind the scenes, see following blog post

How Spring Boot’s Autoconfigurations Work

## 
