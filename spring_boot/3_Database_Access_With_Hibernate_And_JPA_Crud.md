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

If your class doesn't have any constructors with arguments, then java will give  you default no-arg constructor for free. in that case, you don't need to add one.


