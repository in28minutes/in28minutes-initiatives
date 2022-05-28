## JPA and Hibernate Debugging Guide

## Unable to login into H2 Console

Enable h2 console
```
spring.h2.console.enabled=true
```

You don't want a random generated h2 database url. Make it a constant.
```
spring.datasource.url=jdbc:h2:mem:testdb
```

Use `jdbc:h2:mem:testdb` as the database URL in H2 Console
![](images/h2-solution-image.png)

If you still have problems, try removing `<scope>runtime</scope>`  from your pom.xml definition of h2 and see if it makes a difference.

```
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
</dependency>
```

## Tables are not created

If you are having problems with table creation or logging into H2 console, we recommend using this configuration in `application.properties` (This is the FIRST THING you should try. Reasons for each of the configuration is explained later in the guide.)

```
spring.datasource.url=jdbc:h2:mem:testdb;NON_KEYWORDS=USER
spring.h2.console.enabled=true
spring.jpa.defer-datasource-initialization=true
spring.data.jpa.repositories.bootstrap-mode=default
```


https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.5.0-M3-Release-Notes#hibernate-and-datasql => *By default, data.sql scripts are now run before Hibernate is initialized. This aligns the behaviour of basic script-based initialization with that of Flyway and Liquibase. If you want to use data.sql to populate a schema created by Hibernate, set spring.jpa.defer-datasource-initialization to true. While mixing database initialization technologies is not recommended, this will also allow you to use a schema.sql script to build upon a Hibernate-created schema before it’s populated via data.sql* 

```
spring.jpa.defer-datasource-initialization=true
```

Notes about bootstrap-mode https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.3-Release-Notes#bootstrapmode-for-jpa-repositories
```
spring.data.jpa.repositories.bootstrap-mode=default
```

Delete schema.sql if you have created one. If `schema.sql` file exist, tables are NOT created.


## Make sure that Components are picked by Component Scan

Have the right annotations!

```
@Entity
public class Todo {


@Repository
public class ComponentDAO {
```


Spring Boot does a component scan in the package and sub-packages where your @SpringBootApplication is defined. 

>  Why is this important? If your entity class or the repository class is NOT under the package of your @SpringBootApplication class, it will NOT be picked up by component scan. 

#### RECOMMENDED OPTION - Option 1 : Move the component under component scan

Simplest way to fix this is to identify the packages of the SpringBootApplication class and move all the components into that package or sub-packages of it. 

#### Option 2 : Add component and entity scan for the packages containing the components
```
@SpringBootApplication(scanBasePackages= {"com.project.currency.*"})
@EntityScan(basePackages = {"com.project.currency.model"})
@EnableJpaRepositories(basePackages = {"com.project.currency.repository"})
```

Learn more about component scan:
- https://github.com/in28minutes/in28minutes-initiatives/tree/master/The-in28Minutes-TroubleshootingGuide-And-FAQ#q---what-is-the-need-for-a-component-scan


## 2.3.0 Course Update

With the latest versions of Spring Boot (2.3+), the H2 database name is randomly generated each time you restart the server.

You can find the database name and URL from the console log.

#### RECOMMENDED: 

Make the database URL a constant by configuring this in application.properties.

```
spring.datasource.url=jdbc:h2:mem:testdb
```

Delete your maven local repository (content of .m2 folder) and rebuild the project. (You are right. This looks silly. But do not skip it. I've seen many problems caused by dependency caches!)

![](images/eclipse-maven-m2-folder.png)


#### If you face any problems:

**Spring Boot 2.3.1 Upgrade - Changes**
- https://github.com/in28minutes/jpa-with-hibernate/commit/1f30e868ccd2eb7e69cdb989bc990cd00cc82168

**JUnit 5 Upgrade - Changes**
- https://github.com/in28minutes/jpa-with-hibernate/commit/0ae2007c8e08420e6d5ab2a86499274c7c60c8ae