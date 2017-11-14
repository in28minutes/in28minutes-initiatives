* [Java Web Application in 25 Easy Steps](#java-web-application-in-25-easy-steps)
  * [About in28Minutes](#about-in28minutes)
  * [Github Repository](#github-repository)
  * [Selection of the Wonderful 5-Star Reviews](#selection-of-the-wonderful-5-star-reviews)
    + [Hands-on](#hands-on)
    + [We don't teach frameworks. We teach building applications!](#we-don-t-teach-frameworks-we-teach-building-applications-)
    + [Learn quickly](#learn-quickly)
  * [Step By Step Overview](#step-by-step-overview)
  * [Step By Step Details](#step-by-step-details)
    + [Step 01 : Up and running with a Web Application in Tomcat](#step-01---up-and-running-with-a-web-application-in-tomcat)
    + [Step 02 : First JSP](#step-02---first-jsp)
      - [Notes](#notes)
      - [Snippets](#snippets)
    + [Step 03 : Adding a Get Parameter name](#step-03---adding-a-get-parameter-name)
      - [Notes](#notes-1)
      - [Snippets](#snippets-1)
    + [Step 04 : Adding another Get Parameter Password](#step-04---adding-another-get-parameter-password)
      - [Snippets](#snippets-2)
    + [Step 05 : Let's add a form](#step-05---let-s-add-a-form)
    + [Step 06 : New Form and doPost](#step-06---new-form-and-dopost)
    + [Step 07 : Adding Password and Validation of User Id / Password combination](#step-07---adding-password-and-validation-of-user-id---password-combination)
    + [Step 08 : Adding a TodoService and Todos to welcome page](#step-08---adding-a-todoservice-and-todos-to-welcome-page)
    + [Step 09 : Bit of Refactoring - Packages](#step-09---bit-of-refactoring---packages)
    + [Step 10 : Redirect from One Servlet to another - New TodoServlet.](#step-10---redirect-from-one-servlet-to-another---new-todoservlet)
    + [Step 11 : First JSTL Tag : Using a Loop around todos](#step-11---first-jstl-tag---using-a-loop-around-todos)
    + [Step 12 : Difference between Session and Request Scopes](#step-12---difference-between-session-and-request-scopes)
    + [Step 13 : Add a New Todo](#step-13---add-a-new-todo)
    + [Step 14 : Delete Todo with equals and hashcode methods](#step-14---delete-todo-with-equals-and-hashcode-methods)
    + [Step 15 : Adding webjars for jquery and bootstrap](#step-15---adding-webjars-for-jquery-and-bootstrap)
    + [Step 16 : Missing Step :) We want you to take a break. Nothing in here..](#step-16---missing-step----we-want-you-to-take-a-break-nothing-in-here)
    + [Step 17 : Updating Bootstrap to 3.3.6](#step-17---updating-bootstrap-to-336)
    + [Step 18 : More Refactoring](#step-18---more-refactoring)
    + [Step 19 : Adding a Filter for More Security.](#step-19---adding-a-filter-for-more-security)
    + [Step 20 : Logout](#step-20---logout)
    + [Step 21 : Theory : Understand Maven and Tomcat](#step-21---theory---understand-maven-and-tomcat)
    + [Step 22 : Theory : Servlet LifeCycle](#step-22---theory---servlet-lifecycle)
    + [Step 23 : Theory : Model 1 and Model 2 MVC Architectures](#step-23---theory---model-1-and-model-2-mvc-architectures)
    + [Step 24 : Moving Add Functionality to a New Page.](#step-24---moving-add-functionality-to-a-new-page)
    + [Step 25 : Add Category Field](#step-25---add-category-field)
    + [Step 26 : Format the JSPs better.](#step-26---format-the-jsps-better)
    + [Step 27 : JSP Fragments](#step-27---jsp-fragments)
- [More about in28Minutes](#more-about-in28minutes)
        * [If you loved the course](#if-you-loved-the-course)


## Java Web Application in 25 Easy Steps

Developing your first Java Web Application using JSP and Servlets is fun.

In this course, you will learn the basics developing a Basic Todo Management Application using Java Servlets and JSP with Login and Logout functionalities.

You will build a Dynamic Website using the Core technologies of Java Web Programming. You will understand the basic concepts of Java Web Application Development - HTTP protocol, Request-Response cycle, Java Servlets, JSPs.

## About in28Minutes

Read about what we love, why we create courses and our beliefs - [The in28Minutes Way](https://github.com/in28minutes/in28minutes-initiatives/tree/master/The-in28Minutes-Way)
- 15 Courses
- 100,000 Students

![](images/udemy-total-students.png)

## Github Repository

- https://github.com/in28minutes/JavaWebApplicationStepByStep

## Wonderful 5-Star Reviews

### Hands-on

> The best part of it is the hands-on approach which the author maintained throughout the course as he had promised at the beginning of the lecture. He explains the concepts really well and also makes sure that there is not a single line of code you type without understanding what it really does. It was so engaging that it gets you interested in web development and kinda makes you want to learn more about it.

> I got a working servlet! I got a working website!

### We don't teach frameworks. We teach building applications!

> Simple, yet precise explanation. The course is also enabling in understanding how to use tools like eclipse, maven, tomcat.

> You will learn the concepts of Servlets, JSP, Maven, TomCat, and bit of bootstrap and CSS also. A++++

### Learn quickly

> I can see that you will be able to learn many advanced concepts very quickly and broadly within a short time frame. 

## Step By Step Overview

- Step 01 : Up and running with a Web Application in Tomcat
- Step 02 : First JSP
- Step 03 : Adding a Get Parameter name
- Step 04 : Adding another Get Parameter Password
- Step 05 : Let's add a form
- Step 06 : New Form and doPost
- Step 07 : Adding Password and Validation of User Id / Password combination
- Step 08 : Adding a TodoService and Todos to welcome page
- Step 09 : Bit of Refactoring - Packages
- Step 10 : Redirect from One Servlet to another - New TodoServlet.
- Step 11 : First JSTL Tag : Using a Loop around todos
- Step 12 : Difference between Session and Request Scopes
- Step 13 : Add a New Todo
- Step 14 : Delete Todo with equals and hashcode methods
- Step 15 : Adding webjars for jquery and bootstrap
- Step 16 : Missing Step :) We want you to take a break. Nothing in here..
- Step 17 : Updating Bootstrap to 3.3.6
- Step 18 : More Refactoring
- Step 19 : Adding a Filter for More Security.
- Step 20 : Logout
- Step 21 : Theory : Understand Maven and Tomcat
- Step 22 : Theory : Servlet LifeCycle
- Step 23 : Theory : Model 1 and Model 2 MVC Architectures
- Step 24 : Moving Add Functionality to a New Page.
- Step 25 : Add Category Field
- Step 26 : Format the JSPs better.
- Step 27 : JSP Fragments

## Step By Step Details

### Step 01 : Up and running with a Web Application in Tomcat

You can copy code from 
- [Step 01 on Github Repository](https://github.com/in28minutes/JavaWebApplicationStepByStep/blob/master/Step01.md)

\pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.in28minutes</groupId>
	<artifactId>in28Minutes-first-webapp</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<dependencies>
		<dependency>
			<groupId>javax</groupId>
			<artifactId>javaee-web-api</artifactId>
			<version>6.0</version>
			<scope>provided</scope>
		</dependency>
	</dependencies>

	<build>
		<pluginManagement>
			<plugins>
				<plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.2</version>
					<configuration>
						<verbose>true</verbose>
						<source>1.7</source>
						<target>1.7</target>
						<showWarnings>true</showWarnings>
					</configuration>
				</plugin>
				<plugin>
					<groupId>org.apache.tomcat.maven</groupId>
					<artifactId>tomcat7-maven-plugin</artifactId>
					<version>2.2</version>
					<configuration>
						<path>/</path>
						<contextReloadable>true</contextReloadable>
					</configuration>
				</plugin>
			</plugins>
		</pluginManagement>
	</build>
</project>
```
\src\main\java\webapp\LoginServlet.java
```
package webapp;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/*
 * Browser sends Http Request to Web Server
 * 
 * Code in Web Server => Input:HttpRequest, Output: HttpResponse
 * JEE with Servlets
 * 
 * Web Server responds with Http Response
 */

//Java Platform, Enterprise Edition (Java EE) JEE6

//Servlet is a Java programming language class 
//used to extend the capabilities of servers 
//that host applications accessed by means of 
//a request-response programming model.

//1. extends javax.servlet.http.HttpServlet
//2. @WebServlet(urlPatterns = "/login.do")
//3. doGet(HttpServletRequest request, HttpServletResponse response)
//4. How is the response created?

@WebServlet(urlPatterns = "/login.do")
public class LoginServlet extends HttpServlet {

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
		PrintWriter out = response.getWriter();
		out.println("<html>");
		out.println("<head>");
		out.println("<title>Yahoo!!!!!!!!</title>");
		out.println("</head>");
		out.println("<body>");
		out.println("My First Servlet");
		out.println("</body>");
		out.println("</html>");

	}

}
```
\src\main\webapp\WEB-INF\web.xml
```
<!-- webapp/WEB-INF/web.xml -->
<web-app xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
	version="3.0">

	<display-name>To do List</display-name>

	<welcome-file-list>
		<welcome-file>login.do</welcome-file>
	</welcome-file-list>

</web-app>
```

### Step 02 : First JSP

#### Notes
- Create LoginServlet again
- Redirect to a view - JSP

#### Snippets

\src\main\java\webapp\LoginServlet.java
```
request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
```

\src\main\webapp\WEB-INF\views\login.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
My First JSP!!!
</body>
</html>
```

### Step 03 : Adding a Get Parameter name

#### Notes
- Passing a Request Parameter Name

#### Snippets
\src\main\java\webapp\LoginServlet.java
```
request.setAttribute("name", request.getParameter("name"));
```
\src\main\webapp\WEB-INF\views\login.jsp
```
My First JSP!!! My name is ${name}
```

### Step 04 : Adding another Get Parameter Password

#### Snippets
\src\main\java\webapp\LoginServlet.java
```
		request.setAttribute("password",
		                  request.getParameter("password"));
```
\src\main\webapp\WEB-INF\views\login.jsp
```
My First JSP!!! My name is ${name} and password is ${password}
```
### Step 05 : Let's add a form
\src\main\java\webapp\LoginServlet.java
```
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response)
		throws IOException, ServletException {
	request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
}
```
\\src\main\webapp\WEB-INF\views\login.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
	<form action="/login.do" method="POST">
		Name : <input type="text" /> <input type="submit" />
	</form>
</body>
</html>
```
\src\main\webapp\WEB-INF\views\welcome.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
Welcome ${name}
</body>
</html>
```
### Step 06 : New Form and doPost
\src\main\java\webapp\LoginServlet.java
```
@Override
protected void doPost(HttpServletRequest request, HttpServletResponse response)
		throws IOException, ServletException {
	request.setAttribute("name", request.getParameter("name"));
	request.getRequestDispatcher("/WEB-INF/views/welcome.jsp").forward(request, response);
}
```
\src\main\webapp\WEB-INF\views\welcome.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
Welcome ${name}
</body>
</html>
```

### Step 07 : Adding Password and Validation of User Id / Password combination
\src\main\java\webapp\LoginService.java
```
package webapp;

public class LoginService {
	public boolean validateUser(String user, String password) {
		return user.equalsIgnoreCase("in28Minutes") && password.equals("dummy");
	}

}
```
\src\main\java\webapp\LoginServlet.java
```
@Override
protected void doPost(HttpServletRequest request, HttpServletResponse response)
		throws IOException, ServletException {
	String name = request.getParameter("name");
	String password = request.getParameter("password");

	boolean isValidUser = service.validateUser(name, password);

	if (isValidUser) {
		request.setAttribute("name", name);
		request.getRequestDispatcher("/WEB-INF/views/welcome.jsp").forward(request, response);
	} else {
		request.setAttribute("errorMessage", "Invalid Credentials!!");
		request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
	}
}
```
\\src\main\webapp\WEB-INF\views\login.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
	<p><font color="red">${errorMessage}</font></p>
	<form action="/login.do" method="POST">
		Name : <input name="name" type="text" /> Password : <input name="password" type="password" /> <input type="submit" />
	</form>
</body>
</html>
```

### Step 08 : Adding a TodoService and Todos to welcome page

\src\main\java\webapp\LoginServlet.java
```
private LoginService service = new LoginService();
private TodoService todoService = new TodoService();

@Override
protected void doPost(HttpServletRequest request, HttpServletResponse response)
		throws IOException, ServletException {
	String name = request.getParameter("name");
	String password = request.getParameter("password");

	boolean isValidUser = service.validateUser(name, password);

	if (isValidUser) {
		request.setAttribute("name", name);
		request.setAttribute("todos", 
				todoService.retrieveTodos());
		request.getRequestDispatcher("/WEB-INF/views/welcome.jsp").forward(request, response);
	} else {
		request.setAttribute("errorMessage", "Invalid Credentials!!");
		request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
	}
}

```
\src\main\java\webapp\todo\Todo.java
```
package webapp.todo;

public class Todo {

	public Todo(String name) {
		super();
		this.name = name;
	}

	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public String toString() {
		return "Todo [name=" + name + "]";
	}
}
```
\src\main\java\webapp\todo\TodoService.java
```
package webapp.todo;

import java.util.ArrayList;
import java.util.List;

public class TodoService {
	private static List<Todo> todos = new ArrayList();

	static {
		todos.add(new Todo("Learn Web Application"));
		todos.add(new Todo("Learn Spring"));
		todos.add(new Todo("Learn Spring MVC"));
	}

	public List<Todo> retrieveTodos() {
		return todos;
	}
}
```
\src\main\webapp\WEB-INF\views\welcome.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
<H1>Welcome ${name}</H2>
<div>
Your Todos are
${todos}
</div>
</body>
</html>
```
### Step 09 : Bit of Refactoring - Packages
- Basic Refactoring
### Step 10 : Redirect from One Servlet to another - New TodoServlet.

src\main\java\in28minutes\login\LoginServlet.java
```
@Override
protected void doPost(HttpServletRequest request, HttpServletResponse response)
		throws IOException, ServletException {
	String name = request.getParameter("name");
	String password = request.getParameter("password");

	boolean isValidUser = service.validateUser(name, password);

	if (isValidUser) {
		response.sendRedirect("/todo.do");
	} else {
		request.setAttribute("errorMessage", "Invalid Credentials!!");
		request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
	}
}

```

src\main\java\in28minutes\todo\TodoServlet.java
```
package in28minutes.todo;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = "/todo.do")
public class TodoServlet extends HttpServlet {

	private static final long serialVersionUID = 1L;
	private TodoService todoService = new TodoService();

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws IOException, ServletException {
		request.setAttribute("todos", todoService.retrieveTodos());
		request.getRequestDispatcher("/WEB-INF/views/todo.jsp").forward(request, response);
	}
}
```
src\main\webapp\WEB-INF\views\todo.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
<H1>Welcome ${name}</H2>
<div>
Your Todos are
${todos}
</div>
</body>
</html>
```
### Step 11 : First JSTL Tag : Using a Loop around todos
pom.xml
```
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
```

src\main\webapp\WEB-INF\views\todo.jsp
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
<H1>Welcome ${name}</H2>
<div>
Your Todos are
<ol>
<c:forEach items="${todos}" var="todo">
   <li>${todo.name}</li>
</c:forEach>
</ol>
</div>
</body>
</html>
```
### Step 12 : Difference between Session and Request Scopes
- Session Scope 
 - Valid for the entire session of a user. 
 - Data in session can be shared between multiple requests from the same user.
- Request Scope
 - Only valid for the duration of the HTTPRequest

> Recommendation : Keep number of objects in a session to a bare minimum.

> Recommendation : Clean up objects in session when they are not needed anymore.

### Step 13 : Add a New Todo
### Step 14 : Delete Todo with equals and hashcode methods
### Step 15 : Adding webjars for jquery and bootstrap
### Step 16 : Missing Step :) We want you to take a break. Nothing in here..
### Step 17 : Updating Bootstrap to 3.3.6

Bootstrap Sample Page
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<!DOCTYPE html>
<html>
<head>
<title>Todos</title>
<link href="webjars/bootstrap/3.3.6/css/bootstrap.min.css"
	rel="stylesheet">

<style>
	.footer {
		position: absolute;
		bottom: 0;
		width: 100%;
		height: 60px;
		background-color: #f5f5f5;
	}
</style>
</head>

<body>

	<nav class="navbar navbar-default">

		<a href="/" class="navbar-brand">Brand</a>

		<ul class="nav navbar-nav">
			<li class="active"><a href="#">Home</a></li>
			<li><a href="/todo.do">Todos</a></li>
			<li><a href="http://www.in28minutes.com">In28Minutes</a></li>
		</ul>

		<ul class="nav navbar-nav navbar-right">
			<li><a href="/login.do">Login</a></li>
		</ul>

	</nav>

	<div class="container">
		<H1>Heading</H1>
		Body of the Page
	</div>

	<footer class="footer">
		<p>footer content</p>
	</footer>

	<script src="webjars/jquery/1.9.1/jquery.min.js"></script>
	<script src="webjars/bootstrap/3.3.6/js/bootstrap.min.js"></script>

</body>

</html>
```

### Step 18 : More Refactoring
### Step 19 : Adding a Filter for More Security.
### Step 20 : Logout
### Step 21 : Theory : Understand Maven and Tomcat
### Step 22 : Theory : Servlet LifeCycle
### Step 23 : Theory : Model 1 and Model 2 MVC Architectures
### Step 24 : Moving Add Functionality to a New Page.
### Step 25 : Add Category Field
### Step 26 : Format the JSPs better.
### Step 27 : JSP Fragments

# More about in28Minutes

We would love to hear your thoughts.  

##### If you loved the course

#in28Minutes #ImLearningIn28Minutes #ImLovingIn28Minutes 

Share on Twitter - https://twitter.com/home?status=Having%20a%20great%20time!%20%0A%20%23in28Minutes%20%23ImLearningIn28Minutes

![](images/in28Minutes-Java-Course-Roadmap.png)

Good Luck and Keep Learning in28Minutes
- Linked In : https://www.linkedin.com/in/rangakaranam/​
- Facebook  : https://www.facebook.com/in28Minutes​
- Twitter   : https://twitter.com/in28Minutes​
- YouTube   : https://www.youtube.com/rithustutorials​
​
To find out more about our courses and get special offers, visit http://www.in28minutes.com