
## Complete Code Example

# junit-in-5-steps
## step22.md

## Complete Code Example


### /notes.txt

```
Questions
- Where is the database created?
- What schema is used to create the tables?
- Where are the tables created?
- Can I see the data in the database?
- Where is Hibernate coming in from?
- How is a datasource created?

Magic of Spring Boot and in Memory Database
- Zero project setup or infrastructure
- Zero Configuration
- Zero Maintainance
- Easy to use for Learning and Unit Tests
- Simple Configuration to switch to a real database

# Restrictions of using in-memory database
- Data is not persisted between restarts

Spring Boot chooses a default value for you based on whether it thinks your database is embedded (default create-drop) or not (default none). 

HibernateJpaAutoConfiguration matched:
 - @ConditionalOnClass found required classes 'org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean', 'javax.persistence.EntityManager'; @ConditionalOnMissingClass did not find unwanted class (OnClassCondition)
 - HibernateEntityManager found class 'org.hibernate.ejb.HibernateEntityManager' (HibernateJpaAutoConfiguration.HibernateEntityManagerCondition)

DataSourceAutoConfiguration matched:
 - @ConditionalOnClass found required classes 'javax.sql.DataSource', 'org.springframework.jdbc.datasource.embedded.EmbeddedDatabaseType'; @ConditionalOnMissingClass did not find unwanted class (OnClassCondition)

JpaBaseConfiguration#entityManagerFactory matched:
 - @ConditionalOnMissingBean (types: org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean,javax.persistence.EntityManagerFactory; SearchStrategy: all) did not find any beans (OnBeanCondition)

JpaBaseConfiguration#transactionManager matched:
 - @ConditionalOnMissingBean (types: org.springframework.transaction.PlatformTransactionManager; SearchStrategy: all) did not find any beans (OnBeanCondition)
```
---

### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.learning.jpa</groupId>
	<artifactId>jpa-in-10-steps</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>jpa-in-10-steps</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.BUILD-SNAPSHOT</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>com.h2database</groupId>
			<artifactId>h2</artifactId>
			<scope>runtime</scope>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

	<repositories>
		<repository>
			<id>spring-snapshots</id>
			<name>Spring Snapshots</name>
			<url>https://repo.spring.io/snapshot</url>
			<snapshots>
				<enabled>true</enabled>
			</snapshots>
		</repository>
		<repository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</repository>
	</repositories>

	<pluginRepositories>
		<pluginRepository>
			<id>spring-snapshots</id>
			<name>Spring Snapshots</name>
			<url>https://repo.spring.io/snapshot</url>
			<snapshots>
				<enabled>true</enabled>
			</snapshots>
		</pluginRepository>
		<pluginRepository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</pluginRepository>
	</pluginRepositories>


</project>
```
---

### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/entity/User.java

```java
package com.in28minutes.learning.jpa.jpain10steps.entity;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

//Table - User
@Entity
public class User {

	@Id
	@GeneratedValue
	private long id;

	private String name;

	private String role;

	protected User() {

	}

	public User(String name, String role) {
		super();
		this.name = name;
		this.role = role;
	}

	public long getId() {
		return id;
	}

	public String getName() {
		return name;
	}

	public String getRole() {
		return role;
	}

	@Override
	public String toString() {
		return String.format("User [id=%s, name=%s, role=%s]", id, name, role);
	}
}
```
---

### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/JpaIn10StepsApplication.java

```java
package com.in28minutes.learning.jpa.jpain10steps;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class JpaIn10StepsApplication {

	public static void main(String[] args) {
		SpringApplication.run(JpaIn10StepsApplication.class, args);
	}
}
```
---

### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/service/UserDAOService.java

```java
package com.in28minutes.learning.jpa.jpain10steps.service;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.transaction.Transactional;

import org.springframework.stereotype.Repository;

import com.in28minutes.learning.jpa.jpain10steps.entity.User;

@Repository
@Transactional
public class UserDAOService {
		
	@PersistenceContext
	private EntityManager entityManager;
	
