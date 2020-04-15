# Debugging Problems with Full Stack 

## First Thing : Many problems can cause this error

> Access to XMLHttpRequest at 'URL' from origin 'http://localhost:4200' has been blocked by CORS policy: 

Two kind of messages
- MESSAGE 1 : No 'Access-Control-Allow-Origin' header is present on the requested resource.
- MESSAGE 2 : Response to preflight request doesn't pass access control check: It does not have HTTP ok status.

If you have Message 2, high probability that the problem is with Backend API Spring Security Configuration.

### Frontend problems
- Your URL is wrong. 
- You are not sending authorization headers.
- The authorization headers do not match.

### Backend API problems
- @CrossOrigin is not present on the right controller.
- Your Spring Security configuration is not in Component Scan. SpringSecurityConfigurationBasicAuth is in a subpackage of the package which contains RestfulWebServicesApplication class.


## Basic Authentication Problems

### Is your backend API configured right?

Are you able to send a request to http://localhost:8080/hello-world/path-variable/Ranga or to the todo urls with username = 'in28minutes' and password = 'dummy' directly from your browser or REST API client (without using your fronend application).

![](images/full-stack-01-basic-auth.png)

Check your spring security configuration of username and password in application.properties:

```
spring.security.user.name=in28minutes
spring.security.user.password=dummy
```

Is your SpringSecurityConfigurationBasicAuth file configured right? Is it in a subpackage of the package which contains RestfulWebServicesApplication class?

```
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SpringSecurityConfigurationBasicAuth extends WebSecurityConfigurerAdapter{
	
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
		.csrf().disable()	
		.authorizeRequests()
		.antMatchers(HttpMethod.OPTIONS,"/**").permitAll()
				.anyRequest().authenticated()
				.and()
			//.formLogin().and()
			.httpBasic();
	}
}
```


### Is your front end code sending the right details?

Open notepad and Note down the URL and the headers from the browser network tab.
	- URL - ??
	- Authorization Header Name - ??
	- Authorization Header Value - ??

![](images/full-stack-02-network-01.png)
![](images/full-stack-02-network-02.png)
![](images/full-stack-02-network-03.png)

Open REST API client. Create a new request using values noted above. Are you able to execute the request successfully?

![](images/full-stack-01-basic-auth.png)


Important things to check in code below:
- SPACE after Basic: There SHOULD be a SPACE after Basic : 'Basic ' in ('Basic ' + window.btoa(`${username}:${password}`))


Hard Coded Code

```
let username = 'in28minutes'
let password = 'dummy'
let basicAuthHeaderString = 'Basic ' + window.btoa(`${username}:${password}`);
{ Authorization: basicAuthHeaderString }

```

Picking up username from login screen and using basicauth url for authentication.

```
'Basic ' + window.btoa(username + ':' + password);

{
    Authorization: basicAuthHeaderString
  }

 `http://localhost:8080/basicauth`,
