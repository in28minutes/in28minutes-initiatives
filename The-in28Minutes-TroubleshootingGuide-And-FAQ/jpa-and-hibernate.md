## Unable to login into H2 Console

1. Do you have H2 dependency in `pom.xml`? Try removing `<scope>runtime</scope>` and see if it makes a difference.

```
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
</dependency>
```

2. Check if H2 Console is enabled in `application.properties` 

```
spring.h2.console.enabled=true
```

3. Are you using >=2.3.0 Release of Spring Boot? You would need to configure this in `application.properties`.

```
spring.datasource.url=jdbc:h2:mem:testdb
```

> Why is this needed? In releases >=2.3.0 , Spring Boot creates a database with random URL as shown below. We do NOT want that. We want a constant URL.

```
H2 console available at '/h2-console'. Database available at 'jdbc:h2:mem:dd222195-7e0b-4dc0-ae4c-7f53e5ea7ceb'
```

4. Make sure you are using `jdbc:h2:mem:testdb` as the database URL in H2 Console as shown in the image below.

In the browser, change the database url to jdbc:h2:mem:testdb (Shown in the screen below).

![](images/h2-solution-image.png)

5. Delete your maven local repository () and rebuild the project. (You are right. This looks silly. But do not skip it. I've seen many problems caused by dependency caches!)

![](images/eclipse-maven-m2-folder.png)

## Tables are not created

### No 1 : Are you using Spring Boot >=2.3.0 Release?

Are you using >=2.3.0 Release of Spring Boot? Can you configure this in `application.properties`

```
spring.datasource.url=jdbc:h2:mem:testdb
spring.data.jpa.repositories.bootstrap-mode=default
```


You should see this in the log
```
H2 console available at '/h2-console'. Database available at 'jdbc:h2:mem:testdb'
```

### No 2 : Make sure you have the right annotations!

Make sure that the Entities have @Entity annotation and the Repository class has @Repository annotation

### No 3 : Make sure your component is picked up by Component Scan

Spring Boot does a component scan in the package and sub-packages where your @SpringBootApplication is defined. 

Why is this important?

If your entity class or the repository class is NOT under the package of your @SpringBootApplication class, it will NOT be picked up by component scan. 

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