	public long insert(User user){
		entityManager.persist(user);
		return user.getId();
	}
}

/*
 * Spring Data JPA
 * 
 * 
 * 
 */
```
---

### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/service/UserRepository.java

```java
package com.in28minutes.learning.jpa.jpain10steps.service;

import org.springframework.data.jpa.repository.JpaRepository;

import com.in28minutes.learning.jpa.jpain10steps.entity.User;

public interface UserRepository extends JpaRepository<User, Long>{

}
```
---

### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/UserDaoServiceCommandLineRunner.java

```java
package com.in28minutes.learning.jpa.jpain10steps;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

import com.in28minutes.learning.jpa.jpain10steps.entity.User;
import com.in28minutes.learning.jpa.jpain10steps.service.UserDAOService;

@Component
public class UserDaoServiceCommandLineRunner implements CommandLineRunner{

	private static final Logger log = 
			LoggerFactory.getLogger(UserDaoServiceCommandLineRunner.class);
	
	@Autowired
	private UserDAOService userDaoService;
	
	@Override
	public void run(String... arg0) throws Exception {
		User user = new User("Jack", "Admin");
		//New User is created : User [id=1, name=Jack, role=Admin]
		long insert = userDaoService.insert(user);
		log.info("New User is created : " + user);
	}
}
```
---

### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/UserRepositoryCommandLineRunner.java

```java
package com.in28minutes.learning.jpa.jpain10steps;

import java.util.List;
import java.util.Optional;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

import com.in28minutes.learning.jpa.jpain10steps.entity.User;
import com.in28minutes.learning.jpa.jpain10steps.service.UserRepository;

@Component
public class UserRepositoryCommandLineRunner implements CommandLineRunner{

	private static final Logger log = 
			LoggerFactory.getLogger(UserRepositoryCommandLineRunner.class);
	
	@Autowired
	private UserRepository userRepository;
	
	@Override
	public void run(String... arg0) throws Exception {
		User user = new User("Jill", "Admin");
		userRepository.save(user);
		log.info("New User is created : " + user);
		
		Optional<User> userWithIdOne = userRepository.findById(1L);
		log.info("User is retrived : " + userWithIdOne);

		List<User> users = userRepository.findAll();
		log.info("All Users : " + users);			
	}
	
}
```
---

### /src/main/resources/application.properties

```
spring.jpa.show-sql=true
spring.h2.console.enabled=true
logging.level.org.springframework=debug
```
---

### /src/test/java/com/in28minutes/learning/jpa/jpain10steps/JpaIn10StepsApplicationTests.java

```java
package com.in28minutes.learning.jpa.jpain10steps;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class JpaIn10StepsApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /step-completed.sh

```
java -cp /ProgrammingExcellence/Workspaces/Rithus.com/ListDirectoryContentInGitFormat/bin test.ListDirectoryContentInGitFormat >> $1.md
zip -r $1.zip . -x "target/*" -x ".*/*" -x ".*" -x "*.md" -x "mvn*" -x "*.zip"
git add *; git commit -m "$1"; git push;
```
---
## step25.md

### /in28Minutes/git/getting-started-in-5-steps/junit-in-5-steps/src/com/in28minutes/junit/MyMath.java New

```java
package com.in28minutes.junit;

public class MyMath {
	int sum(int[] numbers) {
		int sum = 0;
		for (int i : numbers) {
			sum += i;
		}
		return sum;
	}
}
```
---

### /in28Minutes/git/getting-started-in-5-steps/junit-in-5-steps/test/com/in28minutes/junit/AssertTest.java New

```java
package com.in28minutes.junit;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertTrue;

import org.junit.Test;

public class AssertTest {

	@Test
	public void test() {
		boolean condn = true;
		assertEquals(true, condn);
		assertTrue(condn);
		// assertFalse(condn);
	}

}
```
---

### /in28Minutes/git/getting-started-in-5-steps/junit-in-5-steps/test/com/in28minutes/junit/MyMathTest.java New