```

Compare your code against working
- Angular - https://github.com/in28minutes/full-stack-with-angular-and-spring-boot/blob/master/Backup-18-Working-App-With-Basic-Authentication-After-Enabling-HttpInterceptor.md#frontendtodosrcapperrorerrorcomponentts
- React - https://github.com/in28minutes/full-stack-with-react-and-spring-boot/blob/master/0001-0365-Basic-Auth-Done.md

### Q&A Details Update

Debugging this problem is tough. So, please provide us with as many details as possible:
- What was your last working state?
- What are the code changes that you made since then?
- Screenshots of all the above checks with details for URL, Authorization Header name and value



## JWT Authentication Problems

Check your JWT package imports against this
https://github.com/in28minutes/full-stack-with-angular-and-spring-boot/blob/master/Backup-20-Working-With-JWT-Authentication.md#restful-web-servicessrcmainjavacomin28minutesrestwebservicesrestfulwebservicesjwtjwtinmemoryuserdetailsservicejava

Working code backup
- Angular - https://github.com/in28minutes/full-stack-with-angular-and-spring-boot/blob/master/Backup-20-Working-With-JWT-Authentication.md#frontendtodosrcapploginlogincomponentts
- React - https://github.com/in28minutes/full-stack-with-react-and-spring-boot/blob/master/0001-0373-JWT-Done.md

### Is your backend API configured right?

Take a backup and delete your basic auth package.

Check your JWT package imports against this
https://github.com/in28minutes/full-stack-with-angular-and-spring-boot/blob/master/Backup-20-Working-With-JWT-Authentication.md#restful-web-servicessrcmainjavacomin28minutesrestwebservicesrestfulwebservicesjwtjwtinmemoryuserdetailsservicejava

Here are some of the imports where there could be a conflict.
```
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.util.function.Function;
import io.jsonwebtoken.Clock;
import java.util.Map;
import java.util.Date;
import org.springframework.security.core.AuthenticationException;
import com.fasterxml.jackson.annotation.JsonIgnore;
import java.util.Collection;
import java.util.List;
import java.util.Objects;
```

Do you have these in your application.properties file?

```
jwt.signing.key.secret=mySecret
jwt.get.token.uri=/authenticate
jwt.refresh.token.uri=/refresh
jwt.http.request.header=Authorization
jwt.token.expiration.in.seconds=604800
```

Remember that these values are NOT used in JWT
```
spring.security.user.name=in28minutes
spring.security.user.password=dummy
```

This is where the user details come from
```
@Service
public class JwtInMemoryUserDetailsService implements UserDetailsService {

  static List<JwtUserDetails> inMemoryUserList = new ArrayList<>();

  static {
    inMemoryUserList.add(new JwtUserDetails(1L, "in28minutes",
        "$2a$10$3zHzb.Npv1hfZbLEU5qsdOju/tk2je6W6PnNnY.c1ujWPcZh4PL6e", "ROLE_USER_2"));
```



Are you able to send a POST request to http://localhost:8080/authenticate and get with
```
{
  "username":"in28minutes",
  "password":"dummy"
}
```
And get a token back
```
{
"token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJyYW5nYSIsImV4cCI6MTU0MjQ3MjA3NCwiaWF0IjoxNTQxODY3Mjc0fQ.kD6UJQyxjSPMzAhoTJRr-Z5UL-FfgsyxbdseWQvk0fLi7eVXAKhBkWfj06SwH43sY_ZWBEeLuxaE09szTboefw"
}
```

Are you able to use the Bearer token Authorization header and send GET request to http://localhost:8080/users/in28minutes/todos ?

### Is your front end code sending the right details?

- Open notepad and Note down the URL and the headers from the browser network tab for the authenticate request.
	- URL - ??
	- Body Content - ??
![](images/full-stack-02-network-01.png)
![](images/full-stack-02-network-02.png)
![](images/full-stack-02-network-03.png)


- Open REST API client. Create a new request using values noted above. Are you able to execute the request successfully?
- If you are able to then repeat the same thing with the hello world request.
	- URL - ??
	- Authorization Header Name - ??
	- Authorization Header Value - ??

![](images/full-stack-04-jwt-01.png)
![](images/full-stack-04-jwt-02.png)

- If you are not successful, there is a problem with your front end code.
- Post screenshots and values for URL, Body Content, Headers and Header values in the Q&A.

Important things to check in code:
Are you using right syntax:
```
{
        username,
        password
      }

```

Is the name of the token and the value right? Are you using ticks instead of quotes?

```
`Bearer ${data.token}`
```

### Q&A Details Update

Debugging this problem is tough. So, please provide us with as many details as possible:
- What was your last working state?
- What are the code changes that you made since then?
- Screenshots of all the above checks with details for URL, Authorization Header name and value


## Other Imports

```
import java.util.HashMap;
import java.io.IOException;
import java.io.Serializable;
import java.util.ArrayList;


import io.jsonwebtoken.Claims;
import io.jsonwebtoken.impl.DefaultClock;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;


import java.util.Optional;
import javax.servlet.FilterChain;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.ServletException;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.BadCredentialsException;
import org.springframework.security.authentication.DisabledException;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.builders.WebSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;

import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.security.web.AuthenticationEntryPoint;
import org.springframework.stereotype.Component;
import org.springframework.stereotype.Service;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.filter.OncePerRequestFilter;
```