```java
package com.in28minutes.junit;

import static org.junit.Assert.assertEquals;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

public class MyMathTest {
	MyMath myMath = new MyMath();

	@Before
	public void before() {
		System.out.println("Before");
	}

	@After
	public void after() {
		System.out.println("After");
	}

	@BeforeClass
	public static void beforeClass() {
		System.out.println("Before Class");
	}

	@AfterClass
	public static void afterClass() {
		System.out.println("After Class");
	}

	// MyMath.sum
	// 1,2,3 => 6
	@Test
	public void sum_with3numbers() {
		System.out.println("Test1");
		assertEquals(6, myMath.sum(new int[] { 1, 2, 3 }));
	}

	@Test
	public void sum_with1number() {
		System.out.println("Test2");
		assertEquals(3, myMath.sum(new int[] { 3 }));
	}
}
```
---
### /notes.txt Deleted
### /pom.xml Deleted
### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/JpaIn10StepsApplication.java Deleted
### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/UserDaoServiceCommandLineRunner.java Deleted
### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/UserRepositoryCommandLineRunner.java Deleted
### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/entity/User.java Deleted
### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/service/UserDAOService.java Deleted
### /src/main/java/com/in28minutes/learning/jpa/jpain10steps/service/UserRepository.java Deleted
### /src/main/resources/application.properties Deleted
### /src/test/java/com/in28minutes/learning/jpa/jpain10steps/JpaIn10StepsApplicationTests.java Deleted
### /step-completed.sh Deleted

### readme.md


## First 5 Steps in JUnit

- Git Repository - https://github.com/in28minutes/getting-started-in-5-steps
- Pre-requisites - Java & Eclipse - https://www.youtube.com/playlist?list=PLBBog2r6uMCSmMVTW_QmDLyASBvovyAO3
- We will use embedded maven in Eclipse

### Step 1 : What is JUnit and Unit Testing?
 - What is JUnit?
 - What is Unit Testing?
 - Advantages of Unit Testing

### Step 2 : First JUnit Project and Green Bar
 - What is JUnit?
 - First Project with JUnit
 - First JUnit Class
 - No Failure is Success
 - MyMath class with sum method

### Step 3 : First Code and First Unit Test
 - Unit test for the sum method

### Step 4 : Other assert methods
 - assertTrue and assertFalse methods

### Step 5 : Important annotations
  - @Before @After annotations
  - @BeforeClass @AfterClass annotations

## Complete Code Example


### /src/com/in28minutes/junit/MyMath.java

```java
package com.in28minutes.junit;

public class MyMath {
	int sum(int[] numbers) {
		int sum = 0;
		for (int i : numbers) {
			sum += i;
		}
		return sum;
	}
}
```
---

### /test/com/in28minutes/junit/AssertTest.java

```java
package com.in28minutes.junit;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertTrue;

import org.junit.Test;

public class AssertTest {

	@Test
	public void test() {
		boolean condn = true;
		assertEquals(true, condn);
		assertTrue(condn);
		// assertFalse(condn);
	}

}
```
---

### /test/com/in28minutes/junit/MyMathTest.java

```java
package com.in28minutes.junit;

import static org.junit.Assert.assertEquals;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

public class MyMathTest {
	MyMath myMath = new MyMath();

	@Before
	public void before() {
		System.out.println("Before");
	}

	@After
	public void after() {
		System.out.println("After");
	}

	@BeforeClass
	public static void beforeClass() {
		System.out.println("Before Class");
	}

	@AfterClass
	public static void afterClass() {
		System.out.println("After Class");
	}

	// MyMath.sum
	// 1,2,3 => 6
	@Test
	public void sum_with3numbers() {
		System.out.println("Test1");
		assertEquals(6, myMath.sum(new int[] { 1, 2, 3 }));
	}

	@Test
	public void sum_with1number() {
		System.out.println("Test2");
		assertEquals(3, myMath.sum(new int[] { 3 }));
	}
}
```
---
