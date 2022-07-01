# All Code from In28minutes

# Spring Boot Web Application

<!---
Current Directory : /Users/rangakaranam/Ranga/git/00.courses/spring-boot-master-class/02.Spring-Boot-Web-Application-V2
-->

## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.0.0-M3</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.in28minutes.springboot</groupId>
	<artifactId>myfirstwebapp</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>myfirstwebapp</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>18</java.version>
	</properties>
	<dependencies>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		
<!--		<dependency>
			<groupId>com.h2database</groupId>
			<artifactId>h2</artifactId>
			<scope>runtime</scope>
		</dependency> -->
		
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
		</dependency>
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-validation</artifactId>
		</dependency>

		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>jakarta.servlet.jsp.jstl</groupId>
			<artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
		</dependency>
		
		<dependency>
			<groupId>org.eclipse.jetty</groupId>
			<artifactId>glassfish-jstl</artifactId>
		</dependency>
		
		<dependency>
			<groupId>org.webjars</groupId>
			<artifactId>bootstrap</artifactId>
			<version>5.1.3</version>
		</dependency>

		<dependency>
			<groupId>org.webjars</groupId>
			<artifactId>jquery</artifactId>
			<version>3.6.0</version>
		</dependency>
		
		<dependency>
			<groupId>org.webjars</groupId>
			<artifactId>bootstrap-datepicker</artifactId>
			<version>1.9.0</version>
		</dependency>

		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
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

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/MyfirstwebappApplication.java

```java
package com.in28minutes.springboot.myfirstwebapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyfirstwebappApplication {

	public static void main(String[] args) {
		SpringApplication.run(MyfirstwebappApplication.class, args);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/hello/SayHelloController.java

```java
package com.in28minutes.springboot.myfirstwebapp.hello;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class SayHelloController {
	
	//"say-hello" => "Hello! What are you learning today?"
	
	//say-hello
	// http://localhost:8080/say-hello
	@RequestMapping("say-hello")
	@ResponseBody
	public String sayHello() {
		return "Hello! What are you learning today?";
	}
	
	@RequestMapping("say-hello-html")
	@ResponseBody
	public String sayHelloHtml() {
		StringBuffer sb = new StringBuffer();
		sb.append("<html>");
		sb.append("<head>");
		sb.append("<title> My First HTML Page - Changed</title>");
		sb.append("</head>");
		sb.append("<body>");
		sb.append("My first html page with body - Changed");
		sb.append("</body>");
		sb.append("</html>");
		
		return sb.toString();
	}
	
	//
	// "say-hello-jsp" => sayHello.jsp 
	// /src/main/resources/META-INF/resources/WEB-INF/jsp/sayHello.jsp
	// /src/main/resources/META-INF/resources/WEB-INF/jsp/welcome.jsp
	// /src/main/resources/META-INF/resources/WEB-INF/jsp/login.jsp
	// /src/main/resources/META-INF/resources/WEB-INF/jsp/todos.jsp
	@RequestMapping("say-hello-jsp")
	public String sayHelloJsp() {
		return "sayHello";
	}
}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/login/WelcomeController.java

```java
package com.in28minutes.springboot.myfirstwebapp.login;

import org.springframework.security.core.Authentication;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.SessionAttributes;

@Controller
@SessionAttributes("name")
public class WelcomeController {

	@RequestMapping(value="/",method = RequestMethod.GET)
	public String gotoWelcomePage(ModelMap model) {
		model.put("name", getLoggedinUsername());
		return "welcome";
	}
	
	private String getLoggedinUsername() {
		Authentication authentication = 
				SecurityContextHolder.getContext().getAuthentication();
		return authentication.getName();
	}
}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/security/SpringSecurityConfiguration.java

```java
package com.in28minutes.springboot.myfirstwebapp.security;

import static org.springframework.security.config.Customizer.withDefaults;

import java.util.function.Function;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SpringSecurityConfiguration {
	//LDAP or Database
	//In Memory 
	
	//InMemoryUserDetailsManager
	//InMemoryUserDetailsManager(UserDetails... users)
	
	@Bean
	public InMemoryUserDetailsManager createUserDetailsManager() {
		
		UserDetails userDetails1 = createNewUser("in28minutes", "dummy");
		UserDetails userDetails2 = createNewUser("ranga", "dummydummy");
		
		return new InMemoryUserDetailsManager(userDetails1, userDetails2);
	}

	private UserDetails createNewUser(String username, String password) {
		Function<String, String> passwordEncoder
		= input -> passwordEncoder().encode(input);

		UserDetails userDetails = User.builder()
									.passwordEncoder(passwordEncoder)
									.username(username)
									.password(password)
									.roles("USER","ADMIN")
									.build();
		return userDetails;
	}

	@Bean
	public PasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}
	
	//All URLs are protected
	//A login form is shown for unauthorized requests
	//CSRF disable
	//Frames
	
	@Bean
	public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
		
		http.authorizeHttpRequests(
				auth -> auth.anyRequest().authenticated());
		http.formLogin(withDefaults());
		
		http.csrf().disable();
		http.headers().frameOptions().disable();
		
		return http.build();
	}
	
	
	
	
	
}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/todo/Todo.java

```java
package com.in28minutes.springboot.myfirstwebapp.todo;

import java.time.LocalDate;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Id;
import jakarta.validation.constraints.Size;

//Database (MySQL) 
//Static List of todos => Database (H2, MySQL)

//JPA
// Bean -> Database Table

@Entity
public class Todo {

	public Todo() {
		
	}
	
	public Todo(int id, String username, String description, LocalDate targetDate, boolean done) {
		super();
		this.id = id;
		this.username = username;
		this.description = description;
		this.targetDate = targetDate;
		this.done = done;
	}

	@Id
	@GeneratedValue
	private int id;

	private String username;
	
	@Size(min=10, message="Enter atleast 10 characters")
	private String description;
	private LocalDate targetDate;
	private boolean done;

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getUsername() {
		return username;
	}

	public void setUsername(String username) {
		this.username = username;
	}

	public String getDescription() {
		return description;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	public LocalDate getTargetDate() {
		return targetDate;
	}

	public void setTargetDate(LocalDate targetDate) {
		this.targetDate = targetDate;
	}

	public boolean isDone() {
		return done;
	}

	public void setDone(boolean done) {
		this.done = done;
	}

	@Override
	public String toString() {
		return "Todo [id=" + id + ", username=" + username + ", description=" + description + ", targetDate="
				+ targetDate + ", done=" + done + "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/todo/TodoController.java

```java
package com.in28minutes.springboot.myfirstwebapp.todo;

import java.time.LocalDate;
import java.util.List;

import org.springframework.security.core.Authentication;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.SessionAttributes;

import jakarta.validation.Valid;

//@Controller
@SessionAttributes("name")
public class TodoController {
	
	public TodoController(TodoService todoService) {
		super();
		this.todoService = todoService;
	}

	private TodoService todoService;
		
	
	@RequestMapping("list-todos")
	public String listAllTodos(ModelMap model) {
		String username = getLoggedInUsername(model);
		List<Todo> todos = todoService.findByUsername(username);
		model.addAttribute("todos", todos);
		
		return "listTodos";
	}

	//GET, POST
	@RequestMapping(value="add-todo", method = RequestMethod.GET)
	public String showNewTodoPage(ModelMap model) {
		String username = getLoggedInUsername(model);
		Todo todo = new Todo(0, username, "", LocalDate.now().plusYears(1), false);
		model.put("todo", todo);
		return "todo";
	}

	@RequestMapping(value="add-todo", method = RequestMethod.POST)
	public String addNewTodo(ModelMap model, @Valid Todo todo, BindingResult result) {
		
		if(result.hasErrors()) {
			return "todo";
		}
		
		String username = getLoggedInUsername(model);
		todoService.addTodo(username, todo.getDescription(), 
				LocalDate.now().plusYears(1), false);
		return "redirect:list-todos";
	}

	@RequestMapping("delete-todo")
	public String deleteTodo(@RequestParam int id) {
		//Delete todo
		
		todoService.deleteById(id);
		return "redirect:list-todos";
		
	}

	@RequestMapping(value="update-todo", method = RequestMethod.GET)
	public String showUpdateTodoPage(@RequestParam int id, ModelMap model) {
		Todo todo = todoService.findById(id);
		model.addAttribute("todo", todo);
		return "todo";
	}

	@RequestMapping(value="update-todo", method = RequestMethod.POST)
	public String updateTodo(ModelMap model, @Valid Todo todo, BindingResult result) {
		
		if(result.hasErrors()) {
			return "todo";
		}
		
		String username = getLoggedInUsername(model);
		todo.setUsername(username);
		todoService.updateTodo(todo);
		return "redirect:list-todos";
	}

	private String getLoggedInUsername(ModelMap model) {
		Authentication authentication = 
				SecurityContextHolder.getContext().getAuthentication();
		return authentication.getName();
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/todo/TodoControllerJpa.java

```java
package com.in28minutes.springboot.myfirstwebapp.todo;

import java.time.LocalDate;
import java.util.List;

import org.springframework.security.core.Authentication;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.SessionAttributes;

import jakarta.validation.Valid;

@Controller
@SessionAttributes("name")
public class TodoControllerJpa {
	
	public TodoControllerJpa(TodoRepository todoRepository) {
		super();
		this.todoRepository = todoRepository;
	}

	private TodoRepository todoRepository;
			
	@RequestMapping("list-todos")
	public String listAllTodos(ModelMap model) {
		String username = getLoggedInUsername(model);
				
		List<Todo> todos = todoRepository.findByUsername(username);
		model.addAttribute("todos", todos);
		
		return "listTodos";
	}

	//GET, POST
	@RequestMapping(value="add-todo", method = RequestMethod.GET)
	public String showNewTodoPage(ModelMap model) {
		String username = getLoggedInUsername(model);
		Todo todo = new Todo(0, username, "", LocalDate.now().plusYears(1), false);
		model.put("todo", todo);
		return "todo";
	}

	@RequestMapping(value="add-todo", method = RequestMethod.POST)
	public String addNewTodo(ModelMap model, @Valid Todo todo, BindingResult result) {
		
		if(result.hasErrors()) {
			return "todo";
		}
		
		String username = getLoggedInUsername(model);
		todo.setUsername(username);
		todoRepository.save(todo);
//		todoService.addTodo(username, todo.getDescription(), 
//				todo.getTargetDate(), todo.isDone());
		return "redirect:list-todos";
	}

	@RequestMapping("delete-todo")
	public String deleteTodo(@RequestParam int id) {
		//Delete todo
		todoRepository.deleteById(id);
		return "redirect:list-todos";
		
	}

	@RequestMapping(value="update-todo", method = RequestMethod.GET)
	public String showUpdateTodoPage(@RequestParam int id, ModelMap model) {
		Todo todo = todoRepository.findById(id).get();
		model.addAttribute("todo", todo);
		return "todo";
	}

	@RequestMapping(value="update-todo", method = RequestMethod.POST)
	public String updateTodo(ModelMap model, @Valid Todo todo, BindingResult result) {
		
		if(result.hasErrors()) {
			return "todo";
		}
		
		String username = getLoggedInUsername(model);
		todo.setUsername(username);
		todoRepository.save(todo);
		return "redirect:list-todos";
	}

	private String getLoggedInUsername(ModelMap model) {
		Authentication authentication = 
				SecurityContextHolder.getContext().getAuthentication();
		return authentication.getName();
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/todo/TodoRepository.java

```java
package com.in28minutes.springboot.myfirstwebapp.todo;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;

public interface TodoRepository extends JpaRepository<Todo, Integer>{
	public List<Todo> findByUsername(String username);
}
```
---

### /src/main/java/com/in28minutes/springboot/myfirstwebapp/todo/TodoService.java

```java
package com.in28minutes.springboot.myfirstwebapp.todo;

import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

import org.springframework.stereotype.Service;

import jakarta.validation.Valid;

@Service
public class TodoService {
	
	private static List<Todo> todos = new ArrayList<>();
	
	private static int todosCount = 0;
	
	static {
		todos.add(new Todo(++todosCount, "in28minutes","Get AWS Certified 1", 
							LocalDate.now().plusYears(1), false ));
		todos.add(new Todo(++todosCount, "in28minutes","Learn DevOps 1", 
				LocalDate.now().plusYears(2), false ));
		todos.add(new Todo(++todosCount, "in28minutes","Learn Full Stack Development 1", 
				LocalDate.now().plusYears(3), false ));
	}
	
	public List<Todo> findByUsername(String username){
		Predicate<? super Todo> predicate = 
				todo -> todo.getUsername().equalsIgnoreCase(username);
		return todos.stream().filter(predicate).toList();
	}
	
	public void addTodo(String username, String description, LocalDate targetDate, boolean done) {
		Todo todo = new Todo(++todosCount,username,description,targetDate,done);
		todos.add(todo);
	}
	
	public void deleteById(int id) {
		//todo.getId() == id
		// todo -> todo.getId() == id
		Predicate<? super Todo> predicate = todo -> todo.getId() == id;
		todos.removeIf(predicate);
	}

	public Todo findById(int id) {
		Predicate<? super Todo> predicate = todo -> todo.getId() == id;
		Todo todo = todos.stream().filter(predicate).findFirst().get();
		return todo;
	}

	public void updateTodo(@Valid Todo todo) {
		deleteById(todo.getId());
		todos.add(todo);
	}
}
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/common/footer.jspf

```
<script src="webjars/bootstrap/5.1.3/js/bootstrap.min.js"></script>
		<script src="webjars/jquery/3.6.0/jquery.min.js"></script>
		<script src="webjars/bootstrap-datepicker/1.9.0/js/bootstrap-datepicker.min.js"></script>
						
	</body>
</html>
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/common/header.jspf

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>


<html>
	<head>
		<link href="webjars/bootstrap/5.1.3/css/bootstrap.min.css" rel="stylesheet" >
		<link href="webjars/bootstrap-datepicker/1.9.0/css/bootstrap-datepicker.standalone.min.css" rel="stylesheet" >
		
		<title>Manage Your Todos</title>		
	</head>
	<body>
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/common/navigation.jspf

```
<nav class="navbar navbar-expand-md navbar-light bg-light mb-3 p-1">
	<a class="navbar-brand m-1" href="https://courses.in28minutes.com">in28minutes</a>
	<div class="collapse navbar-collapse">
		<ul class="navbar-nav">
			<li class="nav-item"><a class="nav-link" href="/">Home</a></li>
			<li class="nav-item"><a class="nav-link" href="/list-todos">Todos</a></li>
		</ul>
	</div>
	<ul class="navbar-nav">
		<li class="nav-item"><a class="nav-link" href="/logout">Logout</a></li>
	</ul>	
</nav>
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/listTodos.jsp

```
<%@ include file="common/header.jspf" %>
<%@ include file="common/navigation.jspf" %>	
<div class="container">
	<h1>Your Todos</h1>
	<table class="table">
		<thead>
			<tr>
				<th>Description</th>
				<th>Target Date</th>
				<th>Is Done?</th>
				<th></th>
				<th></th>
			</tr>
		</thead>
		<tbody>		
			<c:forEach items="${todos}" var="todo">
				<tr>
					<td>${todo.description}</td>
					<td>${todo.targetDate}</td>
					<td>${todo.done}</td>
					<td> <a href="delete-todo?id=${todo.id}" class="btn btn-warning">Delete</a>   </td>
					<td> <a href="update-todo?id=${todo.id}" class="btn btn-success">Update</a>   </td>
				</tr>
			</c:forEach>
		</tbody>
	</table>
	<a href="add-todo" class="btn btn-success">Add Todo</a>
</div>

<%@ include file="common/footer.jspf" %>
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/sayHello.jsp

```
<html>
	<head>
		<title> My first HTML Page - JSP</title>
	</head>
	<body>
		<h1>Heading 1</h1>
		<h2>Heading 2</h2>
		
		My first html page with body - JSP
	</body>
</html>
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/todo.jsp

```
<%@ include file="common/header.jspf" %>
<%@ include file="common/navigation.jspf" %>	

<div class="container">
	
	<h1>Enter Todo Details</h1>
	
	<form:form method="post" modelAttribute="todo">

		<fieldset class="mb-3">				
			<form:label path="description">Description</form:label>
			<form:input type="text" path="description" required="required"/>
			<form:errors path="description" cssClass="text-warning"/>
		</fieldset>

		<fieldset class="mb-3">				
			<form:label path="targetDate">Target Date</form:label>
			<form:input type="text" path="targetDate" required="required"/>
			<form:errors path="targetDate" cssClass="text-warning"/>
		</fieldset>

		
		<form:input type="hidden" path="id"/>

		<form:input type="hidden" path="done"/>

		<input type="submit" class="btn btn-success"/>
	
	</form:form>
	
</div>

<%@ include file="common/footer.jspf" %>

<script type="text/javascript">
	$('#targetDate').datepicker({
	    format: 'yyyy-mm-dd'
	});
</script>
```
---

### /src/main/resources/META-INF/resources/WEB-INF/jsp/welcome.jsp

```
<%@ include file="common/header.jspf" %>
<%@ include file="common/navigation.jspf" %>	

<div class="container">
	<h1>Welcome ${name}</h1>
	<a href="list-todos">Manage</a> your todos
</div>

<%@ include file="common/footer.jspf" %>
```
---

### /src/main/resources/application.properties

```properties
#server.port=8081
#sayHello.jsp
#/WEB-INF/jsp/sayHello.jsp

# /WEB-INF/jsp/login.jsp => View Resolver
spring.mvc.view.prefix=/WEB-INF/jsp/
spring.mvc.view.suffix=.jsp
logging.level.org.springframework=info
logging.level.com.in28minutes.springboot.myfirstwebapp=info

spring.mvc.format.date=yyyy-MM-dd

#spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.defer-datasource-initialization=true

spring.datasource.url=jdbc:mysql://localhost:3306/todos
spring.datasource.username=todos-user
spring.datasource.password=dummytodos
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

spring.jpa.hibernate.ddl-auto=update

#/connect todos-user@localhost:3306
#docker run --detach 
#--env MYSQL_ROOT_PASSWORD=dummypassword 
#--env MYSQL_USER=todos-user 
#--env MYSQL_PASSWORD=dummytodos 
#--env MYSQL_DATABASE=todos 
#--name mysql 
#--publish 3306:3306 
#mysql:8-oracle
```
---

### /src/main/resources/data.sql

```
insert into todo (ID, USERNAME, DESCRIPTION, TARGET_DATE, DONE)
values(10001,'in28minutes', 'Get AWS Certified', CURRENT_DATE(), false);

insert into todo (ID, USERNAME, DESCRIPTION, TARGET_DATE, DONE)
values(10002,'in28minutes', 'Get Azure Certified', CURRENT_DATE(), false);

insert into todo (ID, USERNAME, DESCRIPTION, TARGET_DATE, DONE)
values(10003,'in28minutes', 'Get GCP Certified', CURRENT_DATE(), false);

insert into todo (ID, USERNAME, DESCRIPTION, TARGET_DATE, DONE)
values(10004,'in28minutes', 'Learn DevOps', CURRENT_DATE(), false);
```
---

### /src/test/java/com/in28minutes/springboot/myfirstwebapp/MyfirstwebappApplicationTests.java

```java
package com.in28minutes.springboot.myfirstwebapp;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class MyfirstwebappApplicationTests {

	@Test
	void contextLoads() {
	}

}
```
---


# Spring Boot REST API (Advanced)

<!---
Current Directory : /Users/rangakaranam/Ranga/git/00.courses/spring-boot-master-class/05.Spring-Boot-Advanced-V2
-->

## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.0.0-M3</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.in28minutes.springboot</groupId>
	<artifactId>first-rest-api</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>first-rest-api</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-rest</artifactId>
		</dependency>
		
		<dependency>
			<groupId>com.h2database</groupId>
			<artifactId>h2</artifactId>
			<scope>runtime</scope>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
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

### /src/main/java/com/in28minutes/springboot/firstrestapi/FirstRestApiApplication.java

```java
package com.in28minutes.springboot.firstrestapi;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class FirstRestApiApplication {

	public static void main(String[] args) {
		SpringApplication.run(FirstRestApiApplication.class, args);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/helloworld/HelloWorldBean.java

```java
package com.in28minutes.springboot.firstrestapi.helloworld;

public class HelloWorldBean {

	public HelloWorldBean(String message) {
		super();
		this.message = message;
	}

	private String message;

	public String getMessage() {
		return message;
	}

	@Override
	public String toString() {
		return "HelloWorldBean [message=" + message + "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/helloworld/HelloWorldResource.java

```java
package com.in28minutes.springboot.firstrestapi.helloworld;

import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

//@Controller
@RestController
public class HelloWorldResource {
	// /hello-world => "Hello World"
	
	@RequestMapping("/hello-world")
	public String helloWorld() {
		return "Hello World";
	}

	
	@RequestMapping("/hello-world-bean")
	public HelloWorldBean helloWorldBean() {
		return new HelloWorldBean("Hello World");
	}
	
	//Path Variable or Path Params
	// /user/Ranga/todos/1
	
	@RequestMapping("/hello-world-path-param/{name}")
	public HelloWorldBean helloWorldPathParam(@PathVariable String name) {
		return new HelloWorldBean("Hello World, " + name);
	}
	
	@RequestMapping("/hello-world-path-param/{name}/message/{message}")
	public HelloWorldBean helloWorldMultiplePathParam
					(@PathVariable String name,
							@PathVariable String message) {
		return new HelloWorldBean("Hello World " + name + "," + message);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/Question.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.util.List;

public class Question {

	public Question() {

	}

	public Question(String id, String description, List<String> options, String correctAnswer) {
		super();
		this.id = id;
		this.description = description;
		this.options = options;
		this.correctAnswer = correctAnswer;
	}

	private String id;
	private String description;
	private List<String> options;
	private String correctAnswer;

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	
	public String getDescription() {
		return description;
	}

	public List<String> getOptions() {
		return options;
	}

	public String getCorrectAnswer() {
		return correctAnswer;
	}

	@Override
	public String toString() {
		return "Question [id=" + id + ", description=" + description + ", options=" + options + ", correctAnswer="
				+ correctAnswer + "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/Survey.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.util.List;

public class Survey {

	public Survey() {

	}

	public Survey(String id, String title, String description, List<Question> questions) {
		super();
		this.id = id;
		this.title = title;
		this.description = description;
		this.questions = questions;
	}

	private String id;
	private String title;
	private String description;
	private List<Question> questions;

	public String getId() {
		return id;
	}

	public String getTitle() {
		return title;
	}

	public String getDescription() {
		return description;
	}

	public List<Question> getQuestions() {
		return questions;
	}

	@Override
	public String toString() {
		return "Survey [id=" + id + ", title=" + title + ", description=" + description + ", questions=" + questions
				+ "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/SurveyResource.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.net.URI;
import java.util.List;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.server.ResponseStatusException;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

@RestController
public class SurveyResource {
	
	private SurveyService surveyService;
	
	public SurveyResource(SurveyService surveyService) {
		super();
		this.surveyService = surveyService;
	}

	// /surveys => surveys
	@RequestMapping("/surveys")
	public List<Survey> retrieveAllSurveys(){
		return surveyService.retrieveAllSurveys();
	}
	
	@RequestMapping("/surveys/{surveyId}")
	public Survey retrieveSurveyById(@PathVariable String surveyId){
		Survey survey = surveyService.retrieveSurveyById(surveyId);
		
		if(survey==null)
			throw new ResponseStatusException(HttpStatus.NOT_FOUND);
		
		return survey;
	}

	@RequestMapping("/surveys/{surveyId}/questions")
	public List<Question> retrieveAllSurveyQuestions(@PathVariable String surveyId){
		List<Question> questions = surveyService.retrieveAllSurveyQuestions(surveyId);
		
		if(questions==null)
			throw new ResponseStatusException(HttpStatus.NOT_FOUND);
		
		return questions;
	}
	
	@RequestMapping("/surveys/{surveyId}/questions/{questionId}")
	public Question retrieveSpecificSurveyQuestion(@PathVariable String surveyId,
			@PathVariable String questionId){
		Question question = surveyService.retrieveSpecificSurveyQuestion
										(surveyId, questionId);
		
		if(question==null)
			throw new ResponseStatusException(HttpStatus.NOT_FOUND);
		
		return question;
	}

	@RequestMapping(value="/surveys/{surveyId}/questions", method = RequestMethod.POST)
	public ResponseEntity<Object> addNewSurveyQuestion(@PathVariable String surveyId,
			@RequestBody Question question){
		
		String questionId = surveyService.addNewSurveyQuestion(surveyId, question);
		// /surveys/{surveyId}/questions/{questionId}
		URI location = ServletUriComponentsBuilder.fromCurrentRequest()
				.path("/{questionId}").buildAndExpand(questionId).toUri();
		return ResponseEntity.created(location ).build();
		
	}

	@RequestMapping(value="/surveys/{surveyId}/questions/{questionId}", method = RequestMethod.DELETE)
	public ResponseEntity<Object> deleteSurveyQuestion(@PathVariable String surveyId,
			@PathVariable String questionId){
		surveyService.deleteSurveyQuestion(surveyId, questionId);
		return ResponseEntity.noContent().build();
	}

	@RequestMapping(value="/surveys/{surveyId}/questions/{questionId}", method = RequestMethod.PUT)
	public ResponseEntity<Object> updateSurveyQuestion(@PathVariable String surveyId,
			@PathVariable String questionId,
			@RequestBody Question question){
		
		surveyService.updateSurveyQuestion(surveyId, questionId, question);
		
		return ResponseEntity.noContent().build();
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/SurveyService.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.math.BigInteger;
import java.security.SecureRandom;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Optional;
import java.util.function.Predicate;

import org.springframework.stereotype.Service;

@Service
public class SurveyService {

	private static List<Survey> surveys = new ArrayList<>();

	static {

		Question question1 = new Question("Question1", "Most Popular Cloud Platform Today",
				Arrays.asList("AWS", "Azure", "Google Cloud", "Oracle Cloud"), "AWS");
		Question question2 = new Question("Question2", "Fastest Growing Cloud Platform",
				Arrays.asList("AWS", "Azure", "Google Cloud", "Oracle Cloud"), "Google Cloud");
		Question question3 = new Question("Question3", "Most Popular DevOps Tool",
				Arrays.asList("Kubernetes", "Docker", "Terraform", "Azure DevOps"), "Kubernetes");

		List<Question> questions = new ArrayList<>(Arrays.asList(question1, question2, question3));

		Survey survey = new Survey("Survey1", "My Favorite Survey", "Description of the Survey", questions);

		surveys.add(survey);

	}

	public List<Survey> retrieveAllSurveys() {
		return surveys;
	}

	public Survey retrieveSurveyById(String surveyId) {

		Predicate<? super Survey> predicate = survey -> survey.getId().equalsIgnoreCase(surveyId);

		Optional<Survey> optionalSurvey = surveys.stream().filter(predicate).findFirst();

		if (optionalSurvey.isEmpty())
			return null;

		return optionalSurvey.get();
	}

	public List<Question> retrieveAllSurveyQuestions(String surveyId) {
		Survey survey = retrieveSurveyById(surveyId);

		if (survey == null)
			return null;

		return survey.getQuestions();
	}

	public Question retrieveSpecificSurveyQuestion(String surveyId, String questionId) {

		List<Question> surveyQuestions = retrieveAllSurveyQuestions(surveyId);

		if (surveyQuestions == null)
			return null;

		Optional<Question> optionalQuestion = surveyQuestions.stream()
				.filter(q -> q.getId().equalsIgnoreCase(questionId)).findFirst();

		if (optionalQuestion.isEmpty())
			return null;

		return optionalQuestion.get();
	}

	public String addNewSurveyQuestion(String surveyId, Question question) {
		List<Question> questions = retrieveAllSurveyQuestions(surveyId);
		question.setId(generateRandomId());
		questions.add(question);
		return question.getId();
	}

	private String generateRandomId() {
		SecureRandom secureRandom = new SecureRandom();
		String randomId = new BigInteger(32, secureRandom).toString();
		return randomId;
	}

	public String deleteSurveyQuestion(String surveyId, String questionId) {

		List<Question> surveyQuestions = retrieveAllSurveyQuestions(surveyId);

		if (surveyQuestions == null)
			return null;
		

		Predicate<? super Question> predicate = q -> q.getId().equalsIgnoreCase(questionId);
		boolean removed = surveyQuestions.removeIf(predicate);
		
		if(!removed) return null;

		return questionId;
	}

	public void updateSurveyQuestion(String surveyId, String questionId, Question question) {
		List<Question> questions = retrieveAllSurveyQuestions(surveyId);
		questions.removeIf(q -> q.getId().equalsIgnoreCase(questionId));
		questions.add(question);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/user/UserDetails.java

```java
package com.in28minutes.springboot.firstrestapi.user;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Id;

@Entity
public class UserDetails {
	
	@Id
	@GeneratedValue
	private Long id;
	
	private String name;
	private String role;
	
	public UserDetails() {
		
	}
	
	public UserDetails(String name, String role) {
		super();
		this.name = name;
		this.role = role;
	}

	public Long getId() {
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
		return "UserDetails [id=" + id + ", name=" + name + ", role=" + role + "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/user/UserDetailsCommandLineRunner.java

```java
package com.in28minutes.springboot.firstrestapi.user;

import java.util.List;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class UserDetailsCommandLineRunner implements CommandLineRunner {

	public UserDetailsCommandLineRunner(UserDetailsRepository repository) {
		super();
		this.repository = repository;
	}

	private Logger logger = LoggerFactory.getLogger(getClass());

	private UserDetailsRepository repository;

	@Override
	public void run(String... args) throws Exception {
		repository.save(new UserDetails("Ranga", "Admin"));
		repository.save(new UserDetails("Ravi", "Admin"));
		repository.save(new UserDetails("John", "User"));
		
		//List<UserDetails> users = repository.findAll();
		
		List<UserDetails> users = repository.findByRole("Admin");
		
		users.forEach(user -> logger.info(user.toString()));
		
		
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/user/UserDetailsRepository.java

```java
package com.in28minutes.springboot.firstrestapi.user;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;

public interface UserDetailsRepository extends JpaRepository<UserDetails, Long>{
	List<UserDetails> findByRole(String role);
}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/user/UserDetailsRestRepository.java

```java
package com.in28minutes.springboot.firstrestapi.user;

import java.util.List;

import org.springframework.data.repository.PagingAndSortingRepository;

public interface UserDetailsRestRepository extends PagingAndSortingRepository<UserDetails, Long>{
	List<UserDetails> findByRole(String role);
}
```
---

### /src/main/resources/application.properties

```properties
logging.level.org.springframework=info
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.show-sql=true
```
---

### /src/test/java/com/in28minutes/springboot/firstrestapi/FirstRestApiApplicationTests.java

```java
package com.in28minutes.springboot.firstrestapi;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class FirstRestApiApplicationTests {

	@Test
	void contextLoads() {
	}

}
```
---

### /src/test/java/com/in28minutes/springboot/firstrestapi/survey/JsonAssertTest.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import org.json.JSONException;
import org.junit.jupiter.api.Test;
import org.skyscreamer.jsonassert.JSONAssert;

public class JsonAssertTest {

	@Test
	void testJsonAssert() throws JSONException {
		JSONAssert.assertEquals("{}", "{}", false);
		JSONAssert.assertEquals("{id:5}", "{ id : 5 }", false);
		JSONAssert.assertEquals("{id:6, name:Ranga}", "{ id : 6, attr:5, name: \"Ranga\" }", false);	
	}

}
```
---

### /src/test/java/com/in28minutes/springboot/firstrestapi/survey/SurveyResponseIT.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import static org.junit.jupiter.api.Assertions.assertTrue;

import org.json.JSONException;
import org.junit.jupiter.api.Test;
import org.skyscreamer.jsonassert.JSONAssert;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.ResponseEntity;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class SurveyResponseIT {

	// 
	/*
	 
  "id": "Question1",
  "description": "Most Popular Cloud Platform Today",
  "options": [
    "AWS",
    "Azure",
    "Google Cloud",
    "Oracle Cloud"
  ],
  "correctAnswer": "AWS"
} 
	 
	 */
	
	//{"id":"Question1","description":"Most Popular Cloud Platform Today","options":["AWS","Azure","Google Cloud","Oracle Cloud"],"correctAnswer":"AWS"}

	
	@Autowired
	TestRestTemplate template;
	
	@Test
	void retrieveSpecificSurveyQuestion_basicScenario() throws JSONException {
		String url = "/surveys/Survey1/questions/Question1";
		ResponseEntity<String> response = template.getForEntity(url, String.class);
		//String expectedResponse="{\"id\":\"Question1\",\"description\":\"Most Popular Cloud Platform Today\",\"options\":[\"AWS\",\"Azure\",\"Google Cloud\",\"Oracle Cloud\"],\"correctAnswer\":\"AWS\"}";
		String expectedResponse = "{id:Question1, correctAnswer:AWS, \"description\":\"Most Popular Cloud Platform Today\"}"; 
		
		JSONAssert.assertEquals(expectedResponse, response.getBody(), false);
	}
	
	
	
	@Test
	void addNewSurveyQuestion_basicScenario() {
		
		String url = "/surveys/Survey1/questions/";
		
		String requestBody = """
					{
					  "description": "Most Popular Cloud Platform Today New",
					  "options": [
					    "AWS",
					    "Azure",
					    "Google Cloud",
					    "Oracle Cloud"
					  ],
					  "correctAnswer": "AWS"
					}
				""";
		
		HttpHeaders headers = new HttpHeaders();
		headers.add("Content-Type", "application/json");
		HttpEntity<String> httpEntity = new HttpEntity(requestBody, headers);
		
		ResponseEntity<String> responseEntity = template.exchange(url, HttpMethod.POST, httpEntity, String.class);
		System.out.println(responseEntity);

		//<201 CREATED Created,
		assertTrue(responseEntity.getStatusCode().is2xxSuccessful());
		
		String locationHeader = responseEntity.getHeaders().get("Location").get(0);
		
		//Location:"http://localhost:55163/surveys/Survey1/questions/2080216181"
		assertTrue(locationHeader.contains("/surveys/Survey1/questions"));
		
		
	}
}
```
---


# RESTful Web Services with Spring and Spring Boot


### Links from course examples
- Basic Resources
  - http://localhost:8080/hello-world
  - http://localhost:8080/hello-world-bean
  - http://localhost:8080/hello-world/path-variable/Ranga
  - http://localhost:8080/users/
  - http://localhost:8080/users/1
- JPA Resources
  - http://localhost:8080/jpa/users/
  - http://localhost:8080/jpa/users/1
  - http://localhost:8080/jpa/users/10001/posts
- Filtering
  - http://localhost:8080/filtering
  - http://localhost:8080/filtering-list
- Actuator
  - http://localhost:8080/actuator
- Versioning
  - http://localhost:8080/v1/person
  - http://localhost:8080/v2/person
  - http://localhost:8080/person/param
     - params=[version=1]
  - http://localhost:8080/person/param
     - params=[version=2]
  - http://localhost:8080/person/header
     - headers=[X-API-VERSION=1]
  - http://localhost:8080/person/header
     - headers=[X-API-VERSION=2]
  - http://localhost:8080/person/produces
     - produces=[application/vnd.company.app-v1+json]
  - http://localhost:8080/person/produces
  	 - produces=[application/vnd.company.app-v2+json]
- Swagger
  - http://localhost:8080/swagger-ui.html
  - http://localhost:8080/v2/api-docs
- H2-Console
  - http://localhost:8080/h2-console

## Table Structure

```sql
create table user (
id integer not null, 
birth_date timestamp, 
name varchar(255), 
primary key (id)
);

create table post (
id integer not null, 
description varchar(255), 
user_id integer, 
primary key (id)
);

alter table post 
add constraint post_to_user_foreign_key
foreign key (user_id) references user;
```



## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.rest.webservices</groupId>
	<artifactId>restful-web-services</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>restful-web-services</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
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

		<!--<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>-->

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.data</groupId>
			<artifactId>spring-data-rest-hal-browser</artifactId>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-hateoas</artifactId>
		</dependency>

		<dependency>
			<groupId>com.fasterxml.jackson.dataformat</groupId>
			<artifactId>jackson-dataformat-xml</artifactId>
		</dependency>
		
		<dependency>
			<groupId>io.springfox</groupId>
			<artifactId>springfox-swagger2</artifactId>
			<version>2.4.0</version>
		</dependency>

		<dependency>
			<groupId>io.springfox</groupId>
			<artifactId>springfox-swagger-ui</artifactId>
			<version>2.4.0</version>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
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


</project>
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/exception/CustomizedResponseEntityExceptionHandler.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.exception;

import java.util.Date;

import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.context.request.WebRequest;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

import com.in28minutes.rest.webservices.restfulwebservices.user.UserNotFoundException;

@ControllerAdvice
@RestController
public class CustomizedResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {

	@ExceptionHandler(Exception.class)
	public final ResponseEntity<Object> handleAllExceptions(Exception ex, WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(), ex.getMessage(),
				request.getDescription(false));
		return new ResponseEntity(exceptionResponse, HttpStatus.INTERNAL_SERVER_ERROR);
	}

	@ExceptionHandler(UserNotFoundException.class)
	public final ResponseEntity<Object> handleUserNotFoundException(UserNotFoundException ex, WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(), ex.getMessage(),
				request.getDescription(false));
		return new ResponseEntity(exceptionResponse, HttpStatus.NOT_FOUND);
	}
	
	@Override
	protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex,
			HttpHeaders headers, HttpStatus status, WebRequest request) {
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(), "Validation Failed",
				ex.getBindingResult().toString());
		return new ResponseEntity(exceptionResponse, HttpStatus.BAD_REQUEST);
	}	
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/exception/ExceptionResponse.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.exception;

import java.util.Date;

public class ExceptionResponse {
	private Date timestamp;
	private String message;
	private String details;

	public ExceptionResponse(Date timestamp, String message, String details) {
		super();
		this.timestamp = timestamp;
		this.message = message;
		this.details = details;
	}

	public Date getTimestamp() {
		return timestamp;
	}

	public String getMessage() {
		return message;
	}

	public String getDetails() {
		return details;
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/filtering/FilteringController.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.filtering;

import java.util.Arrays;
import java.util.List;

import org.springframework.http.converter.json.MappingJacksonValue;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import com.fasterxml.jackson.databind.ser.FilterProvider;
import com.fasterxml.jackson.databind.ser.impl.SimpleBeanPropertyFilter;
import com.fasterxml.jackson.databind.ser.impl.SimpleFilterProvider;

@RestController
public class FilteringController {

	// field1,field2
	@GetMapping("/filtering")
	public MappingJacksonValue retrieveSomeBean() {
		SomeBean someBean = new SomeBean("value1", "value2", "value3");

		SimpleBeanPropertyFilter filter = SimpleBeanPropertyFilter.filterOutAllExcept("field1", "field2");

		FilterProvider filters = new SimpleFilterProvider().addFilter("SomeBeanFilter", filter);

		MappingJacksonValue mapping = new MappingJacksonValue(someBean);

		mapping.setFilters(filters);

		return mapping;
	}

	// field2, field3
	@GetMapping("/filtering-list")
	public MappingJacksonValue retrieveListOfSomeBeans() {
		List<SomeBean> list = Arrays.asList(new SomeBean("value1", "value2", "value3"),
				new SomeBean("value12", "value22", "value32"));

		SimpleBeanPropertyFilter filter = SimpleBeanPropertyFilter.filterOutAllExcept("field2", "field3");

		FilterProvider filters = new SimpleFilterProvider().addFilter("SomeBeanFilter", filter);

		MappingJacksonValue mapping = new MappingJacksonValue(list);

		mapping.setFilters(filters);

		return mapping;
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/filtering/SomeBean.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.filtering;

import com.fasterxml.jackson.annotation.JsonFilter;

@JsonFilter("SomeBeanFilter")
public class SomeBean {
	
	private String field1;
	
	private String field2;
	
	private String field3;

	public SomeBean(String field1, String field2, String field3) {
		super();
		this.field1 = field1;
		this.field2 = field2;
		this.field3 = field3;
	}

    //Getter and Setters

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/helloworld/HelloWorldBean.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.helloworld;

public class HelloWorldBean {

	private String message;

	public HelloWorldBean(String message) {
		this.message = message;
	}

    //Getter and Setters

	@Override
	public String toString() {
		return String.format("HelloWorldBean [message=%s]", message);
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/helloworld/HelloWorldController.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.helloworld;

import java.util.Locale;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.MessageSource;
import org.springframework.context.i18n.LocaleContextHolder;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestHeader;
import org.springframework.web.bind.annotation.RestController;

//Controller
@RestController
public class HelloWorldController {
	
	@Autowired
	private MessageSource messageSource; 

	@GetMapping(path = "/hello-world")
	public String helloWorld() {
		return "Hello World";
	}

	@GetMapping(path = "/hello-world-bean")
	public HelloWorldBean helloWorldBean() {
		return new HelloWorldBean("Hello World");
	}
	
	///hello-world/path-variable/in28minutes
	@GetMapping(path = "/hello-world/path-variable/{name}")
	public HelloWorldBean helloWorldPathVariable(@PathVariable String name) {
		return new HelloWorldBean(String.format("Hello World, %s", name));
	}

	@GetMapping(path = "/hello-world-internationalized")
	public String helloWorldInternationalized() {
		return messageSource.getMessage("good.morning.message", null, 
									LocaleContextHolder.getLocale());
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/RestfulWebServicesApplication.java

```java
package com.in28minutes.rest.webservices.restfulwebservices;

import java.util.Locale;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.web.servlet.LocaleResolver;
import org.springframework.web.servlet.i18n.AcceptHeaderLocaleResolver;

@SpringBootApplication
public class RestfulWebServicesApplication {

	public static void main(String[] args) {
		SpringApplication.run(RestfulWebServicesApplication.class, args);
	}
	
	@Bean
	public LocaleResolver localeResolver() {
		AcceptHeaderLocaleResolver localeResolver = new AcceptHeaderLocaleResolver();
		localeResolver.setDefaultLocale(Locale.US);
		return localeResolver;
	}
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/SwaggerConfig.java

```java
package com.in28minutes.rest.webservices.restfulwebservices;

import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig {

	public static final Contact DEFAULT_CONTACT = new Contact(
			"Ranga Karanam", "http://www.in28minutes.com", "in28minutes@gmail.com");
	
	public static final ApiInfo DEFAULT_API_INFO = new ApiInfo(
			"Awesome API Title", "Awesome API Description", "1.0",
			"urn:tos", DEFAULT_CONTACT, 
			"Apache 2.0", "http://www.apache.org/licenses/LICENSE-2.0");

	private static final Set<String> DEFAULT_PRODUCES_AND_CONSUMES = 
			new HashSet<String>(Arrays.asList("application/json",
					"application/xml"));

	@Bean
	public Docket api() {
		return new Docket(DocumentationType.SWAGGER_2)
				.apiInfo(DEFAULT_API_INFO)
				.produces(DEFAULT_PRODUCES_AND_CONSUMES)
				.consumes(DEFAULT_PRODUCES_AND_CONSUMES);
	}
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/Post.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import javax.persistence.Entity;
import javax.persistence.FetchType;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.ManyToOne;

import com.fasterxml.jackson.annotation.JsonIgnore;

@Entity
public class Post {
	
	@Id
	@GeneratedValue
	private Integer id;
	private String description;
	
	@ManyToOne(fetch=FetchType.LAZY)
	@JsonIgnore
	private User user;
	
    //Getter and Setters

	@Override
	public String toString() {
		return String.format("Post [id=%s, description=%s]", id, description);
	}
	
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/PostRepository.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface PostRepository extends JpaRepository<Post, Integer>{

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/User.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import java.util.Date;
import java.util.List;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.OneToMany;
import javax.validation.constraints.Past;
import javax.validation.constraints.Size;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;

@ApiModel(description="All details about the user.")
@Entity
public class User {

	@Id
	@GeneratedValue
	private Integer id;

	@Size(min=2, message="Name should have atleast 2 characters")
	@ApiModelProperty(notes="Name should have atleast 2 characters")
	private String name;

	@Past
	@ApiModelProperty(notes="Birth date should be in the past")
	private Date birthDate;
	
	@OneToMany(mappedBy="user")
	private List<Post> posts;

	protected User() {

	}

	public User(Integer id, String name, Date birthDate) {
		super();
		this.id = id;
		this.name = name;
		this.birthDate = birthDate;
	}

    //Getter and Setters

	@Override
	public String toString() {
		return String.format("User [id=%s, name=%s, birthDate=%s]", id, name, birthDate);
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/UserDaoService.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import java.util.ArrayList;
import java.util.Date;
import java.util.Iterator;
import java.util.List;

import org.springframework.stereotype.Component;

@Component
public class UserDaoService {
	
	private static List<User> users = new ArrayList<>();

	private static int usersCount = 3;

	static {
		users.add(new User(1, "Adam", new Date()));
		users.add(new User(2, "Eve", new Date()));
		users.add(new User(3, "Jack", new Date()));
	}

	public List<User> findAll() {
		return users;
	}

	public User save(User user) {
		if (user.getId() == null) {
			user.setId(++usersCount);
		}
		users.add(user);
		return user;
	}

	public User findOne(int id) {
		for (User user : users) {
			if (user.getId() == id) {
				return user;
			}
		}
		return null;
	}

	public User deleteById(int id) {
		Iterator<User> iterator = users.iterator();
		while (iterator.hasNext()) {
			User user = iterator.next();
			if (user.getId() == id) {
				iterator.remove();
				return user;
			}
		}
		return null;
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/UserJPAResource.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import static org.springframework.hateoas.mvc.ControllerLinkBuilder.linkTo;
import static org.springframework.hateoas.mvc.ControllerLinkBuilder.methodOn;

import java.net.URI;
import java.util.List;
import java.util.Optional;

import javax.validation.Valid;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.hateoas.Resource;
import org.springframework.hateoas.mvc.ControllerLinkBuilder;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

@RestController
public class UserJPAResource {

	@Autowired
	private UserRepository userRepository;
	
	@Autowired
	private PostRepository postRepository;

	@GetMapping("/jpa/users")
	public List<User> retrieveAllUsers() {
		return userRepository.findAll();
	}

	@GetMapping("/jpa/users/{id}")
	public Resource<User> retrieveUser(@PathVariable int id) {
		Optional<User> user = userRepository.findById(id);

		if (!user.isPresent())
			throw new UserNotFoundException("id-" + id);

		// "all-users", SERVER_PATH + "/users"
		// retrieveAllUsers
		Resource<User> resource = new Resource<User>(user.get());

		ControllerLinkBuilder linkTo = linkTo(methodOn(this.getClass()).retrieveAllUsers());

		resource.add(linkTo.withRel("all-users"));

		// HATEOAS

		return resource;
	}

	@DeleteMapping("/jpa/users/{id}")
	public void deleteUser(@PathVariable int id) {
		userRepository.deleteById(id);
	}

	//
	// input - details of user
	// output - CREATED & Return the created URI

	// HATEOAS

	@PostMapping("/jpa/users")
	public ResponseEntity<Object> createUser(@Valid @RequestBody User user) {
		User savedUser = userRepository.save(user);

		URI location = ServletUriComponentsBuilder.fromCurrentRequest().path("/{id}").buildAndExpand(savedUser.getId())
				.toUri();

		return ResponseEntity.created(location).build();

	}
	
	@GetMapping("/jpa/users/{id}/posts")
	public List<Post> retrieveAllUsers(@PathVariable int id) {
		Optional<User> userOptional = userRepository.findById(id);
		
		if(!userOptional.isPresent()) {
			throw new UserNotFoundException("id-" + id);
		}
		
		return userOptional.get().getPosts();
	}


	@PostMapping("/jpa/users/{id}/posts")
	public ResponseEntity<Object> createPost(@PathVariable int id, @RequestBody Post post) {
		
		Optional<User> userOptional = userRepository.findById(id);
		
		if(!userOptional.isPresent()) {
			throw new UserNotFoundException("id-" + id);
		}

		User user = userOptional.get();
		
		post.setUser(user);
		
		postRepository.save(post);
		
		URI location = ServletUriComponentsBuilder.fromCurrentRequest().path("/{id}").buildAndExpand(post.getId())
				.toUri();

		return ResponseEntity.created(location).build();

	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/UserNotFoundException.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ResponseStatus;

@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException extends RuntimeException {
	public UserNotFoundException(String message) {
		super(message);
	}
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/UserRepository.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends JpaRepository<User, Integer>{

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/user/UserResource.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.user;

import static org.springframework.hateoas.mvc.ControllerLinkBuilder.linkTo;
import static org.springframework.hateoas.mvc.ControllerLinkBuilder.methodOn;

import java.net.URI;
import java.util.List;

import javax.validation.Valid;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.hateoas.Resource;
import org.springframework.hateoas.mvc.ControllerLinkBuilder;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

@RestController
public class UserResource {

	@Autowired
	private UserDaoService service;

	@GetMapping("/users")
	public List<User> retrieveAllUsers() {
		return service.findAll();
	}

	@GetMapping("/users/{id}")
	public Resource<User> retrieveUser(@PathVariable int id) {
		User user = service.findOne(id);
		
		if(user==null)
			throw new UserNotFoundException("id-"+ id);
		
		
		//"all-users", SERVER_PATH + "/users"
		//retrieveAllUsers
		Resource<User> resource = new Resource<User>(user);
		
		ControllerLinkBuilder linkTo = 
				linkTo(methodOn(this.getClass()).retrieveAllUsers());
		
		resource.add(linkTo.withRel("all-users"));
		
		//HATEOAS
		
		return resource;
	}

	@DeleteMapping("/users/{id}")
	public void deleteUser(@PathVariable int id) {
		User user = service.deleteById(id);
		
		if(user==null)
			throw new UserNotFoundException("id-"+ id);		
	}

	//
	// input - details of user
	// output - CREATED & Return the created URI
	
	//HATEOAS
	
	@PostMapping("/users")
	public ResponseEntity<Object> createUser(@Valid @RequestBody User user) {
		User savedUser = service.save(user);
		// CREATED
		// /user/{id}     savedUser.getId()
		
		URI location = ServletUriComponentsBuilder
			.fromCurrentRequest()
			.path("/{id}")
			.buildAndExpand(savedUser.getId()).toUri();
		
		return ResponseEntity.created(location).build();
		
	}
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/versioning/Name.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.versioning;

public class Name {
	private String firstName;
	private String lastName;

	public Name() {
	}

	public Name(String firstName, String lastName) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
	}

    //Getter and Setters

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/versioning/PersonV1.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.versioning;

public class PersonV1 {
	private String name;

	public PersonV1() {
		super();
	}
	
	public PersonV1(String name) {
		super();
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	
}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/versioning/PersonV2.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.versioning;

public class PersonV2 {
	private Name name;

	public PersonV2() {
		super();
	}

	public PersonV2(Name name) {
		super();
		this.name = name;
	}

	public Name getName() {
		return name;
	}

	public void setName(Name name) {
		this.name = name;
	}

}
```
---

### /src/main/java/com/in28minutes/rest/webservices/restfulwebservices/versioning/PersonVersioningController.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.versioning;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class PersonVersioningController {

	@GetMapping("v1/person")
	public PersonV1 personV1() {
		return new PersonV1("Bob Charlie");
	}

	@GetMapping("v2/person")
	public PersonV2 personV2() {
		return new PersonV2(new Name("Bob", "Charlie"));
	}

	@GetMapping(value = "/person/param", params = "version=1")
	public PersonV1 paramV1() {
		return new PersonV1("Bob Charlie");
	}

	@GetMapping(value = "/person/param", params = "version=2")
	public PersonV2 paramV2() {
		return new PersonV2(new Name("Bob", "Charlie"));
	}

	@GetMapping(value = "/person/header", headers = "X-API-VERSION=1")
	public PersonV1 headerV1() {
		return new PersonV1("Bob Charlie");
	}

	@GetMapping(value = "/person/header", headers = "X-API-VERSION=2")
	public PersonV2 headerV2() {
		return new PersonV2(new Name("Bob", "Charlie"));
	}

	@GetMapping(value = "/person/produces", produces = "application/vnd.company.app-v1+json")
	public PersonV1 producesV1() {
		return new PersonV1("Bob Charlie");
	}

	@GetMapping(value = "/person/produces", produces = "application/vnd.company.app-v2+json")
	public PersonV2 producesV2() {
		return new PersonV2(new Name("Bob", "Charlie"));
	}

}
```
---

### /src/main/resources/application.properties

```properties
logging.level.org.springframework = info
#This is not really needed as this is the default after 2.0.0.RELEASE
spring.jackson.serialization.write-dates-as-timestamps=false
management.endpoints.web.exposure.include=*
spring.security.user.name=username
spring.security.user.password=password
spring.jpa.show-sql=true
spring.h2.console.enabled=true
```
---

### /src/main/resources/data.sql

```
insert into user values(10001, sysdate(), 'AB');
insert into user values(10002, sysdate(), 'Jill');
insert into user values(10003, sysdate(), 'Jam');
insert into post values(11001, 'My First Post', 10001);
insert into post values(11002, 'My Second Post', 10001);
```
---

### /src/main/resources/messages.properties

```properties
good.morning.message=Good Morning
```
---

### /src/main/resources/messages_fr.properties

```properties
good.morning.message=Bonjour
```
---

### /src/main/resources/messages_nl.properties

```properties
good.morning.message=Goede Morgen
```
---

### /src/test/java/com/in28minutes/rest/webservices/restfulwebservices/RestfulWebServicesApplicationTests.java

```java
package com.in28minutes.rest.webservices.restfulwebservices;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class RestfulWebServicesApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

# SOAP Web Services with Spring and Spring Boot


## Useful Links
 - XML Schema - http://edutechwiki.unige.ch/en/XML_Schema_tutorial_-_Basics
 - WSDL URl - http://localhost:8080/ws/courses.wsdl
 - Spring Web Services - http://projects.spring.io/spring-ws/

## Security Dependencies

```xml
	<dependency>
            <groupId>org.springframework.ws</groupId>
            <artifactId>spring-ws-security</artifactId>
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.security</groupId>
                    <artifactId>spring-security-core</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>com.sun.xml.wss</groupId>
            <artifactId>xws-security</artifactId>
            <version>3.0</version>
            <exclusions>
                <exclusion>
                    <groupId>javax.xml.crypto</groupId>
                    <artifactId>xmldsig</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>javax.activation</groupId>
            <artifactId>activation</artifactId>
            <version>1.1.1</version>
        </dependency>
```    

## Security Request
```xml
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">
	<Header>
		<wsse:Security
			xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"
			mustUnderstand="1">
			<wsse:UsernameToken>
				<wsse:Username>user</wsse:Username>
				<wsse:Password>password</wsse:Password>
			</wsse:UsernameToken>
		</wsse:Security>
	</Header>
	<Body>
		<GetCourseDetailsRequest xmlns="http://in28minutes.com/courses">
			<id>1</id>
		</GetCourseDetailsRequest>
	</Body>
</Envelope>
```

## securityPolicy.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<xwss:SecurityConfiguration 
xmlns:xwss="http://java.sun.com/xml/ns/xwss/config">
	<xwss:RequireUsernameToken
		passwordDigestRequired="false" nonceRequired="false" />
</xwss:SecurityConfiguration>
```

## Error
java.lang.NoClassDefFoundError: javax/wsdl/extensions/ExtensibilityElement

## Security with WS-Security
 - Authentication
 - Digital signatures
 - Certificates
 
 - Implementation -> XWSS - XML and Web Services Security.
   - Security Policy
   - XwsSecurityInterceptor


## Complete Code Example

### /example-files/Request-Security.xml

```xml
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">
	<Header>
		<wsse:Security
			xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"
			mustUnderstand="1">
			<wsse:UsernameToken>
				<wsse:Username>user</wsse:Username>
				<wsse:Password>password</wsse:Password>
			</wsse:UsernameToken>
		</wsse:Security>
	</Header>
	<Body>
		<GetCourseDetailsRequest xmlns="http://in28minutes.com/courses">
			<id>1</id>
		</GetCourseDetailsRequest>
	</Body>
</Envelope>
```
---

### /example-files/Request.xml

```xml
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">
	<Body>
		<GetCourseDetailsRequest xmlns="http://in28minutes.com/courses">
			<id>1</id>
		</GetCourseDetailsRequest>
	</Body>
</Envelope>
```
---

### /example-files/Response-Fault.xml

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
	<SOAP-ENV:Header />
	<SOAP-ENV:Body>
		<SOAP-ENV:Fault>
			<faultcode xmlns:ns0="http://in28minutes.com/courses">ns0:001_COURSE_NOT_FOUND</faultcode>
			<faultstring xml:lang="en">Invalid Course Id 1234</faultstring>
		</SOAP-ENV:Fault>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
---

### /example-files/Response.xml

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Header/>
    <SOAP-ENV:Body>
        <ns2:GetCourseDetailsResponse xmlns:ns2="http://in28minutes.com/courses">
            <ns2:CourseDetails>
                <ns2:id>1</ns2:id>
                <ns2:name>Spring</ns2:name>
                <ns2:description>10 Steps</ns2:description>
            </ns2:CourseDetails>
        </ns2:GetCourseDetailsResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
---

### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.soap.webservices</groupId>
	<artifactId>soap-course-management</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>soap-course-management</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
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
			<artifactId>spring-boot-starter-web-services</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
		</dependency>
		<dependency>
			<groupId>wsdl4j</groupId>
			<artifactId>wsdl4j</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.ws</groupId>
			<artifactId>spring-ws-security</artifactId>
			<exclusions>
				<exclusion>
					<groupId>org.springframework.security</groupId>
					<artifactId>spring-security-core</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>com.sun.xml.wss</groupId>
			<artifactId>xws-security</artifactId>
			<version>3.0</version>
			<exclusions>
				<exclusion>
					<groupId>javax.xml.crypto</groupId>
					<artifactId>xmldsig</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>javax.activation</groupId>
			<artifactId>activation</artifactId>
			<version>1.1.1</version>
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
			<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>jaxb2-maven-plugin</artifactId>
				<version>1.6</version>
				<executions>
					<execution>
						<id>xjc</id>
						<goals>
							<goal>xjc</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<schemaDirectory>${project.basedir}/src/main/resources</schemaDirectory>
					<outputDirectory>${project.basedir}/src/main/java</outputDirectory>
					<clearOutputDir>false</clearOutputDir>
				</configuration>
			</plugin>
			<!-- JAXB2 Maven Plugin -->
			<!-- XSD Source Folder -->
			<!-- Java Class Source Folder -->
			<!-- clear folder -> false -->

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

### /src/main/java/com/in28minutes/courses/CourseDetails.java

Removed Generated Code

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/bean/Course.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap.bean;

public class Course {
	private int id;
	private String name;
	private String description;
	
	
	public Course(int id, String name, String description) {
		super();
		this.id = id;
		this.name = name;
		this.description = description;
	}

    //Getter and Setters

	@Override
	public String toString() {
		return String.format("Course [id=%s, name=%s, description=%s]", id, name, description);
	}

}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/CourseDetailsEndpoint.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ws.server.endpoint.annotation.Endpoint;
import org.springframework.ws.server.endpoint.annotation.PayloadRoot;
import org.springframework.ws.server.endpoint.annotation.RequestPayload;
import org.springframework.ws.server.endpoint.annotation.ResponsePayload;

import com.in28minutes.courses.CourseDetails;
import com.in28minutes.courses.DeleteCourseDetailsRequest;
import com.in28minutes.courses.DeleteCourseDetailsResponse;
import com.in28minutes.courses.GetAllCourseDetailsRequest;
import com.in28minutes.courses.GetAllCourseDetailsResponse;
import com.in28minutes.courses.GetCourseDetailsRequest;
import com.in28minutes.courses.GetCourseDetailsResponse;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.bean.Course;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.exception.CourseNotFoundException;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.service.CourseDetailsService;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.service.CourseDetailsService.Status;

@Endpoint
public class CourseDetailsEndpoint {

	@Autowired
	CourseDetailsService service;

	// method
	// input - GetCourseDetailsRequest
	// output - GetCourseDetailsResponse

	// http://in28minutes.com/courses
	// GetCourseDetailsRequest
	@PayloadRoot(namespace = "http://in28minutes.com/courses", localPart = "GetCourseDetailsRequest")
	@ResponsePayload
	public GetCourseDetailsResponse processCourseDetailsRequest(@RequestPayload GetCourseDetailsRequest request) {

		Course course = service.findById(request.getId());

		if (course == null)
			throw new CourseNotFoundException("Invalid Course Id " + request.getId());

		return mapCourseDetails(course);
	}

	private GetCourseDetailsResponse mapCourseDetails(Course course) {
		GetCourseDetailsResponse response = new GetCourseDetailsResponse();
		response.setCourseDetails(mapCourse(course));
		return response;
	}

	private GetAllCourseDetailsResponse mapAllCourseDetails(List<Course> courses) {
		GetAllCourseDetailsResponse response = new GetAllCourseDetailsResponse();
		for (Course course : courses) {
			CourseDetails mapCourse = mapCourse(course);
			response.getCourseDetails().add(mapCourse);
		}
		return response;
	}

	private CourseDetails mapCourse(Course course) {
		CourseDetails courseDetails = new CourseDetails();

		courseDetails.setId(course.getId());

		courseDetails.setName(course.getName());

		courseDetails.setDescription(course.getDescription());
		return courseDetails;
	}

	@PayloadRoot(namespace = "http://in28minutes.com/courses", localPart = "GetAllCourseDetailsRequest")
	@ResponsePayload
	public GetAllCourseDetailsResponse processAllCourseDetailsRequest(
			@RequestPayload GetAllCourseDetailsRequest request) {

		List<Course> courses = service.findAll();

		return mapAllCourseDetails(courses);
	}

	@PayloadRoot(namespace = "http://in28minutes.com/courses", localPart = "DeleteCourseDetailsRequest")
	@ResponsePayload
	public DeleteCourseDetailsResponse deleteCourseDetailsRequest(@RequestPayload DeleteCourseDetailsRequest request) {

		Status status = service.deleteById(request.getId());

		DeleteCourseDetailsResponse response = new DeleteCourseDetailsResponse();
		response.setStatus(mapStatus(status));

		return response;
	}

	private com.in28minutes.courses.Status mapStatus(Status status) {
		if (status == Status.FAILURE)
			return com.in28minutes.courses.Status.FAILURE;
		return com.in28minutes.courses.Status.SUCCESS;
	}
}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/exception/CourseNotFoundException.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap.exception;

import org.springframework.ws.soap.server.endpoint.annotation.FaultCode;
import org.springframework.ws.soap.server.endpoint.annotation.SoapFault;

@SoapFault(faultCode = FaultCode.CUSTOM, customFaultCode = "{http://in28minutes.com/courses}001_COURSE_NOT_FOUND")
public class CourseNotFoundException extends RuntimeException {

	private static final long serialVersionUID = 3518170101751491969L;

	public CourseNotFoundException(String message) {
		super(message);
	}
}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/service/CourseDetailsService.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap.service;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

import org.springframework.stereotype.Component;

import com.in28minutes.soap.webservices.soapcoursemanagement.soap.bean.Course;

@Component
public class CourseDetailsService {
	
	public enum Status {
		SUCCESS, FAILURE;
	}

	private static List<Course> courses = new ArrayList<>();

	static {
		Course course1 = new Course(1, "Spring", "10 Steps");
		courses.add(course1);

		Course course2 = new Course(2, "Spring MVC", "10 Examples");
		courses.add(course2);

		Course course3 = new Course(3, "Spring Boot", "6K Students");
		courses.add(course3);

		Course course4 = new Course(4, "Maven", "Most popular maven course on internet!");
		courses.add(course4);
	}

	// course - 1
	public Course findById(int id) {
		for (Course course : courses) {
			if (course.getId() == id)
				return course;
		}
		return null;
	}

	// courses
	public List<Course> findAll() {
		return courses;
	}

	public Status deleteById(int id) {
		Iterator<Course> iterator = courses.iterator();
		while (iterator.hasNext()) {
			Course course = iterator.next();
			if (course.getId() == id) {
				iterator.remove();
				return Status.SUCCESS;
			}
		}
		return Status.FAILURE;
	}

	// updating course & new course
}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/WebServiceConfig.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap;

import java.util.Collections;
import java.util.List;

import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.ClassPathResource;
import org.springframework.ws.config.annotation.EnableWs;
import org.springframework.ws.config.annotation.WsConfigurerAdapter;
import org.springframework.ws.server.EndpointInterceptor;
import org.springframework.ws.soap.security.xwss.XwsSecurityInterceptor;
import org.springframework.ws.soap.security.xwss.callback.SimplePasswordValidationCallbackHandler;
import org.springframework.ws.transport.http.MessageDispatcherServlet;
import org.springframework.ws.wsdl.wsdl11.DefaultWsdl11Definition;
import org.springframework.xml.xsd.SimpleXsdSchema;
import org.springframework.xml.xsd.XsdSchema;

//Enable Spring Web Services
@EnableWs
// Spring Configuration
@Configuration
public class WebServiceConfig extends WsConfigurerAdapter{
	// MessageDispatcherServlet
	// ApplicationContext
	// url -> /ws/*

	@Bean
	public ServletRegistrationBean messageDispatcherServlet(ApplicationContext context) {
		MessageDispatcherServlet messageDispatcherServlet = new MessageDispatcherServlet();
		messageDispatcherServlet.setApplicationContext(context);
		messageDispatcherServlet.setTransformWsdlLocations(true);
		return new ServletRegistrationBean(messageDispatcherServlet, "/ws/*");
	}

	// /ws/courses.wsdl
	// course-details.xsd
	@Bean(name = "courses")
	public DefaultWsdl11Definition defaultWsdl11Definition(XsdSchema coursesSchema) {
		DefaultWsdl11Definition definition = new DefaultWsdl11Definition();
		definition.setPortTypeName("CoursePort");
		definition.setTargetNamespace("http://in28minutes.com/courses");
		definition.setLocationUri("/ws");
		definition.setSchema(coursesSchema);
		return definition;
	}

	@Bean
	public XsdSchema coursesSchema() {
		return new SimpleXsdSchema(new ClassPathResource("course-details.xsd"));
	}
	

	//XwsSecurityInterceptor
	@Bean
	public XwsSecurityInterceptor securityInterceptor(){
		XwsSecurityInterceptor securityInterceptor = new XwsSecurityInterceptor();
		//Callback Handler -> SimplePasswordValidationCallbackHandler
		securityInterceptor.setCallbackHandler(callbackHandler());
		//Security Policy -> securityPolicy.xml
		securityInterceptor.setPolicyConfiguration(new ClassPathResource("securityPolicy.xml"));
		return securityInterceptor;
	}
	
	@Bean
	public SimplePasswordValidationCallbackHandler callbackHandler() {
		SimplePasswordValidationCallbackHandler handler = new SimplePasswordValidationCallbackHandler();
		handler.setUsersMap(Collections.singletonMap("user", "password"));
		return handler;
	}

	//Interceptors.add -> XwsSecurityInterceptor
	@Override
	public void addInterceptors(List<EndpointInterceptor> interceptors) {
		interceptors.add(securityInterceptor());
	}

}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/SoapCourseManagementApplication.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SoapCourseManagementApplication {

	public static void main(String[] args) {
		SpringApplication.run(SoapCourseManagementApplication.class, args);
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/main/resources/course-details.xsd

```
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
	targetNamespace="http://in28minutes.com/courses" xmlns:tns="http://in28minutes.com/courses"
	elementFormDefault="qualified">

	<xs:element name="GetCourseDetailsRequest">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="id" type="xs:int" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="GetCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="CourseDetails" type="tns:CourseDetails" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="GetAllCourseDetailsRequest">
		<xs:complexType>
		</xs:complexType>
	</xs:element>

	<xs:element name="GetAllCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="CourseDetails" type="tns:CourseDetails"
					maxOccurs="unbounded" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="DeleteCourseDetailsRequest">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="id" type="xs:int" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="DeleteCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="status" type="tns:Status" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:simpleType name="Status">
		<xs:restriction base="xs:string">
			<xs:enumeration value="SUCCESS" />
			<xs:enumeration value="FAILURE" />
		</xs:restriction>
	</xs:simpleType>

	<xs:complexType name="CourseDetails">
		<xs:sequence>
			<xs:element name="id" type="xs:int" />
			<xs:element name="name" type="xs:string" />
			<xs:element name="description" type="xs:string" />
		</xs:sequence>
	</xs:complexType>

</xs:schema>
```
---

### /src/main/resources/securityPolicy.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xwss:SecurityConfiguration 
	xmlns:xwss="http://java.sun.com/xml/ns/xwss/config">
	<xwss:RequireUsernameToken
		passwordDigestRequired="false" nonceRequired="false" />
</xwss:SecurityConfiguration>
```
---

### /src/test/java/com/in28minutes/soap/webservices/soapcoursemanagement/SoapCourseManagementApplicationTests.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SoapCourseManagementApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

## Complete Code Example


### /example-files/course-details.xsd

```
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" 
targetNamespace="http://in28minutes.com/courses" 
xmlns:tns="http://in28minutes.com/courses" elementFormDefault="qualified">
	
	<xs:element name="GetCourseDetailsRequest">
		<xs:complexType>
			<xs:sequence>
				<xs:element name= "id" type="xs:integer"/>
			</xs:sequence>	
		</xs:complexType>
	</xs:element>
	
	<xs:element name="GetCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name= "CourseDetails" type="tns:CourseDetails"/>
			</xs:sequence>	
		</xs:complexType>
	</xs:element>
	
	<xs:complexType name="CourseDetails">
		<xs:sequence>
			<xs:element name="id" type="xs:integer"/>
			<xs:element name="name" type="xs:string"/>
			<xs:element name="description" type="xs:string"/>
		</xs:sequence>
	</xs:complexType>
	
</xs:schema>
```
---

### /example-files/Request-Security.xml

```xml
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">
	<Header>
		<wsse:Security
			xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"
			mustUnderstand="1">
			<wsse:UsernameToken>
				<wsse:Username>user</wsse:Username>
				<wsse:Password>password</wsse:Password>
			</wsse:UsernameToken>
		</wsse:Security>
	</Header>
	<Body>
		<GetCourseDetailsRequest xmlns="http://in28minutes.com/courses">
			<id>1</id>
		</GetCourseDetailsRequest>
	</Body>
</Envelope>
```
---

### /example-files/Request.xml

```xml
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">
	<Body>
		<GetCourseDetailsRequest xmlns="http://in28minutes.com/courses">
			<id>1</id>
		</GetCourseDetailsRequest>
	</Body>
</Envelope>
```
---

### /example-files/Response-Fault.xml

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
	<SOAP-ENV:Header />
	<SOAP-ENV:Body>
		<SOAP-ENV:Fault>
			<faultcode xmlns:ns0="http://in28minutes.com/courses">ns0:001_COURSE_NOT_FOUND</faultcode>
			<faultstring xml:lang="en">Invalid Course Id 1234</faultstring>
		</SOAP-ENV:Fault>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
---

### /example-files/Response.xml

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Header/>
    <SOAP-ENV:Body>
        <ns2:GetCourseDetailsResponse xmlns:ns2="http://in28minutes.com/courses">
            <ns2:CourseDetails>
                <ns2:id>1</ns2:id>
                <ns2:name>Spring</ns2:name>
                <ns2:description>10 Steps</ns2:description>
            </ns2:CourseDetails>
        </ns2:GetCourseDetailsResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
---

### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.soap.webservices</groupId>
	<artifactId>soap-course-management</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>soap-course-management</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
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
			<artifactId>spring-boot-starter-web-services</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
		</dependency>
		<dependency>
			<groupId>wsdl4j</groupId>
			<artifactId>wsdl4j</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.ws</groupId>
			<artifactId>spring-ws-security</artifactId>
			<exclusions>
				<exclusion>
					<groupId>org.springframework.security</groupId>
					<artifactId>spring-security-core</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>com.sun.xml.wss</groupId>
			<artifactId>xws-security</artifactId>
			<version>3.0</version>
			<exclusions>
				<exclusion>
					<groupId>javax.xml.crypto</groupId>
					<artifactId>xmldsig</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>javax.activation</groupId>
			<artifactId>activation</artifactId>
			<version>1.1.1</version>
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
			<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>jaxb2-maven-plugin</artifactId>
				<version>1.6</version>
				<executions>
					<execution>
						<id>xjc</id>
						<goals>
							<goal>xjc</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<schemaDirectory>${project.basedir}/src/main/resources</schemaDirectory>
					<outputDirectory>${project.basedir}/src/main/java</outputDirectory>
					<clearOutputDir>false</clearOutputDir>
				</configuration>
			</plugin>
			<!-- JAXB2 Maven Plugin -->
			<!-- XSD Source Folder -->
			<!-- Java Class Source Folder -->
			<!-- clear folder -> false -->

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

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/bean/Course.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap.bean;

public class Course {
	private int id;
	private String name;
	private String description;
	
	
	public Course(int id, String name, String description) {
		super();
		this.id = id;
		this.name = name;
		this.description = description;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getDescription() {
		return description;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	@Override
	public String toString() {
		return String.format("Course [id=%s, name=%s, description=%s]", id, name, description);
	}

}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/CourseDetailsEndpoint.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ws.server.endpoint.annotation.Endpoint;
import org.springframework.ws.server.endpoint.annotation.PayloadRoot;
import org.springframework.ws.server.endpoint.annotation.RequestPayload;
import org.springframework.ws.server.endpoint.annotation.ResponsePayload;

import com.in28minutes.courses.CourseDetails;
import com.in28minutes.courses.DeleteCourseDetailsRequest;
import com.in28minutes.courses.DeleteCourseDetailsResponse;
import com.in28minutes.courses.GetAllCourseDetailsRequest;
import com.in28minutes.courses.GetAllCourseDetailsResponse;
import com.in28minutes.courses.GetCourseDetailsRequest;
import com.in28minutes.courses.GetCourseDetailsResponse;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.bean.Course;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.exception.CourseNotFoundException;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.service.CourseDetailsService;
import com.in28minutes.soap.webservices.soapcoursemanagement.soap.service.CourseDetailsService.Status;

@Endpoint
public class CourseDetailsEndpoint {

	@Autowired
	CourseDetailsService service;

	// method
	// input - GetCourseDetailsRequest
	// output - GetCourseDetailsResponse

	// http://in28minutes.com/courses
	// GetCourseDetailsRequest
	@PayloadRoot(namespace = "http://in28minutes.com/courses", localPart = "GetCourseDetailsRequest")
	@ResponsePayload
	public GetCourseDetailsResponse processCourseDetailsRequest(@RequestPayload GetCourseDetailsRequest request) {

		Course course = service.findById(request.getId());

		if (course == null)
			throw new CourseNotFoundException("Invalid Course Id " + request.getId());

		return mapCourseDetails(course);
	}

	private GetCourseDetailsResponse mapCourseDetails(Course course) {
		GetCourseDetailsResponse response = new GetCourseDetailsResponse();
		response.setCourseDetails(mapCourse(course));
		return response;
	}

	private GetAllCourseDetailsResponse mapAllCourseDetails(List<Course> courses) {
		GetAllCourseDetailsResponse response = new GetAllCourseDetailsResponse();
		for (Course course : courses) {
			CourseDetails mapCourse = mapCourse(course);
			response.getCourseDetails().add(mapCourse);
		}
		return response;
	}

	private CourseDetails mapCourse(Course course) {
		CourseDetails courseDetails = new CourseDetails();

		courseDetails.setId(course.getId());

		courseDetails.setName(course.getName());

		courseDetails.setDescription(course.getDescription());
		return courseDetails;
	}

	@PayloadRoot(namespace = "http://in28minutes.com/courses", localPart = "GetAllCourseDetailsRequest")
	@ResponsePayload
	public GetAllCourseDetailsResponse processAllCourseDetailsRequest(
			@RequestPayload GetAllCourseDetailsRequest request) {

		List<Course> courses = service.findAll();

		return mapAllCourseDetails(courses);
	}

	@PayloadRoot(namespace = "http://in28minutes.com/courses", localPart = "DeleteCourseDetailsRequest")
	@ResponsePayload
	public DeleteCourseDetailsResponse deleteCourseDetailsRequest(@RequestPayload DeleteCourseDetailsRequest request) {

		Status status = service.deleteById(request.getId());

		DeleteCourseDetailsResponse response = new DeleteCourseDetailsResponse();
		response.setStatus(mapStatus(status));

		return response;
	}

	private com.in28minutes.courses.Status mapStatus(Status status) {
		if (status == Status.FAILURE)
			return com.in28minutes.courses.Status.FAILURE;
		return com.in28minutes.courses.Status.SUCCESS;
	}
}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/exception/CourseNotFoundException.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap.exception;

import org.springframework.ws.soap.server.endpoint.annotation.FaultCode;
import org.springframework.ws.soap.server.endpoint.annotation.SoapFault;

@SoapFault(faultCode = FaultCode.CUSTOM, customFaultCode = "{http://in28minutes.com/courses}001_COURSE_NOT_FOUND")
public class CourseNotFoundException extends RuntimeException {

	private static final long serialVersionUID = 3518170101751491969L;

	public CourseNotFoundException(String message) {
		super(message);
	}
}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/service/CourseDetailsService.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap.service;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

import org.springframework.stereotype.Component;

import com.in28minutes.soap.webservices.soapcoursemanagement.soap.bean.Course;

@Component
public class CourseDetailsService {
	
	public enum Status {
		SUCCESS, FAILURE;
	}

	private static List<Course> courses = new ArrayList<>();

	static {
		Course course1 = new Course(1, "Spring", "10 Steps");
		courses.add(course1);

		Course course2 = new Course(2, "Spring MVC", "10 Examples");
		courses.add(course2);

		Course course3 = new Course(3, "Spring Boot", "6K Students");
		courses.add(course3);

		Course course4 = new Course(4, "Maven", "Most popular maven course on internet!");
		courses.add(course4);
	}

	// course - 1
	public Course findById(int id) {
		for (Course course : courses) {
			if (course.getId() == id)
				return course;
		}
		return null;
	}

	// courses
	public List<Course> findAll() {
		return courses;
	}

	public Status deleteById(int id) {
		Iterator<Course> iterator = courses.iterator();
		while (iterator.hasNext()) {
			Course course = iterator.next();
			if (course.getId() == id) {
				iterator.remove();
				return Status.SUCCESS;
			}
		}
		return Status.FAILURE;
	}

	// updating course & new course
}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/soap/WebServiceConfig.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement.soap;

import java.util.Collections;
import java.util.List;

import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.ClassPathResource;
import org.springframework.ws.config.annotation.EnableWs;
import org.springframework.ws.config.annotation.WsConfigurerAdapter;
import org.springframework.ws.server.EndpointInterceptor;
import org.springframework.ws.soap.security.xwss.XwsSecurityInterceptor;
import org.springframework.ws.soap.security.xwss.callback.SimplePasswordValidationCallbackHandler;
import org.springframework.ws.transport.http.MessageDispatcherServlet;
import org.springframework.ws.wsdl.wsdl11.DefaultWsdl11Definition;
import org.springframework.xml.xsd.SimpleXsdSchema;
import org.springframework.xml.xsd.XsdSchema;

//Enable Spring Web Services
@EnableWs
// Spring Configuration
@Configuration
public class WebServiceConfig extends WsConfigurerAdapter{
	// MessageDispatcherServlet
	// ApplicationContext
	// url -> /ws/*

	@Bean
	public ServletRegistrationBean messageDispatcherServlet(ApplicationContext context) {
		MessageDispatcherServlet messageDispatcherServlet = new MessageDispatcherServlet();
		messageDispatcherServlet.setApplicationContext(context);
		messageDispatcherServlet.setTransformWsdlLocations(true);
		return new ServletRegistrationBean(messageDispatcherServlet, "/ws/*");
	}

	// /ws/courses.wsdl
	// course-details.xsd
	@Bean(name = "courses")
	public DefaultWsdl11Definition defaultWsdl11Definition(XsdSchema coursesSchema) {
		DefaultWsdl11Definition definition = new DefaultWsdl11Definition();
		definition.setPortTypeName("CoursePort");
		definition.setTargetNamespace("http://in28minutes.com/courses");
		definition.setLocationUri("/ws");
		definition.setSchema(coursesSchema);
		return definition;
	}

	@Bean
	public XsdSchema coursesSchema() {
		return new SimpleXsdSchema(new ClassPathResource("course-details.xsd"));
	}
	

	//XwsSecurityInterceptor
	@Bean
	public XwsSecurityInterceptor securityInterceptor(){
		XwsSecurityInterceptor securityInterceptor = new XwsSecurityInterceptor();
		//Callback Handler -> SimplePasswordValidationCallbackHandler
		securityInterceptor.setCallbackHandler(callbackHandler());
		//Security Policy -> securityPolicy.xml
		securityInterceptor.setPolicyConfiguration(new ClassPathResource("securityPolicy.xml"));
		return securityInterceptor;
	}
	
	@Bean
	public SimplePasswordValidationCallbackHandler callbackHandler() {
		SimplePasswordValidationCallbackHandler handler = new SimplePasswordValidationCallbackHandler();
		handler.setUsersMap(Collections.singletonMap("user", "password"));
		return handler;
	}

	//Interceptors.add -> XwsSecurityInterceptor
	@Override
	public void addInterceptors(List<EndpointInterceptor> interceptors) {
		interceptors.add(securityInterceptor());
	}

}
```
---

### /src/main/java/com/in28minutes/soap/webservices/soapcoursemanagement/SoapCourseManagementApplication.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SoapCourseManagementApplication {

	public static void main(String[] args) {
		SpringApplication.run(SoapCourseManagementApplication.class, args);
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/main/resources/course-details.xsd

```
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
	targetNamespace="http://in28minutes.com/courses" xmlns:tns="http://in28minutes.com/courses"
	elementFormDefault="qualified">

	<xs:element name="GetCourseDetailsRequest">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="id" type="xs:int" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="GetCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="CourseDetails" type="tns:CourseDetails" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="GetAllCourseDetailsRequest">
		<xs:complexType>
		</xs:complexType>
	</xs:element>

	<xs:element name="GetAllCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="CourseDetails" type="tns:CourseDetails"
					maxOccurs="unbounded" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="DeleteCourseDetailsRequest">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="id" type="xs:int" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:element name="DeleteCourseDetailsResponse">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="status" type="tns:Status" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>

	<xs:simpleType name="Status">
		<xs:restriction base="xs:string">
			<xs:enumeration value="SUCCESS" />
			<xs:enumeration value="FAILURE" />
		</xs:restriction>
	</xs:simpleType>

	<xs:complexType name="CourseDetails">
		<xs:sequence>
			<xs:element name="id" type="xs:int" />
			<xs:element name="name" type="xs:string" />
			<xs:element name="description" type="xs:string" />
		</xs:sequence>
	</xs:complexType>

</xs:schema>
```
---

### /src/main/resources/securityPolicy.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xwss:SecurityConfiguration 
	xmlns:xwss="http://java.sun.com/xml/ns/xwss/config">
	<xwss:RequireUsernameToken
		passwordDigestRequired="false" nonceRequired="false" />
</xwss:SecurityConfiguration>
```
---

### /src/test/java/com/in28minutes/soap/webservices/soapcoursemanagement/SoapCourseManagementApplicationTests.java

```java
package com.in28minutes.soap.webservices.soapcoursemanagement;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SoapCourseManagementApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

# Microservices with Spring Boot and Spring Cloud


## Ports

|     Application       |     Port          |
| ------------- | ------------- |
| Limits Service | 8080, 8081, ... |
| Spring Cloud Config Server | 8888 |
|  |  |
| Currency Exchange Service | 8000, 8001, 8002, ..  |
| Currency Conversion Service | 8100, 8101, 8102, ... |
| Netflix Eureka Naming Server | 8761 |
| Netflix Zuul API Gateway Server | 8765 |
| Zipkin Distributed Tracing Server | 9411 |


## URLs

|     Application       |     URL          |
| ------------- | ------------- |
| Limits Service | http://localhost:8080/limits POST -> http://localhost:8080/actuator/refresh|
|Spring Cloud Config Server| http://localhost:8888/limits-service/default http://localhost:8888/limits-service/dev |
|  Currency Converter Service - Direct Call| http://localhost:8100/currency-converter/from/USD/to/INR/quantity/10|
|  Currency Converter Service - Feign| http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000|
| Currency Exchange Service | http://localhost:8000/currency-exchange/from/EUR/to/INR http://localhost:8001/currency-exchange/from/USD/to/INR|
| Eureka | http://localhost:8761/|
| Zuul - Currency Exchange & Exchange Services | http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10|
| Zipkin | http://localhost:9411/zipkin/ |
| Spring Cloud Bus Refresh | http://localhost:8080/bus/refresh |

## VM Argument

-Dserver.port=8001

## Commands

```
mkdir git-configuration-repo
cd git-configuration-repo/
git init
git add -A
git commit -m "first commit"
```

## Spring Cloud Configuration

```
spring.cloud.config.failFast=true

```

## More Reading about Microservices
- Design and Governance of Microservices
    - https://martinfowler.com/microservices/
- 12 Factor App 
    - https://12factor.net/
    - https://dzone.com/articles/the-12-factor-app-a-java-developers-perspective
- Spring Cloud
    - http://projects.spring.io/spring-cloud/

## Complete Code Example

### /03.microservices/currency-conversion-service/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>currency-conversion-service</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>currency-conversion-service</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-openfeign</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-sleuth</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-bus-amqp</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/currency-conversion-service/src/main/java/com/in28minutes/microservices/currencyconversionservice/CurrencyConversionBean.java

```java
package com.in28minutes.microservices.currencyconversionservice;

import java.math.BigDecimal;

public class CurrencyConversionBean {
	private Long id;
	private String from;
	private String to;
	private BigDecimal conversionMultiple;
	private BigDecimal quantity;
	private BigDecimal totalCalculatedAmount;
	private int port;

	public CurrencyConversionBean() {

	}

	public CurrencyConversionBean(Long id, String from, String to, BigDecimal conversionMultiple, BigDecimal quantity,
			BigDecimal totalCalculatedAmount, int port) {
		super();
		this.id = id;
		this.from = from;
		this.to = to;
		this.conversionMultiple = conversionMultiple;
		this.quantity = quantity;
		this.totalCalculatedAmount = totalCalculatedAmount;
		this.port = port;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getFrom() {
		return from;
	}

	public void setFrom(String from) {
		this.from = from;
	}

	public String getTo() {
		return to;
	}

	public void setTo(String to) {
		this.to = to;
	}

	public BigDecimal getConversionMultiple() {
		return conversionMultiple;
	}

	public void setConversionMultiple(BigDecimal conversionMultiple) {
		this.conversionMultiple = conversionMultiple;
	}

	public BigDecimal getQuantity() {
		return quantity;
	}

	public void setQuantity(BigDecimal quantity) {
		this.quantity = quantity;
	}

	public BigDecimal getTotalCalculatedAmount() {
		return totalCalculatedAmount;
	}

	public void setTotalCalculatedAmount(BigDecimal totalCalculatedAmount) {
		this.totalCalculatedAmount = totalCalculatedAmount;
	}

	public int getPort() {
		return port;
	}

	public void setPort(int port) {
		this.port = port;
	}

}
```
---

### /03.microservices/currency-conversion-service/src/main/java/com/in28minutes/microservices/currencyconversionservice/CurrencyConversionController.java

```java
package com.in28minutes.microservices.currencyconversionservice;

import java.math.BigDecimal;
import java.util.HashMap;
import java.util.Map;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

@RestController
public class CurrencyConversionController {

	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	private CurrencyExchangeServiceProxy proxy;

	@GetMapping("/currency-converter/from/{from}/to/{to}/quantity/{quantity}")
	public CurrencyConversionBean convertCurrency(@PathVariable String from, @PathVariable String to,
			@PathVariable BigDecimal quantity) {

		// Feign - Problem 1
		Map<String, String> uriVariables = new HashMap<>();
		uriVariables.put("from", from);
		uriVariables.put("to", to);

		ResponseEntity<CurrencyConversionBean> responseEntity = new RestTemplate().getForEntity(
				"http://localhost:8000/currency-exchange/from/{from}/to/{to}", CurrencyConversionBean.class,
				uriVariables);

		CurrencyConversionBean response = responseEntity.getBody();

		return new CurrencyConversionBean(response.getId(), from, to, response.getConversionMultiple(), quantity,
				quantity.multiply(response.getConversionMultiple()), response.getPort());
	}

	@GetMapping("/currency-converter-feign/from/{from}/to/{to}/quantity/{quantity}")
	public CurrencyConversionBean convertCurrencyFeign(@PathVariable String from, @PathVariable String to,
			@PathVariable BigDecimal quantity) {

		CurrencyConversionBean response = proxy.retrieveExchangeValue(from, to);

		logger.info("{}", response);
		
		return new CurrencyConversionBean(response.getId(), from, to, response.getConversionMultiple(), quantity,
				quantity.multiply(response.getConversionMultiple()), response.getPort());
	}

}
```
---

### /03.microservices/currency-conversion-service/src/main/java/com/in28minutes/microservices/currencyconversionservice/CurrencyConversionServiceApplication.java

```java
package com.in28minutes.microservices.currencyconversionservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.openfeign.EnableFeignClients;
import org.springframework.context.annotation.Bean;

import brave.sampler.Sampler;

@SpringBootApplication
@EnableFeignClients("com.in28minutes.microservices.currencyconversionservice")
@EnableDiscoveryClient
public class CurrencyConversionServiceApplication {

	public static void main(String[] args) {
		SpringApplication.run(CurrencyConversionServiceApplication.class, args);
	}

	@Bean
	public Sampler defaultSampler() {
		return Sampler.ALWAYS_SAMPLE;
	}

}
```
---

### /03.microservices/currency-conversion-service/src/main/java/com/in28minutes/microservices/currencyconversionservice/CurrencyExchangeServiceProxy.java

```java
package com.in28minutes.microservices.currencyconversionservice;

import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.cloud.netflix.ribbon.RibbonClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

//@FeignClient(name="currency-exchange-service", url="localhost:8000")
//@FeignClient(name="currency-exchange-service")
@FeignClient(name="netflix-zuul-api-gateway-server")
@RibbonClient(name="currency-exchange-service")
public interface CurrencyExchangeServiceProxy {
	//@GetMapping("/currency-exchange/from/{from}/to/{to}")
	@GetMapping("/currency-exchange-service/currency-exchange/from/{from}/to/{to}")
	public CurrencyConversionBean retrieveExchangeValue
		(@PathVariable("from") String from, @PathVariable("to") String to);
}
```
---

### /03.microservices/currency-conversion-service/src/main/resources/application.properties

```properties
spring.application.name=currency-conversion-service
server.port=8100
eureka.client.service-url.default-zone=http://localhost:8761/eureka
#currency-exchange-service.ribbon.listOfServers=http://localhost:8000,http://localhost:8001
```
---

### /03.microservices/currency-conversion-service/src/test/java/com/in28minutes/microservices/currencyconversionservice/CurrencyConversionServiceApplicationTests.java

```java
package com.in28minutes.microservices.currencyconversionservice;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class CurrencyConversionServiceApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /03.microservices/currency-exchange-service/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>currency-exchange-service</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>currency-exchange-service</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-sleuth</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-bus-amqp</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>com.h2database</groupId>
			<artifactId>h2</artifactId>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/currency-exchange-service/src/main/java/com/in28minutes/microservices/currencyexchangeservice/CurrencyExchangeController.java

```java
package com.in28minutes.microservices.currencyexchangeservice;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class CurrencyExchangeController {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private Environment environment;
	
	@Autowired
	private ExchangeValueRepository repository;
	
	@GetMapping("/currency-exchange/from/{from}/to/{to}")
	public ExchangeValue retrieveExchangeValue
		(@PathVariable String from, @PathVariable String to){
		
		ExchangeValue exchangeValue = 
				repository.findByFromAndTo(from, to);
		
		exchangeValue.setPort(
				Integer.parseInt(environment.getProperty("local.server.port")));
		
		logger.info("{}", exchangeValue);
		
		return exchangeValue;
	}
}
```
---

### /03.microservices/currency-exchange-service/src/main/java/com/in28minutes/microservices/currencyexchangeservice/CurrencyExchangeServiceApplication.java

```java
package com.in28minutes.microservices.currencyexchangeservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.context.annotation.Bean;

import brave.sampler.Sampler;

@SpringBootApplication
@EnableDiscoveryClient
public class CurrencyExchangeServiceApplication {

	public static void main(String[] args) {
		SpringApplication.run(CurrencyExchangeServiceApplication.class, args);
	}
	
	@Bean
	public Sampler defaultSampler(){
		return Sampler.ALWAYS_SAMPLE;
	}

}
```
---

### /03.microservices/currency-exchange-service/src/main/java/com/in28minutes/microservices/currencyexchangeservice/ExchangeValue.java

```java
package com.in28minutes.microservices.currencyexchangeservice;

import java.math.BigDecimal;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class ExchangeValue {
	
	@Id
	private Long id;
	
	@Column(name="currency_from")
	private String from;
	
	@Column(name="currency_to")
	private String to;
	
	private BigDecimal conversionMultiple;
	private int port;
	
	public ExchangeValue() {
		
	}
	

	public ExchangeValue(Long id, String from, String to, BigDecimal conversionMultiple) {
		super();
		this.id = id;
		this.from = from;
		this.to = to;
		this.conversionMultiple = conversionMultiple;
	}

    //Getter and Setters

}
```
---

### /03.microservices/currency-exchange-service/src/main/java/com/in28minutes/microservices/currencyexchangeservice/ExchangeValueRepository.java

```java
package com.in28minutes.microservices.currencyexchangeservice;

import org.springframework.data.jpa.repository.JpaRepository;

public interface ExchangeValueRepository extends 
		JpaRepository<ExchangeValue, Long>{
	ExchangeValue findByFromAndTo(String from, String to);
}
```
---

### /03.microservices/currency-exchange-service/src/main/resources/application.properties

```properties
spring.application.name=currency-exchange-service
server.port=8000

spring.jpa.show-sql=true
spring.h2.console.enabled=true

eureka.client.service-url.default-zone=http://localhost:8761/eureka
```
---

### /03.microservices/currency-exchange-service/src/main/resources/data.sql

```
insert into exchange_value(id,currency_from,currency_to,conversion_multiple,port)
values(10001,'USD','INR',65,0);
insert into exchange_value(id,currency_from,currency_to,conversion_multiple,port)
values(10002,'EUR','INR',75,0);
insert into exchange_value(id,currency_from,currency_to,conversion_multiple,port)
values(10003,'AUD','INR',25,0);
```
---

### /03.microservices/currency-exchange-service/src/test/java/com/in28minutes/microservices/currencyexchangeservice/CurrencyExchangeServiceApplicationTests.java

```java
package com.in28minutes.microservices.currencyexchangeservice;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class CurrencyExchangeServiceApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /03.microservices/git-localconfig-repo/limits-service-dev.properties

```properties
limits-service.minimum=1
```
---

### /03.microservices/git-localconfig-repo/limits-service-qa.properties

```properties
limits-service.minimum=2
limits-service.maximum=222
```
---

### /03.microservices/git-localconfig-repo/limits-service.properties

```properties
limits-service.minimum=8
limits-service.maximum=888
management.endpoints.web.exposure.include=*
```
---

### /03.microservices/limits-service/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>limits-service</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>limits-service</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-bus-amqp</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/limits-service/src/main/java/com/in28minutes/microservices/limitsservice/bean/LimitConfiguration.java

```java
package com.in28minutes.microservices.limitsservice.bean;

public class LimitConfiguration {
	private int maximum;
	private int minimum;

	protected LimitConfiguration() {

	}

	public LimitConfiguration(int maximum, int minimum) {
		super();
		this.maximum = maximum;
		this.minimum = minimum;
	}

	public int getMaximum() {
		return maximum;
	}

	public int getMinimum() {
		return minimum;
	}

}
```
---

### /03.microservices/limits-service/src/main/java/com/in28minutes/microservices/limitsservice/Configuration.java

```java
package com.in28minutes.microservices.limitsservice;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties("limits-service")
public class Configuration {
	
	private int minimum;
	private int maximum;

    //Getter and Setters


}
```
---

### /03.microservices/limits-service/src/main/java/com/in28minutes/microservices/limitsservice/LimitsConfigurationController.java

```java
package com.in28minutes.microservices.limitsservice;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import com.in28minutes.microservices.limitsservice.bean.LimitConfiguration;
import com.netflix.hystrix.contrib.javanica.annotation.HystrixCommand;

@RestController
public class LimitsConfigurationController {

	@Autowired
	private Configuration configuration;

	@GetMapping("/limits")
	public LimitConfiguration retrieveLimitsFromConfigurations() {
		LimitConfiguration limitConfiguration = new LimitConfiguration(configuration.getMaximum(), 
				configuration.getMinimum());
		return limitConfiguration;
	}
	
	@GetMapping("/fault-tolerance-example")
	@HystrixCommand(fallbackMethod="fallbackRetrieveConfiguration")
	public LimitConfiguration retrieveConfiguration() {
		throw new RuntimeException("Not available");
	}

	public LimitConfiguration fallbackRetrieveConfiguration() {
		return new LimitConfiguration(999, 9);
	}

}
```
---

### /03.microservices/limits-service/src/main/java/com/in28minutes/microservices/limitsservice/LimitsServiceApplication.java

```java
package com.in28minutes.microservices.limitsservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.hystrix.EnableHystrix;

@SpringBootApplication
@EnableHystrix
public class LimitsServiceApplication {
	public static void main(String[] args) {
		SpringApplication.run(LimitsServiceApplication.class, args);
	}
}
```
---

### /03.microservices/limits-service/src/main/resources/bootstrap.properties

```properties
spring.application.name=limits-service
spring.cloud.config.uri=http://localhost:8888
spring.profiles.active=qa
management.endpoints.web.exposure.include=*
```
---

### /03.microservices/limits-service/src/test/java/com/in28minutes/microservices/limitsservice/LimitsServiceApplicationTests.java

```java
package com.in28minutes.microservices.limitsservice;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class LimitsServiceApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /03.microservices/netflix-eureka-naming-server/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>netflix-eureka-naming-server</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>netflix-eureka-naming-server</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/netflix-eureka-naming-server/src/main/java/com/in28minutes/microservices/netflixeurekanamingserver/NetflixEurekaNamingServerApplication.java

```java
package com.in28minutes.microservices.netflixeurekanamingserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class NetflixEurekaNamingServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(NetflixEurekaNamingServerApplication.class, args);
	}
}
```
---

### /03.microservices/netflix-eureka-naming-server/src/main/resources/application.properties

```properties

spring.application.name=netflix-eureka-naming-server
server.port=8761

eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```
---

### /03.microservices/netflix-eureka-naming-server/src/test/java/com/in28minutes/microservices/netflixeurekanamingserver/NetflixEurekaNamingServerApplicationTests.java

```java
package com.in28minutes.microservices.netflixeurekanamingserver;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class NetflixEurekaNamingServerApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /03.microservices/netflix-zuul-api-gateway-server/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>netflix-zuul-api-gateway-server</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>netflix-zuul-api-gateway-server</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-sleuth</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-bus-amqp</artifactId>
		</dependency>


		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/netflix-zuul-api-gateway-server/src/main/java/com/in28minutes/microservices/netflixzuulapigatewayserver/NetflixZuulApiGatewayServerApplication.java

```java
package com.in28minutes.microservices.netflixzuulapigatewayserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.netflix.zuul.EnableZuulProxy;
import org.springframework.context.annotation.Bean;

import brave.sampler.Sampler;

@EnableZuulProxy
@EnableDiscoveryClient
@SpringBootApplication
public class NetflixZuulApiGatewayServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(NetflixZuulApiGatewayServerApplication.class, args);
	}
	
	@Bean
	public Sampler defaultSampler(){
		return Sampler.ALWAYS_SAMPLE;
	}
}
```
---

### /03.microservices/netflix-zuul-api-gateway-server/src/main/java/com/in28minutes/microservices/netflixzuulapigatewayserver/ZuulLoggingFilter.java

```java
package com.in28minutes.microservices.netflixzuulapigatewayserver;

import javax.servlet.http.HttpServletRequest;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

import com.netflix.zuul.ZuulFilter;
import com.netflix.zuul.context.RequestContext;

@Component
public class ZuulLoggingFilter extends ZuulFilter{

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Override
	public boolean shouldFilter() {
		return true;
	}

	@Override
	public Object run() {
		HttpServletRequest request = 
				RequestContext.getCurrentContext().getRequest();
		logger.info("request -> {} request uri -> {}", 
				request, request.getRequestURI());
		return null;
	}

	@Override
	public String filterType() {
		return "pre";
	}

	@Override
	public int filterOrder() {
		return 1;
	}
}
```
---

### /03.microservices/netflix-zuul-api-gateway-server/src/main/resources/application.properties

```properties
spring.application.name=netflix-zuul-api-gateway-server
server.port=8765
eureka.client.service-url.default-zone=http://localhost:8761/eureka
```
---

### /03.microservices/netflix-zuul-api-gateway-server/src/test/java/com/in28minutes/microservices/netflixzuulapigatewayserver/NetflixZuulApiGatewayServerApplicationTests.java

```java
package com.in28minutes.microservices.netflixzuulapigatewayserver;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class NetflixZuulApiGatewayServerApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /03.microservices/spring-cloud-config-server/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>spring-cloud-config-server</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>spring-cloud-config-server</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-config-server</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-bus-amqp</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/spring-cloud-config-server/src/main/java/com/in28minutes/microservices/springcloudconfigserver/SpringCloudConfigServerApplication.java

```java
package com.in28minutes.microservices.springcloudconfigserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.config.server.EnableConfigServer;

@EnableConfigServer
@SpringBootApplication
public class SpringCloudConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringCloudConfigServerApplication.class, args);
	}
}
```
---

### /03.microservices/spring-cloud-config-server/src/main/resources/application.properties

```properties
spring.application.name=spring-cloud-config-server
server.port=8888
spring.cloud.config.server.git.uri=file:///in28Minutes/git/spring-micro-services/03.microservices/git-localconfig-repo
```
---

### /03.microservices/spring-cloud-config-server/src/test/java/com/in28minutes/microservices/springcloudconfigserver/SpringCloudConfigServerApplicationTests.java

```java
package com.in28minutes.microservices.springcloudconfigserver;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringCloudConfigServerApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /03.microservices/zipkin-distributed-tracing-server/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.microservices</groupId>
	<artifactId>zipkin-distributed-tracing-server</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>zipkin-distributed-tracing-server</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>Finchley.M8</spring-cloud.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin-stream</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-stream-rabbit</artifactId>
		</dependency>

		<dependency>
			<groupId>io.zipkin.java</groupId>
			<artifactId>zipkin-autoconfigure-ui</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

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

### /03.microservices/zipkin-distributed-tracing-server/src/main/java/com/in28minutes/microservices/zipkindistributedtracingserver/ZipkinDistributedTracingServerApplication.java

```java
package com.in28minutes.microservices.zipkindistributedtracingserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import zipkin.server.EnableZipkinServer;

@EnableZipkinServer
@SpringBootApplication
public class ZipkinDistributedTracingServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ZipkinDistributedTracingServerApplication.class, args);
	}
}
```
---

### /03.microservices/zipkin-distributed-tracing-server/src/main/resources/application.properties

```properties
spring.application.name=zipkin-distributed-tracing-server
server.port=9411
```
---

### /03.microservices/zipkin-distributed-tracing-server/src/test/java/com/in28minutes/microservices/zipkindistributedtracingserver/ZipkinDistributedTracingServerApplicationTests.java

```java
package com.in28minutes.microservices.zipkindistributedtracingserver;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class ZipkinDistributedTracingServerApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

##  AOP with Spring and AspectJ



## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.spring.aop</groupId>
	<artifactId>spring-aop</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>spring-aop</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-aop</artifactId>
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

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/AfterAopAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class AfterAopAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@AfterReturning(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()", 
			returning = "result")
	public void afterReturning(JoinPoint joinPoint, Object result) {
		logger.info("{} returned with value {}", joinPoint, result);
	}
	
	@After(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()")
	public void after(JoinPoint joinPoint) {
		logger.info("after execution of {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/CommonJoinPointConfig.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.annotation.Pointcut;

public class CommonJoinPointConfig {
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.data.*.*(..))")
	public void dataLayerExecution(){}
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.business.*.*(..))")
	public void businessLayerExecution(){}
	
	@Pointcut("dataLayerExecution() && businessLayerExecution()")
	public void allLayerExecution(){}
	
	@Pointcut("bean(*dao*)")
	public void beanContainingDao(){}
	
	@Pointcut("within(com.in28minutes.spring.aop.springaop.data..*)")
	public void dataLayerExecutionWithWithin(){}

	@Pointcut("@annotation(com.in28minutes.spring.aop.springaop.aspect.TrackTime)")
	public void trackTimeAnnotation(){}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/MethodExecutionCalculationAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

@Aspect
@Configuration
public class MethodExecutionCalculationAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Around("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.trackTimeAnnotation()")
	public void around(ProceedingJoinPoint joinPoint) throws Throwable {
		long startTime = System.currentTimeMillis();

		joinPoint.proceed();

		long timeTaken = System.currentTimeMillis() - startTime;
		logger.info("Time Taken by {} is {}", joinPoint, timeTaken);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/TrackTime.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface TrackTime {

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/UserAccessAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class UserAccessAspect {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	//What kind of method calls I would intercept
	//execution(* PACKAGE.*.*(..))
	//Weaving & Weaver
	@Before("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.dataLayerExecution()")
	public void before(JoinPoint joinPoint){
		//Advice
		logger.info(" Check for user access ");
		logger.info(" Allowed execution for {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business1.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;
import com.in28minutes.spring.aop.springaop.data.Dao1;

@Service
public class Business1 {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	private Dao1 dao1;
	
	@TrackTime
	public String calculateSomething(){
		//Business Logic
		String value = dao1.retrieveSomething();
		logger.info("In Business - {}", value);
		return value;
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business2.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.data.Dao2;

@Service
public class Business2 {
	
	@Autowired
	private Dao2 dao2;
	
	public String calculateSomething(){
		//Business Logic
		return dao2.retrieveSomething();
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao1.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;

@Repository
public class Dao1 {
	
	@TrackTime
	public String retrieveSomething(){
		return "Dao1";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao2.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

@Repository
public class Dao2 {

	public String retrieveSomething(){
		return "Dao2";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/SpringAopApplication.java

```java
package com.in28minutes.spring.aop.springaop;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.spring.aop.springaop.business.Business1;
import com.in28minutes.spring.aop.springaop.business.Business2;

@SpringBootApplication
public class SpringAopApplication implements CommandLineRunner{
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private Business1 business1;

	@Autowired
	private Business2 business2;
	
	public static void main(String[] args) {
		SpringApplication.run(SpringAopApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		logger.info(business1.calculateSomething());
		logger.info(business2.calculateSomething());
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/test/java/com/in28minutes/spring/aop/springaop/SpringAopApplicationTests.java

```java
package com.in28minutes.spring.aop.springaop;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringAopApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.spring.aop</groupId>
	<artifactId>spring-aop</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>spring-aop</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-aop</artifactId>
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

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/AfterAopAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class AfterAopAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@AfterReturning(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()", 
			returning = "result")
	public void afterReturning(JoinPoint joinPoint, Object result) {
		logger.info("{} returned with value {}", joinPoint, result);
	}
	
	@After(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()")
	public void after(JoinPoint joinPoint) {
		logger.info("after execution of {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/CommonJoinPointConfig.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.annotation.Pointcut;

public class CommonJoinPointConfig {
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.data.*.*(..))")
	public void dataLayerExecution(){}
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.business.*.*(..))")
	public void businessLayerExecution(){}
	
	@Pointcut("dataLayerExecution() && businessLayerExecution()")
	public void allLayerExecution(){}
	
	@Pointcut("bean(*dao*)")
	public void beanContainingDao(){}
	
	@Pointcut("within(com.in28minutes.spring.aop.springaop.data..*)")
	public void dataLayerExecutionWithWithin(){}

	@Pointcut("@annotation(com.in28minutes.spring.aop.springaop.aspect.TrackTime)")
	public void trackTimeAnnotation(){}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/MethodExecutionCalculationAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

@Aspect
@Configuration
public class MethodExecutionCalculationAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Around("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.trackTimeAnnotation()")
	public void around(ProceedingJoinPoint joinPoint) throws Throwable {
		long startTime = System.currentTimeMillis();

		joinPoint.proceed();

		long timeTaken = System.currentTimeMillis() - startTime;
		logger.info("Time Taken by {} is {}", joinPoint, timeTaken);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/TrackTime.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface TrackTime {

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/UserAccessAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class UserAccessAspect {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	//What kind of method calls I would intercept
	//execution(* PACKAGE.*.*(..))
	//Weaving & Weaver
	@Before("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.dataLayerExecution()")
	public void before(JoinPoint joinPoint){
		//Advice
		logger.info(" Check for user access ");
		logger.info(" Allowed execution for {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business1.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;
import com.in28minutes.spring.aop.springaop.data.Dao1;

@Service
public class Business1 {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	private Dao1 dao1;
	
	@TrackTime
	public String calculateSomething(){
		//Business Logic
		String value = dao1.retrieveSomething();
		logger.info("In Business - {}", value);
		return value;
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business2.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.data.Dao2;

@Service
public class Business2 {
	
	@Autowired
	private Dao2 dao2;
	
	public String calculateSomething(){
		//Business Logic
		return dao2.retrieveSomething();
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao1.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;

@Repository
public class Dao1 {
	
	@TrackTime
	public String retrieveSomething(){
		return "Dao1";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao2.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

@Repository
public class Dao2 {

	public String retrieveSomething(){
		return "Dao2";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/SpringAopApplication.java

```java
package com.in28minutes.spring.aop.springaop;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.spring.aop.springaop.business.Business1;
import com.in28minutes.spring.aop.springaop.business.Business2;

@SpringBootApplication
public class SpringAopApplication implements CommandLineRunner{
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private Business1 business1;

	@Autowired
	private Business2 business2;
	
	public static void main(String[] args) {
		SpringApplication.run(SpringAopApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		logger.info(business1.calculateSomething());
		logger.info(business2.calculateSomething());
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/test/java/com/in28minutes/spring/aop/springaop/SpringAopApplicationTests.java

```java
package com.in28minutes.spring.aop.springaop;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringAopApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

##  AOP with Spring and AspectJ

Let's play and learn more about Spring AOP

- Step 01 - Setting up AOP Example - Part 1 
- Step 02 - Setting up AOP Example - Part 2
- Step 03 - Defining an @Before advice
- Step 04 - Understand AOP Terminology - Pointcut, Advice, Aspect, Join Point, Weaving and Weaver
- Step 05 - Using @After, @AfterReturning, @AfterThrowing advices
- Step 06 - Using @Around advice to implement performance tracing
- Step 07 - Best Practice : Use common Pointcut Configuration
- Step 08 - Quick summary of other Pointcuts
- Step 09 - Creating Custom Annotation and an Aspect for Tracking Time

## Complete Code Example


## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.spring.aop</groupId>
	<artifactId>spring-aop</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>spring-aop</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-aop</artifactId>
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

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/AfterAopAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class AfterAopAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@AfterReturning(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()", 
			returning = "result")
	public void afterReturning(JoinPoint joinPoint, Object result) {
		logger.info("{} returned with value {}", joinPoint, result);
	}
	
	@After(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()")
	public void after(JoinPoint joinPoint) {
		logger.info("after execution of {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/CommonJoinPointConfig.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.annotation.Pointcut;

public class CommonJoinPointConfig {
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.data.*.*(..))")
	public void dataLayerExecution(){}
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.business.*.*(..))")
	public void businessLayerExecution(){}
	
	@Pointcut("dataLayerExecution() && businessLayerExecution()")
	public void allLayerExecution(){}
	
	@Pointcut("bean(*dao*)")
	public void beanContainingDao(){}
	
	@Pointcut("within(com.in28minutes.spring.aop.springaop.data..*)")
	public void dataLayerExecutionWithWithin(){}

	@Pointcut("@annotation(com.in28minutes.spring.aop.springaop.aspect.TrackTime)")
	public void trackTimeAnnotation(){}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/MethodExecutionCalculationAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

@Aspect
@Configuration
public class MethodExecutionCalculationAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Around("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.trackTimeAnnotation()")
	public void around(ProceedingJoinPoint joinPoint) throws Throwable {
		long startTime = System.currentTimeMillis();

		joinPoint.proceed();

		long timeTaken = System.currentTimeMillis() - startTime;
		logger.info("Time Taken by {} is {}", joinPoint, timeTaken);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/TrackTime.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface TrackTime {

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/UserAccessAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class UserAccessAspect {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	//What kind of method calls I would intercept
	//execution(* PACKAGE.*.*(..))
	//Weaving & Weaver
	@Before("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.dataLayerExecution()")
	public void before(JoinPoint joinPoint){
		//Advice
		logger.info(" Check for user access ");
		logger.info(" Allowed execution for {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business1.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;
import com.in28minutes.spring.aop.springaop.data.Dao1;

@Service
public class Business1 {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	private Dao1 dao1;
	
	@TrackTime
	public String calculateSomething(){
		//Business Logic
		String value = dao1.retrieveSomething();
		logger.info("In Business - {}", value);
		return value;
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business2.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.data.Dao2;

@Service
public class Business2 {
	
	@Autowired
	private Dao2 dao2;
	
	public String calculateSomething(){
		//Business Logic
		return dao2.retrieveSomething();
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao1.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;

@Repository
public class Dao1 {
	
	@TrackTime
	public String retrieveSomething(){
		return "Dao1";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao2.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

@Repository
public class Dao2 {

	public String retrieveSomething(){
		return "Dao2";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/SpringAopApplication.java

```java
package com.in28minutes.spring.aop.springaop;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.spring.aop.springaop.business.Business1;
import com.in28minutes.spring.aop.springaop.business.Business2;

@SpringBootApplication
public class SpringAopApplication implements CommandLineRunner{
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private Business1 business1;

	@Autowired
	private Business2 business2;
	
	public static void main(String[] args) {
		SpringApplication.run(SpringAopApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		logger.info(business1.calculateSomething());
		logger.info(business2.calculateSomething());
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/test/java/com/in28minutes/spring/aop/springaop/SpringAopApplicationTests.java

```java
package com.in28minutes.spring.aop.springaop;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringAopApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.spring.aop</groupId>
	<artifactId>spring-aop</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>spring-aop</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-aop</artifactId>
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

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/AfterAopAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class AfterAopAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@AfterReturning(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()", 
			returning = "result")
	public void afterReturning(JoinPoint joinPoint, Object result) {
		logger.info("{} returned with value {}", joinPoint, result);
	}
	
	@After(value = "com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.businessLayerExecution()")
	public void after(JoinPoint joinPoint) {
		logger.info("after execution of {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/CommonJoinPointConfig.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.annotation.Pointcut;

public class CommonJoinPointConfig {
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.data.*.*(..))")
	public void dataLayerExecution(){}
	
	@Pointcut("execution(* com.in28minutes.spring.aop.springaop.business.*.*(..))")
	public void businessLayerExecution(){}
	
	@Pointcut("dataLayerExecution() && businessLayerExecution()")
	public void allLayerExecution(){}
	
	@Pointcut("bean(*dao*)")
	public void beanContainingDao(){}
	
	@Pointcut("within(com.in28minutes.spring.aop.springaop.data..*)")
	public void dataLayerExecutionWithWithin(){}

	@Pointcut("@annotation(com.in28minutes.spring.aop.springaop.aspect.TrackTime)")
	public void trackTimeAnnotation(){}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/MethodExecutionCalculationAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

@Aspect
@Configuration
public class MethodExecutionCalculationAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Around("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.trackTimeAnnotation()")
	public void around(ProceedingJoinPoint joinPoint) throws Throwable {
		long startTime = System.currentTimeMillis();

		joinPoint.proceed();

		long timeTaken = System.currentTimeMillis() - startTime;
		logger.info("Time Taken by {} is {}", joinPoint, timeTaken);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/TrackTime.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface TrackTime {

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/aspect/UserAccessAspect.java

```java
package com.in28minutes.spring.aop.springaop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Configuration;

//AOP
//Configuration
@Aspect
@Configuration
public class UserAccessAspect {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	//What kind of method calls I would intercept
	//execution(* PACKAGE.*.*(..))
	//Weaving & Weaver
	@Before("com.in28minutes.spring.aop.springaop.aspect.CommonJoinPointConfig.dataLayerExecution()")
	public void before(JoinPoint joinPoint){
		//Advice
		logger.info(" Check for user access ");
		logger.info(" Allowed execution for {}", joinPoint);
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business1.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;
import com.in28minutes.spring.aop.springaop.data.Dao1;

@Service
public class Business1 {
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	private Dao1 dao1;
	
	@TrackTime
	public String calculateSomething(){
		//Business Logic
		String value = dao1.retrieveSomething();
		logger.info("In Business - {}", value);
		return value;
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/business/Business2.java

```java
package com.in28minutes.spring.aop.springaop.business;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.in28minutes.spring.aop.springaop.data.Dao2;

@Service
public class Business2 {
	
	@Autowired
	private Dao2 dao2;
	
	public String calculateSomething(){
		//Business Logic
		return dao2.retrieveSomething();
	}
}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao1.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

import com.in28minutes.spring.aop.springaop.aspect.TrackTime;

@Repository
public class Dao1 {
	
	@TrackTime
	public String retrieveSomething(){
		return "Dao1";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/data/Dao2.java

```java
package com.in28minutes.spring.aop.springaop.data;

import org.springframework.stereotype.Repository;

@Repository
public class Dao2 {

	public String retrieveSomething(){
		return "Dao2";
	}

}
```
---

### /src/main/java/com/in28minutes/spring/aop/springaop/SpringAopApplication.java

```java
package com.in28minutes.spring.aop.springaop;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.spring.aop.springaop.business.Business1;
import com.in28minutes.spring.aop.springaop.business.Business2;

@SpringBootApplication
public class SpringAopApplication implements CommandLineRunner{
	
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private Business1 business1;

	@Autowired
	private Business2 business2;
	
	public static void main(String[] args) {
		SpringApplication.run(SpringAopApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		logger.info(business1.calculateSomething());
		logger.info(business2.calculateSomething());
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/test/java/com/in28minutes/spring/aop/springaop/SpringAopApplicationTests.java

```java
package com.in28minutes.spring.aop.springaop;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringAopApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---


## First 5 Steps in Eclipse


## Complete Code Example


### /src/HelloWorld.java

```java
import java.util.HashMap;
import java.util.Map;

public class HelloWorld {
	public static void main(String[] args) {
		Map<String, String> map = new HashMap<String, String>();
		map.put("key", "value");
	}
}
```
---

### /src/Person.java

```java
public class Person {
	private String firstName;
	private String lastName;
	private String ssn;

	public Person(String firstName, String lastName, String ssn) {
		super();
		this.firstName = firstName;
		this.lastName = lastName;
		this.ssn = ssn;
	}

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}

	public String getSsn() {
		return ssn;
	}

	public void setSsn(String ssn) {
		this.ssn = ssn;
	}

	@Override
	public String toString() {
		return String.format("Person [firstName=%s, lastName=%s, ssn=%s]", firstName, lastName, ssn);
	}

}
// Alt + Shift + S
// Cmd + Option + S
```
---

## First 5 Steps in Maven

## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.learning.maven</groupId>
	<artifactId>maven-in-few-steps</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	
	<packaging>jar</packaging>

	<name>maven-in-few-steps</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
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
<!--

Remote Maven Repository
-> 
Local Maven Repository
  
 - Local Repository => Local System

 - Remote Maven repository => Central Repositories
   - stores all the versions of all dependencies. JUnit 4.2,4.3,4.4

 - mvn install vs mvn deploy 
   - copies the created jar to local maven repository - a temp folder on my machine where maven stores the files.
-->
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

### /src/main/java/com/in28minutes/learning/maven/maveninfewsteps/MavenInFewStepsApplication.java

```java
package com.in28minutes.learning.maven.maveninfewsteps;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MavenInFewStepsApplication {

	public static void main(String[] args) {
		SpringApplication.run(MavenInFewStepsApplication.class, args);
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/test/java/com/in28minutes/learning/maven/maveninfewsteps/MavenInFewStepsApplicationTests.java

```java
package com.in28minutes.learning.maven.maveninfewsteps;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class MavenInFewStepsApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

## First 5 Steps in JUnit


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

## First 5 Steps in Mockito


## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.mockito</groupId>
	<artifactId>mockito-demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>mockito-demo</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
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

### /src/main/java/com/in28minutes/mockito/mockitodemo/DataService.java

```java
package com.in28minutes.mockito.mockitodemo;

public interface DataService {
	int[] retrieveAllData();
}
```
---

### /src/main/java/com/in28minutes/mockito/mockitodemo/MockitoDemoApplication.java

```java
package com.in28minutes.mockito.mockitodemo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MockitoDemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(MockitoDemoApplication.class, args);
	}
}
```
---

### /src/main/java/com/in28minutes/mockito/mockitodemo/SomeBusinessImpl.java

```java
package com.in28minutes.mockito.mockitodemo;

public class SomeBusinessImpl {
	private DataService dataService;

	public SomeBusinessImpl(DataService dataService) {
		super();
		this.dataService = dataService;
	}

	int findTheGreatestFromAllData() {
		int[] data = dataService.retrieveAllData();
		int greatest = Integer.MIN_VALUE;

		for (int value : data) {
			if (value > greatest) {
				greatest = value;
			}
		}
		return greatest;
	}
}
```
---

### /src/main/resources/application.properties

```properties
```
---

### /src/test/java/com/in28minutes/mockito/mockitodemo/ListTest.java

```java
package com.in28minutes.mockito.mockitodemo;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.when;

import java.util.List;

import org.junit.Test;
import org.mockito.Mockito;

public class ListTest {

	@Test
	public void testSize() {
		List listMock = mock(List.class);
		when(listMock.size()).thenReturn(10);
		assertEquals(10, listMock.size());
		assertEquals(10, listMock.size());
	}

	@Test
	public void testSize_multipleReturns() {
		List listMock = mock(List.class);
		when(listMock.size()).thenReturn(10).thenReturn(20);
		assertEquals(10, listMock.size());
		assertEquals(20, listMock.size());
		assertEquals(20, listMock.size());
	}

	@Test
	public void testGet_SpecificParameter() {
		List listMock = mock(List.class);
		when(listMock.get(0)).thenReturn("SomeString");
		assertEquals("SomeString", listMock.get(0));
		assertEquals(null, listMock.get(1));
	}

	@Test
	public void testGet_GenericParameter() {
		List listMock = mock(List.class);
		when(listMock.get(Mockito.anyInt())).thenReturn("SomeString");
		assertEquals("SomeString", listMock.get(0));
		assertEquals("SomeString", listMock.get(1));
	}
}
```
---

### /src/test/java/com/in28minutes/mockito/mockitodemo/MockitoDemoApplicationTests.java

```java
package com.in28minutes.mockito.mockitodemo;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class MockitoDemoApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /src/test/java/com/in28minutes/mockito/mockitodemo/SomeBusinessMockAnnotationsTest.java

```java
package com.in28minutes.mockito.mockitodemo;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.when;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.MockitoJUnitRunner;

@RunWith(MockitoJUnitRunner.class)
public class SomeBusinessMockAnnotationsTest {

	@Mock
	DataService dataServiceMock;

	@InjectMocks
	SomeBusinessImpl businessImpl;

	@Test
	public void testFindTheGreatestFromAllData() {
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] { 24, 15, 3 });
		assertEquals(24, businessImpl.findTheGreatestFromAllData());
	}

	@Test
	public void testFindTheGreatestFromAllData_ForOneValue() {
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] { 15 });
		assertEquals(15, businessImpl.findTheGreatestFromAllData());
	}

	@Test
	public void testFindTheGreatestFromAllData_NoValues() {
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] {});
		assertEquals(Integer.MIN_VALUE, businessImpl.findTheGreatestFromAllData());
	}
}
```
---

### /src/test/java/com/in28minutes/mockito/mockitodemo/SomeBusinessMockTest.java

```java
package com.in28minutes.mockito.mockitodemo;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.when;

import org.junit.Test;

public class SomeBusinessMockTest {

	@Test
	public void testFindTheGreatestFromAllData() {
		DataService dataServiceMock = mock(DataService.class);
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] { 24, 15, 3 });
		SomeBusinessImpl businessImpl = new SomeBusinessImpl(dataServiceMock);
		int result = businessImpl.findTheGreatestFromAllData();
		assertEquals(24, result);
	}

	@Test
	public void testFindTheGreatestFromAllData_ForOneValue() {
		DataService dataServiceMock = mock(DataService.class);
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] { 15 });
		SomeBusinessImpl businessImpl = new SomeBusinessImpl(dataServiceMock);
		int result = businessImpl.findTheGreatestFromAllData();
		assertEquals(15, result);
	}

}
```
---

### /src/test/java/com/in28minutes/mockito/mockitodemo/SomeBusinessStubTest.java

```java
package com.in28minutes.mockito.mockitodemo;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

public class SomeBusinessStubTest {
	@Test
	public void testFindTheGreatestFromAllData() {
		SomeBusinessImpl businessImpl = new SomeBusinessImpl(new DataServiceStub());
		int result = businessImpl.findTheGreatestFromAllData();
		assertEquals(24, result);

	}

}

class DataServiceStub implements DataService {
	@Override
	public int[] retrieveAllData() {
		return new int[] { 24, 6, 15 };
	}
}
```
---

##  First 10 Steps in Spring Boot

- Step 1 : Introduction to Spring Boot - Goals and Important Features
- Step 2 : Developing Spring Applications before Spring Boot
- Step 3 : Using Spring Initializr to create a Spring Boot Application
- Step 4 : Creating a Simple REST Controller
- Step 5 : What is Spring Boot Auto Configuration?
- Step 6 : Spring Boot vs Spring vs Spring MVC
- Step 7 : Spring Boot Starter Projects - Starter Web and Starter JPA
- Step 8 : Overview of different Spring Boot Starter Projects
- Step 9 : Spring Boot Actuator
- Step 10 : Spring Boot Developer Tools
- Spring Boot - Conclusion

## Complete Code Example
---

### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.springboot.basics</groupId>
	<artifactId>springboot-in-10-steps</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>springboot-in-10-steps</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.data</groupId>
			<artifactId>spring-data-rest-hal-browser</artifactId>
		</dependency>

<!-- 
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		 -->
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
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

### /src/main/java/com/in28minutes/springboot/basics/springbootin10steps/Book.java

```java
package com.in28minutes.springboot.basics.springbootin10steps;

public class Book {
	long id;
	String name;
	String author;

	public Book(long id, String name, String author) {
		super();
		this.id = id;
		this.name = name;
		this.author = author;
	}

	public long getId() {
		return id;
	}

	public String getName() {
		return name;
	}

	public String getAuthor() {
		return author;
	}

	@Override
	public String toString() {
		return String.format("Book [id=%s, name=%s, author=%s]", id, name, author);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/basics/springbootin10steps/BooksController.java

```java
package com.in28minutes.springboot.basics.springbootin10steps;

import java.util.Arrays;
import java.util.List;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class BooksController {
	@GetMapping("/books")
	public List<Book> getAllBooks() {
		return Arrays.asList(
				new Book(1l, "Mastering Spring 5.2", "Ranga Karanam"));
	}
}
```
---

### /src/main/java/com/in28minutes/springboot/basics/springbootin10steps/SpringbootIn10StepsApplication.java

```java
package com.in28minutes.springboot.basics.springbootin10steps;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class SpringbootIn10StepsApplication {

	public static void main(String[] args) {
		ApplicationContext applicationContext = 
				SpringApplication.run(SpringbootIn10StepsApplication.class, args);
		
		for (String name : applicationContext.getBeanDefinitionNames()) {
			System.out.println(name);
		}
	}
}
```
---

### /src/main/resources/application.properties

```properties
#logging.level.org.springframework = DEBUG
management.endpoints.web.exposure.include=*
```
---

### /src/test/java/com/in28minutes/springboot/basics/springbootin10steps/SpringbootIn10StepsApplicationTests.java

```java
package com.in28minutes.springboot.basics.springbootin10steps;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringbootIn10StepsApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

##  Basics of Web Application with Spring MVC

## Complete Code Example

### /pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.in28minutes</groupId>
	<artifactId>in28Minutes-springmvc</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<dependencies>
		<dependency>
			<groupId>javax</groupId>
			<artifactId>javaee-web-api</artifactId>
			<version>6.0</version>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>4.2.2.RELEASE</version>
		</dependency>

		<dependency>
			<groupId>log4j</groupId>
			<artifactId>log4j</artifactId>
			<version>1.2.17</version>
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
						<source>1.8</source>
						<target>1.8</target>
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
### /src/main/java/com/in28minutes/login/LoginController.java
```
package com.in28minutes.login;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class LoginController {

	@Autowired
	private LoginService loginService;

	@RequestMapping(value = "/login", method = RequestMethod.GET)
	public String showLoginPage() {
		return "login";
	}

	@RequestMapping(value = "/login", method = RequestMethod.POST)
	public String handleUserLogin(ModelMap model, @RequestParam String name,
			@RequestParam String password) {

		if (!loginService.validateUser(name, password)) {
			model.put("errorMessage", "Invalid Credentials");
			return "login";
		}

		model.put("name", name);
		return "welcome";
	}
}
```
### /src/main/java/com/in28minutes/login/LoginService.java
```
package com.in28minutes.login;

import org.springframework.stereotype.Service;

@Service
public class LoginService {
	public boolean validateUser(String user, String password) {
		return user.equalsIgnoreCase("in28Minutes") && password.equals("dummy");
	}

}
```
### /src/main/resources/log4j.properties
```
log4j.rootLogger=TRACE, Appender1, Appender2
 
log4j.appender.Appender1=org.apache.log4j.ConsoleAppender
log4j.appender.Appender1.layout=org.apache.log4j.PatternLayout
log4j.appender.Appender1.layout.ConversionPattern=%-7p %d [%t] %c %x - %m%n
 
```
### /src/main/webapp/WEB-INF/todo-servlet.xml
```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.in28minutes" />

    <mvc:annotation-driven />
    
    <bean
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix">
            <value>/WEB-INF/views/</value>
        </property>
        <property name="suffix">
            <value>.jsp</value>
        </property>
    </bean>
    
</beans>
```
### /src/main/webapp/WEB-INF/views/login.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
    <p><font color="red">${errorMessage}</font></p>
    <form action="/login" method="POST">
        Name : <input name="name" type="text" /> Password : <input name="password" type="password" /> <input type="submit" />
    </form>
</body>
</html>
```
### /src/main/webapp/WEB-INF/views/welcome.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
Welcome ${name}. You are now authenticated.
</body>
</html>
```
### /src/main/webapp/WEB-INF/web.xml
```
<web-app xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
    version="3.0">

    <display-name>To do List</display-name>

    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>
            org.springframework.web.servlet.DispatcherServlet
        </servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/todo-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

# Master JPA and Hibernate with Spring Boot


## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.database</groupId>
	<artifactId>database-demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>database-demo</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
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
			<artifactId>spring-boot-starter-jdbc</artifactId>
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

### /src/main/java/com/in28minutes/database/databasedemo/entity/Person.java

```java
package com.in28minutes.database.databasedemo.entity;

import java.util.Date;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.NamedQuery;

@Entity
@NamedQuery(name="find_all_persons", query="select p from Person p")
public class Person {

	@Id
	@GeneratedValue
	private int id;

	private String name;
	private String location;
	private Date birthDate;

	public Person() {

	}

	public Person(int id, String name, String location, Date birthDate) {
		super();
		this.id = id;
		this.name = name;
		this.location = location;
		this.birthDate = birthDate;
	}

	public Person(String name, String location, Date birthDate) {
		super();
		this.name = name;
		this.location = location;
		this.birthDate = birthDate;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getLocation() {
		return location;
	}

	public void setLocation(String location) {
		this.location = location;
	}

	public Date getBirthDate() {
		return birthDate;
	}

	public void setBirthDate(Date birthDate) {
		this.birthDate = birthDate;
	}

	@Override
	public String toString() {
		return String.format("\nPerson [id=%s, name=%s, location=%s, birthDate=%s]", id, name, location, birthDate);
	}

}
```
---

### /src/main/java/com/in28minutes/database/databasedemo/jdbc/PersonJbdcDao.java

```java
package com.in28minutes.database.databasedemo.jdbc;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Timestamp;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Repository;

import com.in28minutes.database.databasedemo.entity.Person;

@Repository
public class PersonJbdcDao {

	@Autowired
	JdbcTemplate jdbcTemplate;
	
	class PersonRowMapper implements RowMapper<Person>{
		@Override
		public Person mapRow(ResultSet rs, int rowNum) throws SQLException {
			Person person = new Person();
			person.setId(rs.getInt("id"));
			person.setName(rs.getString("name"));
			person.setLocation(rs.getString("location"));
			person.setBirthDate(rs.getTimestamp("birth_date"));
			return person;
		}
		
	}
	
	public List<Person> findAll() {
		return jdbcTemplate.query("select * from person", new PersonRowMapper());
	}

	public Person findById(int id) {
		return jdbcTemplate.queryForObject("select * from person where id=?", new Object[] { id },
				new BeanPropertyRowMapper<Person>(Person.class));
	}

	public int deleteById(int id) {
		return jdbcTemplate.update("delete from person where id=?", new Object[] { id });
	}

	public int insert(Person person) {
		return jdbcTemplate.update("insert into person (id, name, location, birth_date) " + "values(?,  ?, ?, ?)",
				new Object[] { person.getId(), person.getName(), person.getLocation(),
						new Timestamp(person.getBirthDate().getTime()) });
	}

	public int update(Person person) {
		return jdbcTemplate.update("update person " + " set name = ?, location = ?, birth_date = ? " + " where id = ?",
				new Object[] { person.getName(), person.getLocation(), new Timestamp(person.getBirthDate().getTime()),
						person.getId() });
	}

}
```
---

### /src/main/java/com/in28minutes/database/databasedemo/jpa/PersonJpaRepository.java

```java
package com.in28minutes.database.databasedemo.jpa;

import java.util.List;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.persistence.TypedQuery;
import javax.transaction.Transactional;

import org.springframework.stereotype.Repository;

import com.in28minutes.database.databasedemo.entity.Person;

@Repository
@Transactional
public class PersonJpaRepository {

	// connect to the database
	@PersistenceContext
	EntityManager entityManager;

	public List<Person> findAll() {
		TypedQuery<Person> namedQuery = entityManager.createNamedQuery("find_all_persons", Person.class);
		return namedQuery.getResultList();
	}

	public Person findById(int id) {
		return entityManager.find(Person.class, id);// JPA
	}

	public Person update(Person person) {
		return entityManager.merge(person);
	}

	public Person insert(Person person) {
		return entityManager.merge(person);
	}

	public void deleteById(int id) {
		Person person = findById(id);
		entityManager.remove(person);
	}

}
```
---

### /src/main/java/com/in28minutes/database/databasedemo/JpaDemoApplication.java

```java
package com.in28minutes.database.databasedemo;

import java.util.Date;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.database.databasedemo.entity.Person;
import com.in28minutes.database.databasedemo.jpa.PersonJpaRepository;

@SpringBootApplication
public class JpaDemoApplication implements CommandLineRunner {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	PersonJpaRepository repository;

	public static void main(String[] args) {
		SpringApplication.run(JpaDemoApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		
		logger.info("User id 10001 -> {}", repository.findById(10001));
		
		logger.info("Inserting -> {}", 
				repository.insert(new Person("Tara", "Berlin", new Date())));
		
		logger.info("Update 10003 -> {}", 
				repository.update(new Person(10003, "Pieter", "Utrecht", new Date())));
		
		repository.deleteById(10002);

		logger.info("All users -> {}", repository.findAll());
	}
}
```
---

### /src/main/java/com/in28minutes/database/databasedemo/SpringJdbcDemoApplication.java

```java
package com.in28minutes.database.databasedemo;

import java.util.Date;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.database.databasedemo.entity.Person;
import com.in28minutes.database.databasedemo.jdbc.PersonJbdcDao;

//@SpringBootApplication
public class SpringJdbcDemoApplication implements CommandLineRunner {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	PersonJbdcDao dao;

	public static void main(String[] args) {
		SpringApplication.run(SpringJdbcDemoApplication.class, args);
	}

	@Override
	public void run(String... args) throws Exception {
		
		logger.info("All users -> {}", dao.findAll());
		
		logger.info("User id 10001 -> {}", dao.findById(10001));
		
		logger.info("Deleting 10002 -> No of Rows Deleted - {}", 
				dao.deleteById(10002));
		
		logger.info("Inserting 10004 -> {}", 
				dao.insert(new Person(10004, "Tara", "Berlin", new Date())));
		
		logger.info("Update 10003 -> {}", 
				dao.update(new Person(10003, "Pieter", "Utrecht", new Date())));
		
	}
}
```
---

### /src/main/resources/application.properties

```properties
spring.h2.console.enabled=true
spring.jpa.show-sql=true
#logging.level.root=debug
```
---

### /src/main/resources/data.sql

```
/*
create table person
(
   id integer not null,
   name varchar(255) not null,
   location varchar(255),
   birth_date timestamp,
   primary key(id)
);
*/

INSERT INTO PERSON (ID, NAME, LOCATION, BIRTH_DATE ) 
VALUES(10001,  'Ranga', 'Hyderabad',sysdate());
INSERT INTO PERSON (ID, NAME, LOCATION, BIRTH_DATE ) 
VALUES(10002,  'James', 'New York',sysdate());
INSERT INTO PERSON (ID, NAME, LOCATION, BIRTH_DATE ) 
VALUES(10003,  'Pieter', 'Amsterdam',sysdate());

```
---

### /src/test/java/com/in28minutes/database/databasedemo/SpringJdbcDemoApplicationTests.java

```java
package com.in28minutes.database.databasedemo;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringJdbcDemoApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

##  JPA & Hibernate in Depth



## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.in28minutes.jpa.hibernate</groupId>
	<artifactId>demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>demo</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.0.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
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
			<artifactId>spring-boot-starter-data-rest</artifactId>
		</dependency>
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-ehcache</artifactId>
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

### /src/main/java/com/in28minutes/jpa/hibernate/demo/DemoApplication.java

```java
package com.in28minutes.jpa.hibernate.demo;

import java.math.BigDecimal;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.in28minutes.jpa.hibernate.demo.entity.FullTimeEmployee;
import com.in28minutes.jpa.hibernate.demo.entity.PartTimeEmployee;
import com.in28minutes.jpa.hibernate.demo.repository.CourseRepository;
import com.in28minutes.jpa.hibernate.demo.repository.EmployeeRepository;
import com.in28minutes.jpa.hibernate.demo.repository.StudentRepository;

@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private CourseRepository courseRepository;

	@Autowired
	private StudentRepository studentRepository;

	@Autowired
	private EmployeeRepository employeeRepository;

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

	@Override
	public void run(String... arg0) throws Exception {
		// studentRepository.saveStudentWithPassport();
		// repository.playWithEntityManager();
		// courseRepository.addHardcodedReviewsForCourse();
		// List<Review> reviews = new ArrayList<>();

		// reviews.add(new Review("5", "Great Hands-on Stuff."));
		// reviews.add(new Review("5", "Hatsoff."));

		// courseRepository.addReviewsForCourse(10003L, reviews );
		// studentRepository.insertHardcodedStudentAndCourse();
		// studentRepository.insertStudentAndCourse(new Student("Jack"),
		// new Course("Microservices in 100 Steps"));

		// Jack FullTimeEmployee salary - 10000$
		// Jill PartTimeEmployee - 50$ per hour
		/*
		employeeRepository.insert(new PartTimeEmployee("Jill", new BigDecimal("50")));
		employeeRepository.insert(new FullTimeEmployee("Jack", new BigDecimal("10000")));

		logger.info("Full Time Employees -> {}", 
				employeeRepository.retrieveAllFullTimeEmployees());
		
		logger.info("Part Time Employees -> {}", 
				employeeRepository.retrieveAllPartTimeEmployees());*/
	}
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/Address.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import javax.persistence.Embeddable;

@Embeddable
public class Address {
	protected Address() {}
	
	public Address(String line1, String line2, String city) {
		super();
		this.line1 = line1;
		this.line2 = line2;
		this.city = city;
	}

	private String line1;
	private String line2;
	private String city;

	
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/Course.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;

import javax.persistence.Cacheable;
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.ManyToMany;
import javax.persistence.NamedQueries;
import javax.persistence.NamedQuery;
import javax.persistence.OneToMany;
import javax.persistence.PreRemove;

import org.hibernate.annotations.CreationTimestamp;
import org.hibernate.annotations.SQLDelete;
import org.hibernate.annotations.UpdateTimestamp;
import org.hibernate.annotations.Where;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.fasterxml.jackson.annotation.JsonIgnore;

@Entity
@NamedQueries(value = { 
		@NamedQuery(name = "query_get_all_courses", 
				query = "Select  c  From Course c"),		
		@NamedQuery(name = "query_get_all_courses_join_fetch", 
		query = "Select  c  From Course c JOIN FETCH c.students s"),		
		@NamedQuery(name = "query_get_100_Step_courses", 
		query = "Select  c  From Course c where name like '%100 Steps'") })
@Cacheable
@SQLDelete(sql="update course set is_deleted=true where id=?")
@Where(clause="is_deleted = false")
public class Course {

	private static Logger LOGGER = LoggerFactory.getLogger(Course.class);
	
	@Id
	@GeneratedValue
	private Long id;

	@Column(nullable = false)
	private String name;

	@OneToMany(mappedBy="course")
	private List<Review> reviews = new ArrayList<>();
	
	@ManyToMany(mappedBy="courses")
	@JsonIgnore
	private List<Student> students = new ArrayList<>();
	
	@UpdateTimestamp
	private LocalDateTime lastUpdatedDate;

	@CreationTimestamp
	private LocalDateTime createdDate;
	
	private boolean isDeleted;
	
	@PreRemove
	private void preRemove(){
		LOGGER.info("Setting isDeleted to True");
		this.isDeleted = true;
	}

	protected Course() {
	}

	public Course(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	
	public List<Review> getReviews() {
		return reviews;
	}

	public void addReview(Review review) {
		this.reviews.add(review);
	}

	public void removeReview(Review review) {
		this.reviews.remove(review);
	}

	public List<Student> getStudents() {
		return students;
	}

	public void addStudent(Student student) {
		this.students.add(student);
	}

	public Long getId() {
		return id;
	}

	@Override
	public String toString() {
		return String.format("Course[%s]", name);
	}
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/Employee.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import javax.persistence.Column;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.MappedSuperclass;

@MappedSuperclass
//@Entity
//@Inheritance(strategy=InheritanceType.JOINED)
public abstract class Employee {

	@Id
	@GeneratedValue
	private Long id;

	@Column(nullable = false)
	private String name;

	protected Employee() {
	}

	public Employee(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Long getId() {
		return id;
	}

	@Override
	public String toString() {
		return String.format("Employee[%s]", name);
	}
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/FullTimeEmployee.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import java.math.BigDecimal;

import javax.persistence.Entity;

@Entity
public class FullTimeEmployee extends Employee {
	protected FullTimeEmployee() {
	}

	public FullTimeEmployee(String name, BigDecimal salary) {
		super(name);
		this.salary = salary;
	}

	private BigDecimal salary;

}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/PartTimeEmployee.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import java.math.BigDecimal;

import javax.persistence.Entity;

@Entity
public class PartTimeEmployee extends Employee {

	protected PartTimeEmployee() {
	}

	public PartTimeEmployee(String name, BigDecimal hourlyWage) {
		super(name);
		this.hourlyWage = hourlyWage;
	}

	private BigDecimal hourlyWage;

}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/Passport.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.FetchType;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.OneToOne;

@Entity
public class Passport {

	@Id
	@GeneratedValue
	private Long id;

	@Column(nullable = false)
	private String number;
	
	@OneToOne(fetch=FetchType.LAZY, mappedBy="passport")
	private Student student;

	protected Passport() {
	}

	public Passport(String number) {
		this.number = number;
	}

	public String getNumber() {
		return number;
	}

	public void setNumber(String number) {
		this.number = number;
	}

	public Student getStudent() {
		return student;
	}

	public void setStudent(Student student) {
		this.student = student;
	}

	public Long getId() {
		return id;
	}

	@Override
	public String toString() {
		return String.format("Passport[%s]", number);
	}
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/Review.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import javax.persistence.Entity;
import javax.persistence.EnumType;
import javax.persistence.Enumerated;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.ManyToOne;

@Entity
public class Review {

	@Id
	@GeneratedValue
	private Long id;

	@Enumerated(EnumType.STRING)
	private ReviewRating rating;

	private String description;

	@ManyToOne
	private Course course;

	protected Review() {
	}

	public Review(ReviewRating rating, String description) {
		this.rating = rating;
		this.description = description;
	}

	public String getDescription() {
		return description;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	public ReviewRating getRating() {
		return rating;
	}

	public void setRating(ReviewRating rating) {
		this.rating = rating;
	}

	public Course getCourse() {
		return course;
	}

	public void setCourse(Course course) {
		this.course = course;
	}

	public Long getId() {
		return id;
	}

	@Override
	public String toString() {
		return String.format("Review[%s %s]", rating, description);
	}

}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/ReviewRating.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

public enum ReviewRating {
	ZERO, ONE, TWO, THREE, FOUR, FIVE
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/entity/Student.java

```java
package com.in28minutes.jpa.hibernate.demo.entity;

import java.util.ArrayList;
import java.util.List;

import javax.persistence.Column;
import javax.persistence.Embedded;
import javax.persistence.Entity;
import javax.persistence.FetchType;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.JoinColumn;
import javax.persistence.JoinTable;
import javax.persistence.ManyToMany;
import javax.persistence.OneToOne;

@Entity
public class Student {

	@Id
	@GeneratedValue
	private Long id;

	@Column(nullable = false)
	private String name;

	@Embedded
	private Address address;

	@OneToOne(fetch = FetchType.LAZY)
	private Passport passport;

	@ManyToMany
	@JoinTable(name = "STUDENT_COURSE", joinColumns = @JoinColumn(name = "STUDENT_ID"), inverseJoinColumns = @JoinColumn(name = "COURSE_ID"))
	private List<Course> courses = new ArrayList<>();

	protected Student() {
	}

	public Student(String name) {
		this.name = name;
	}

	public Address getAddress() {
		return address;
	}

	public void setAddress(Address address) {
		this.address = address;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Passport getPassport() {
		return passport;
	}

	public void setPassport(Passport passport) {
		this.passport = passport;
	}

	public List<Course> getCourses() {
		return courses;
	}

	public void addCourse(Course course) {
		this.courses.add(course);
	}

	public Long getId() {
		return id;
	}

	@Override
	public String toString() {
		return String.format("Student[%s]", name);
	}
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/repository/CourseRepository.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import javax.persistence.EntityManager;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.entity.Course;
import com.in28minutes.jpa.hibernate.demo.entity.Review;
import com.in28minutes.jpa.hibernate.demo.entity.ReviewRating;

@Repository
@Transactional
public class CourseRepository {

	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	EntityManager em;

	public Course findById(Long id) {
		Course course = em.find(Course.class, id);
		logger.info("Course -> {}", course);
		return course;
	}

	public Course save(Course course) {

		if (course.getId() == null) {
			em.persist(course);
		} else {
			em.merge(course);
		}

		return course;
	}

	public void deleteById(Long id) {
		Course course = findById(id);
		em.remove(course);
	}

	public void playWithEntityManager() {
		Course course1 = new Course("Web Services in 100 Steps");
		em.persist(course1);
		
		Course course2 = findById(10001L);
		
		course2.setName("JPA in 50 Steps - Updated");
		
	}

	public void addHardcodedReviewsForCourse() {
		//get the course 10003
		Course course = findById(10003L);
		logger.info("course.getReviews() -> {}", course.getReviews());
		
		//add 2 reviews to it
		Review review1 = new Review(ReviewRating.FIVE, "Great Hands-on Stuff.");	
		Review review2 = new Review(ReviewRating.FIVE, "Hatsoff.");
		
		//setting the relationship
		course.addReview(review1);
		review1.setCourse(course);
		
		course.addReview(review2);
		review2.setCourse(course);
		
		//save it to the database
		em.persist(review1);
		em.persist(review2);
	}
	
	public void addReviewsForCourse(Long courseId, List<Review> reviews) {		
		Course course = findById(courseId);
		logger.info("course.getReviews() -> {}", course.getReviews());
		for(Review review:reviews)
		{			
			//setting the relationship
			course.addReview(review);
			review.setCourse(course);
			em.persist(review);
		}
	}
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/repository/CourseSpringDataRepository.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.rest.core.annotation.RepositoryRestResource;

import com.in28minutes.jpa.hibernate.demo.entity.Course;

@RepositoryRestResource(path="courses")
public interface CourseSpringDataRepository extends JpaRepository<Course, Long> {
	List<Course> findByNameAndId(String name, Long id);

	List<Course> findByName(String name);

	List<Course> countByName(String name);

	List<Course> findByNameOrderByIdDesc(String name);

	List<Course> deleteByName(String name);

	@Query("Select  c  From Course c where name like '%100 Steps'")
	List<Course> courseWith100StepsInName();

	@Query(value = "Select  *  From Course c where name like '%100 Steps'", nativeQuery = true)
	List<Course> courseWith100StepsInNameUsingNativeQuery();

	@Query(name = "query_get_100_Step_courses")
	List<Course> courseWith100StepsInNameUsingNamedQuery();
}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/repository/EmployeeRepository.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import javax.persistence.EntityManager;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.entity.Employee;
import com.in28minutes.jpa.hibernate.demo.entity.FullTimeEmployee;
import com.in28minutes.jpa.hibernate.demo.entity.PartTimeEmployee;

@Repository
@Transactional
public class EmployeeRepository {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	EntityManager em;

	public void insert(Employee employee) {
		em.persist(employee);
	}

	public List<PartTimeEmployee> retrieveAllPartTimeEmployees() {
		return em.createQuery("select e from PartTimeEmployee e", PartTimeEmployee.class).getResultList();
	}

	public List<FullTimeEmployee> retrieveAllFullTimeEmployees() {
		return em.createQuery("select e from FullTimeEmployee e", FullTimeEmployee.class).getResultList();
	}

}
```
---

### /src/main/java/com/in28minutes/jpa/hibernate/demo/repository/StudentRepository.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import javax.persistence.EntityManager;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.entity.Course;
import com.in28minutes.jpa.hibernate.demo.entity.Passport;
import com.in28minutes.jpa.hibernate.demo.entity.Student;

@Repository
@Transactional
public class StudentRepository {

	private Logger logger = LoggerFactory.getLogger(this.getClass());
	
	@Autowired
	EntityManager em;

	public Student findById(Long id) {
		return em.find(Student.class, id);
	}

	public Student save(Student student) {

		if (student.getId() == null) {
			em.persist(student);
		} else {
			em.merge(student);
		}

		return student;
	}

	public void deleteById(Long id) {
		Student student = findById(id);
		em.remove(student);
	}

	public void saveStudentWithPassport() {
		Passport passport = new Passport("Z123456");
		em.persist(passport);

		Student student = new Student("Mike");

		student.setPassport(passport);
		em.persist(student);	
	}
	
	public void someOperationToUnderstandPersistenceContext() {
		//Database Operation 1 - Retrieve student
		Student student = em.find(Student.class, 20001L);
		//Persistence Context (student)
		
		
		//Database Operation 2 - Retrieve passport
		Passport passport = student.getPassport();
		//Persistence Context (student, passport)

		//Database Operation 3 - update passport
		passport.setNumber("E123457");
		//Persistence Context (student, passport++)
		
		//Database Operation 4 - update student
		student.setName("Ranga - updated");
		//Persistence Context (student++ , passport++)
	}
	
	public void insertHardcodedStudentAndCourse(){
		Student student = new Student("Jack");
		Course course = new Course("Microservices in 100 Steps");
		em.persist(student);
		em.persist(course);
		
		student.addCourse(course);
		course.addStudent(student);
		em.persist(student);
	}

	public void insertStudentAndCourse(Student student, Course course){
		//Student student = new Student("Jack");
		//Course course = new Course("Microservices in 100 Steps");
		student.addCourse(course);
		course.addStudent(student);

		em.persist(student);
		em.persist(course);
	}

}
```
---

### /src/main/resources/application.properties

```properties
# Enabling H2 Console
spring.h2.console.enabled=true

#Turn Statistics on
spring.jpa.properties.hibernate.generate_statistics=true
logging.level.org.hibernate.stat=debug

# Show all queries
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
logging.level.org.hibernate.type=trace
spring.jpa.properties.hibernate.connection.isolation=2

# Performance
spring.jpa.properties.hibernate.jdbc.batch_size=10

# Second Level Cache - Ehcache

#1. enable second level cache
spring.jpa.properties.hibernate.cache.use_second_level_cache=true

#2. specify the caching framework - EhCache
spring.jpa.properties.hibernate.cache.region.factory_class=org.hibernate.cache.ehcache.EhCacheRegionFactory

#3. Only cache what I tell to cache.
spring.jpa.properties.javax.persistence.sharedCache.mode=ENABLE_SELECTIVE

logging.level.net.sf.ehcache=debug

#4. What data to cache?
```
---

### /src/main/resources/data.sql

```
insert into course(id, name, created_date, last_updated_date,is_deleted) 
values(10001,'JPA in 50 Steps', sysdate(), sysdate(),false);
insert into course(id, name, created_date, last_updated_date,is_deleted) 
values(10002,'Spring in 50 Steps', sysdate(), sysdate(),false);
insert into course(id, name, created_date, last_updated_date,is_deleted) 
values(10003,'Spring Boot in 100 Steps', sysdate(), sysdate(),false);


insert into passport(id,number)
values(40001,'E123456');
insert into passport(id,number)
values(40002,'N123457');
insert into passport(id,number)
values(40003,'L123890');

insert into student(id,name,passport_id)
values(20001,'Ranga',40001);
insert into student(id,name,passport_id)
values(20002,'Adam',40002);
insert into student(id,name,passport_id)
values(20003,'Jane',40003);

insert into review(id,rating,description,course_id)
values(50001,'FIVE', 'Great Course',10001);
insert into review(id,rating,description,course_id)
values(50002,'FOUR', 'Wonderful Course',10001);
insert into review(id,rating,description,course_id)
values(50003,'FIVE', 'Awesome Course',10003);

insert into student_course(student_id,course_id)
values(20001,10001);
insert into student_course(student_id,course_id)
values(20002,10001);
insert into student_course(student_id,course_id)
values(20003,10001);
insert into student_course(student_id,course_id)
values(20001,10003);
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/DemoApplicationTests.java

```java
package com.in28minutes.jpa.hibernate.demo;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class DemoApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/CourseRepositoryTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertNull;

import java.util.List;

import javax.persistence.EntityGraph;
import javax.persistence.EntityManager;
import javax.persistence.Subgraph;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.annotation.DirtiesContext;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Course;
import com.in28minutes.jpa.hibernate.demo.entity.Review;
import com.in28minutes.jpa.hibernate.demo.entity.Student;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class CourseRepositoryTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	CourseRepository repository;

	@Autowired
	EntityManager em;

	@Test
	public void findById_basic() {
		Course course = repository.findById(10001L);
		assertEquals("JPA in 50 Steps", course.getName());
	}
	
	@Test
	public void findById_firstLevelCacheDemo() {
		
		Course course = repository.findById(10001L);
		logger.info("First Course Retrieved {}", course);

		Course course1 = repository.findById(10001L);
		logger.info("First Course Retrieved again {}", course1);

		assertEquals("JPA in 50 Steps", course.getName());
		
		assertEquals("JPA in 50 Steps", course1.getName());
	}


	@Test
	@DirtiesContext
	public void deleteById_basic() {
		repository.deleteById(10002L);
		assertNull(repository.findById(10002L));
	}

	@Test
	@DirtiesContext
	public void save_basic() {
		// get a course
		Course course = repository.findById(10001L);
		assertEquals("JPA in 50 Steps", course.getName());

		// update details
		course.setName("JPA in 50 Steps - Updated");
		repository.save(course);

		// check the value
		Course course1 = repository.findById(10001L);
		assertEquals("JPA in 50 Steps - Updated", course1.getName());
	}

	@Test
	@DirtiesContext
	public void playWithEntityManager() {
		repository.playWithEntityManager();
	}

	@Test
	@Transactional
	public void retrieveReviewsForCourse() {
		Course course = repository.findById(10001L);
		logger.info("{}", course.getReviews());
	}

	@Test
	@Transactional
	public void retrieveCourseForReview() {
		Review review = em.find(Review.class, 50001L);
		logger.info("{}", review.getCourse());
	}

	@Test
	@Transactional
	@DirtiesContext
	public void performance() {
		//for (int i = 0; i < 20; i++)
			//em.persist(new Course("Something" + i));
		//em.flush();
		
		//EntityGraph graph = em.getEntityGraph("graph.CourseAndStudents");
		
		EntityGraph<Course> graph = em.createEntityGraph(Course.class);
	    Subgraph<List<Student>> bookSubGraph = graph.addSubgraph("students");
	    
	    List<Course> courses = em.createQuery("Select c from Course c", Course.class)
	        .setHint("javax.persistence.loadgraph", graph)
	        .getResultList();
	    for (Course course : courses) {
	      System.out.println(course + " " + course.getStudents());
	    }
	}

	@Test
	@Transactional
	@DirtiesContext
	public void performance_without_hint() {	    
	    List<Course> courses = em.createQuery("Select c from Course c", Course.class)
	        //.setHint("javax.persistence.loadgraph", graph)
	        .getResultList();
	    for (Course course : courses) {
	      System.out.println(course + " " + course.getStudents());
	    }
	}

}
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/CourseSpringDataRepositoryTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;

import java.util.Optional;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Pageable;
import org.springframework.data.domain.Sort;
import org.springframework.test.context.junit4.SpringRunner;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Course;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class CourseSpringDataRepositoryTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	CourseSpringDataRepository repository;

	@Test
	public void findById_CoursePresent() {
		Optional<Course> courseOptional = repository.findById(10001L);
		assertTrue(courseOptional.isPresent());
	}

	@Test
	public void findById_CourseNotPresent() {
		Optional<Course> courseOptional = repository.findById(20001L);
		assertFalse(courseOptional.isPresent());
	}

	@Test
	public void playingAroundWithSpringDataRepository() {
		//Course course = new Course("Microservices in 100 Steps");
		//repository.save(course);

		//course.setName("Microservices in 100 Steps - Updated");
		//repository.save(course);
		logger.info("Courses -> {} ", repository.findAll());
		logger.info("Count -> {} ", repository.count());
	}

	@Test
	public void sort() {
		Sort sort = new Sort(Sort.Direction.ASC, "name");
		logger.info("Sorted Courses -> {} ", repository.findAll(sort));
		//Courses -> [Course[JPA in 50 Steps], Course[Spring in 50 Steps], Course[Spring Boot in 100 Steps]] 
	}

	@Test
	public void pagination() {
		PageRequest pageRequest = PageRequest.of(0, 3);
		Page<Course> firstPage = repository.findAll(pageRequest);
		logger.info("First Page -> {} ", firstPage.getContent());
		
		Pageable secondPageable = firstPage.nextPageable();
		Page<Course> secondPage = repository.findAll(secondPageable);
		logger.info("Second Page -> {} ", secondPage.getContent());
	}
	
	@Test
	public void findUsingName() {
		logger.info("FindByName -> {} ", repository.findByName("JPA in 50 Steps"));
	}

	@Test
	public void findUsingStudentsName() {
		logger.info("findUsingStudentsName -> {} ", repository.findByName("Ranga"));
	}

}
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/CriteriaQueryTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import javax.persistence.EntityManager;
import javax.persistence.TypedQuery;
import javax.persistence.criteria.CriteriaBuilder;
import javax.persistence.criteria.CriteriaQuery;
import javax.persistence.criteria.Join;
import javax.persistence.criteria.JoinType;
import javax.persistence.criteria.Predicate;
import javax.persistence.criteria.Root;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Course;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class CriteriaQueryTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	EntityManager em;

	@Test
	public void all_courses() {
		// "Select c From Course c"

		// 1. Use Criteria Builder to create a Criteria Query returning the
		// expected result object
		CriteriaBuilder cb = em.getCriteriaBuilder();
		CriteriaQuery<Course> cq = cb.createQuery(Course.class);

		// 2. Define roots for tables which are involved in the query
		Root<Course> courseRoot = cq.from(Course.class);

		// 3. Define Predicates etc using Criteria Builder

		// 4. Add Predicates etc to the Criteria Query

		// 5. Build the TypedQuery using the entity manager and criteria query
		TypedQuery<Course> query = em.createQuery(cq.select(courseRoot));

		List<Course> resultList = query.getResultList();

		logger.info("Typed Query -> {}", resultList);
		// [Course[JPA in 50 Steps], Course[Spring in 50 Steps], Course[Spring
		// Boot in 100 Steps]]
	}

	@Test
	public void all_courses_having_100Steps() {
		// "Select c From Course c where name like '%100 Steps' "

		// 1. Use Criteria Builder to create a Criteria Query returning the
		// expected result object
		CriteriaBuilder cb = em.getCriteriaBuilder();
		CriteriaQuery<Course> cq = cb.createQuery(Course.class);

		// 2. Define roots for tables which are involved in the query
		Root<Course> courseRoot = cq.from(Course.class);

		// 3. Define Predicates etc using Criteria Builder
		Predicate like100Steps = cb.like(courseRoot.get("name"), "%100 Steps");

		// 4. Add Predicates etc to the Criteria Query
		cq.where(like100Steps);

		// 5. Build the TypedQuery using the entity manager and criteria query
		TypedQuery<Course> query = em.createQuery(cq.select(courseRoot));

		List<Course> resultList = query.getResultList();

		logger.info("Typed Query -> {}", resultList);
		// [Course[Spring Boot in 100 Steps]]
	}

	@Test
	public void all_courses_without_students() {
		// "Select c From Course c where c.students is empty"

		// 1. Use Criteria Builder to create a Criteria Query returning the
		// expected result object
		CriteriaBuilder cb = em.getCriteriaBuilder();
		CriteriaQuery<Course> cq = cb.createQuery(Course.class);

		// 2. Define roots for tables which are involved in the query
		Root<Course> courseRoot = cq.from(Course.class);

		// 3. Define Predicates etc using Criteria Builder
		Predicate studentsIsEmpty = cb.isEmpty(courseRoot.get("students"));

		// 4. Add Predicates etc to the Criteria Query
		cq.where(studentsIsEmpty);

		// 5. Build the TypedQuery using the entity manager and criteria query
		TypedQuery<Course> query = em.createQuery(cq.select(courseRoot));

		List<Course> resultList = query.getResultList();

		logger.info("Typed Query -> {}", resultList);
		// [Course[Spring in 50 Steps]]
	}

	@Test
	public void join() {
		// "Select c From Course c join c.students s"

		// 1. Use Criteria Builder to create a Criteria Query returning the
		// expected result object
		CriteriaBuilder cb = em.getCriteriaBuilder();
		CriteriaQuery<Course> cq = cb.createQuery(Course.class);

		// 2. Define roots for tables which are involved in the query
		Root<Course> courseRoot = cq.from(Course.class);

		// 3. Define Predicates etc using Criteria Builder
		Join<Object, Object> join = courseRoot.join("students");

		// 4. Add Predicates etc to the Criteria Query

		// 5. Build the TypedQuery using the entity manager and criteria query
		TypedQuery<Course> query = em.createQuery(cq.select(courseRoot));

		List<Course> resultList = query.getResultList();

		logger.info("Typed Query -> {}", resultList);
		// [Course[JPA in 50 Steps], Course[JPA in 50 Steps], Course[JPA in 50
		// Steps], Course[Spring Boot in 100 Steps]]
	}

	@Test
	public void left_join() {
		// "Select c From Course c left join c.students s"

		// 1. Use Criteria Builder to create a Criteria Query returning the
		// expected result object
		CriteriaBuilder cb = em.getCriteriaBuilder();
		CriteriaQuery<Course> cq = cb.createQuery(Course.class);

		// 2. Define roots for tables which are involved in the query
		Root<Course> courseRoot = cq.from(Course.class);

		// 3. Define Predicates etc using Criteria Builder
		Join<Object, Object> join = courseRoot.join("students", JoinType.LEFT);

		// 4. Add Predicates etc to the Criteria Query

		// 5. Build the TypedQuery using the entity manager and criteria query
		TypedQuery<Course> query = em.createQuery(cq.select(courseRoot));

		List<Course> resultList = query.getResultList();

		logger.info("Typed Query -> {}", resultList);
		// [Course[JPA in 50 Steps], Course[JPA in 50 Steps], Course[JPA in 50
		// Steps], Course[Spring in 50 Steps], Course[Spring Boot in 100 Steps]]
	}

}
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/JPQLTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import javax.persistence.EntityManager;
import javax.persistence.Query;
import javax.persistence.TypedQuery;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Course;
import com.in28minutes.jpa.hibernate.demo.entity.Student;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class JPQLTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	EntityManager em;

	@Test
	public void jpql_basic() {
		Query query = em.createNamedQuery("query_get_all_courses");
		List resultList = query.getResultList();
		logger.info("Select  c  From Course c -> {}", resultList);
	}

	@Test
	public void jpql_typed() {
		TypedQuery<Course> query = em.createNamedQuery("query_get_all_courses", Course.class);

		List<Course> resultList = query.getResultList();

		logger.info("Select  c  From Course c -> {}", resultList);
	}

	@Test
	public void jpql_where() {
		TypedQuery<Course> query = em.createNamedQuery("query_get_100_Step_courses", Course.class);

		List<Course> resultList = query.getResultList();

		logger.info("Select  c  From Course c where name like '%100 Steps'-> {}", resultList);
		// [Course[Web Services in 100 Steps], Course[Spring Boot in 100 Steps]]
	}

	@Test
	public void jpql_courses_without_students() {
		TypedQuery<Course> query = em.createQuery("Select c from Course c where c.students is empty", Course.class);
		List<Course> resultList = query.getResultList();
		logger.info("Results -> {}", resultList);
		// [Course[Spring in 50 Steps]]
	}

	
	@Test
	public void jpql_courses_with_atleast_2_students() {
		TypedQuery<Course> query = em.createQuery("Select c from Course c where size(c.students) >= 2", Course.class);
		List<Course> resultList = query.getResultList();
		logger.info("Results -> {}", resultList);
		//[Course[JPA in 50 Steps]]
	}

	@Test
	public void jpql_courses_ordered_by_students() {
		TypedQuery<Course> query = em.createQuery("Select c from Course c order by size(c.students) desc", Course.class);
		List<Course> resultList = query.getResultList();
		logger.info("Results -> {}", resultList);
	}

	@Test
	public void jpql_students_with_passports_in_a_certain_pattern() {
		TypedQuery<Student> query = em.createQuery("Select s from Student s where s.passport.number like '%1234%'", Student.class);
		List<Student> resultList = query.getResultList();
		logger.info("Results -> {}", resultList);
	}

	//like
	//BETWEEN 100 and 1000
	//IS NULL
	//upper, lower, trim, length
	
	//JOIN => Select c, s from Course c JOIN c.students s
	//LEFT JOIN => Select c, s from Course c LEFT JOIN c.students s
	//CROSS JOIN => Select c, s from Course c, Student s
	//3 and 4 =>3 * 4 = 12 Rows
	@Test
	public void join(){
		Query query = em.createQuery("Select c, s from Course c JOIN c.students s");
		List<Object[]> resultList = query.getResultList();
		logger.info("Results Size -> {}", resultList.size());
		for(Object[] result:resultList){
			logger.info("Course{} Student{}", result[0], result[1]);
		}
	}

	@Test
	public void left_join(){
		Query query = em.createQuery("Select c, s from Course c LEFT JOIN c.students s");
		List<Object[]> resultList = query.getResultList();
		logger.info("Results Size -> {}", resultList.size());
		for(Object[] result:resultList){
			logger.info("Course{} Student{}", result[0], result[1]);
		}
	}

	@Test
	public void cross_join(){
		Query query = em.createQuery("Select c, s from Course c, Student s");
		List<Object[]> resultList = query.getResultList();
		logger.info("Results Size -> {}", resultList.size());
		for(Object[] result:resultList){
			logger.info("Course{} Student{}", result[0], result[1]);
		}
	}

}








```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/NativeQueriesTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import javax.persistence.EntityManager;
import javax.persistence.Query;
import javax.persistence.TypedQuery;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Course;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class NativeQueriesTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	EntityManager em;

	@Test
	public void native_queries_basic() {
		Query query = em.createNativeQuery("SELECT * FROM COURSE", Course.class);
		List resultList = query.getResultList();
		logger.info("SELECT * FROM COURSE  -> {}", resultList);
		//SELECT * FROM COURSE  -> [Course[Web Services in 100 Steps], Course[JPA in 50 Steps - Updated], Course[Spring in 50 Steps], Course[Spring Boot in 100 Steps]]
	}

	@Test
	public void native_queries_with_parameter() {
		Query query = em.createNativeQuery("SELECT * FROM COURSE where id = ?", Course.class);
		query.setParameter(1, 10001L);
		List resultList = query.getResultList();
		logger.info("SELECT * FROM COURSE  where id = ? -> {}", resultList);
		//[Course[JPA in 50 Steps - Updated]]
	}

	@Test
	public void native_queries_with_named_parameter() {
		Query query = em.createNativeQuery("SELECT * FROM COURSE where id = :id", Course.class);
		query.setParameter("id", 10001L);
		List resultList = query.getResultList();
		logger.info("SELECT * FROM COURSE  where id = :id -> {}", resultList);
		//[Course[JPA in 50 Steps - Updated]]
	}
	
	@Test
	@Transactional
	public void native_queries_to_update() {
		Query query = em.createNativeQuery("Update COURSE set last_updated_date=sysdate()");
		int noOfRowsUpdated = query.executeUpdate();
		logger.info("noOfRowsUpdated  -> {}", noOfRowsUpdated);
		//SELECT * FROM COURSE  -> [Course[Web Services in 100 Steps], Course[JPA in 50 Steps - Updated], Course[Spring in 50 Steps], Course[Spring Boot in 100 Steps]]
	}


}
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/PerformanceTuningTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import java.util.List;

import javax.persistence.EntityGraph;
import javax.persistence.EntityManager;
import javax.persistence.Subgraph;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Course;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class PerformanceTuningTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	EntityManager em;

	@Test
	@Transactional
	public void creatingNPlusOneProblem() {
		List<Course> courses = em
				.createNamedQuery("query_get_all_courses", Course.class)
				.getResultList();
		for(Course course:courses){
			logger.info("Course -> {} Students -> {}",course, course.getStudents());
		}
	}
	
	@Test
	@Transactional
	public void solvingNPlusOneProblem_EntityGraph() {

		EntityGraph<Course> entityGraph = em.createEntityGraph(Course.class);
		Subgraph<Object> subGraph = entityGraph.addSubgraph("students");
		
		List<Course> courses = em
				.createNamedQuery("query_get_all_courses", Course.class)
				.setHint("javax.persistence.loadgraph", entityGraph)
				.getResultList();
		
		for(Course course:courses){
			logger.info("Course -> {} Students -> {}",course, course.getStudents());
		}
	}

	@Test
	@Transactional
	public void solvingNPlusOneProblem_JoinFetch() {
		List<Course> courses = em
				.createNamedQuery("query_get_all_courses_join_fetch", Course.class)
				.getResultList();
		for(Course course:courses){
			logger.info("Course -> {} Students -> {}",course, course.getStudents());
		}
	}

}
```
---

### /src/test/java/com/in28minutes/jpa/hibernate/demo/repository/StudentRepositoryTest.java

```java
package com.in28minutes.jpa.hibernate.demo.repository;

import javax.persistence.EntityManager;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import com.in28minutes.jpa.hibernate.demo.DemoApplication;
import com.in28minutes.jpa.hibernate.demo.entity.Address;
import com.in28minutes.jpa.hibernate.demo.entity.Passport;
import com.in28minutes.jpa.hibernate.demo.entity.Student;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = DemoApplication.class)
public class StudentRepositoryTest {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	StudentRepository repository;

	@Autowired
	EntityManager em;

	// Session & Session Factory

	// EntityManager & Persistence Context
	// Transaction

	@Test
	public void someTest() {
		repository.someOperationToUnderstandPersistenceContext();
	}

	@Test
	@Transactional
	public void retrieveStudentAndPassportDetails() {
		Student student = em.find(Student.class, 20001L);
		logger.info("student -> {}", student);
		logger.info("passport -> {}", student.getPassport());
	}

	@Test
	@Transactional
	public void setAddressDetails() {
		Student student = em.find(Student.class, 20001L);
		student.setAddress(new Address("No 101", "Some Street", "Hyderabad"));
		em.flush();
	}

	@Test
	@Transactional
	public void retrievePassportAndAssociatedStudent() {
		Passport passport = em.find(Passport.class, 40001L);
		logger.info("passport -> {}", passport);
		logger.info("student -> {}", passport.getStudent());
	}
	
	@Test
	@Transactional
	public void retrieveStudentAndCourses() {
		Student student = em.find(Student.class, 20001L);
		
		logger.info("student -> {}", student);
		logger.info("courses -> {}", student.getCourses());
	}

}
```
---

# Spring Boot Advanced 

## Complete Code Example

### pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.in28minutes.springboot</groupId>
  <artifactId>first-springboot-project</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.4.0.RELEASE</version>
  </parent>

  <properties>
    <java.version>1.8</java.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-security</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-rest</artifactId>
    </dependency>

    <dependency>
      <groupId>com.h2database</groupId>
      <artifactId>h2</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <optional>true</optional>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.data</groupId>
      <artifactId>spring-data-rest-hal-browser</artifactId>
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
</project>
```
### src/main/java/com/in28minutes/springboot/Application.java
```
package com.in28minutes.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Profile;

@SpringBootApplication
public class Application {

  public static void main(String[] args) {
    ApplicationContext ctx = SpringApplication.run(Application.class, args);

  }

  @Profile("prod")
  @Bean
  public String dummy() {
    return "something";
  }
}
```
### src/main/java/com/in28minutes/springboot/configuration/BasicConfiguration.java
```
package com.in28minutes.springboot.configuration;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties("basic")
public class BasicConfiguration {
  private boolean value;
  private String message;
  private int number;

  public boolean isValue() {
    return value;
  }

  public void setValue(boolean value) {
    this.value = value;
  }

  public String getMessage() {
    return message;
  }

  public void setMessage(String message) {
    this.message = message;
  }

  public int getNumber() {
    return number;
  }

  public void setNumber(int number) {
    this.number = number;
  }
}
```
### src/main/java/com/in28minutes/springboot/controller/SurveyController.java
```
package com.in28minutes.springboot.controller;

import java.net.URI;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

import com.in28minutes.springboot.model.Question;
import com.in28minutes.springboot.service.SurveyService;

@RestController
class SurveyController {
  @Autowired
  private SurveyService surveyService;

  @GetMapping("/surveys/{surveyId}/questions")
  public List<Question> retrieveQuestions(@PathVariable String surveyId) {
    return surveyService.retrieveQuestions(surveyId);
  }

  // GET "/surveys/{surveyId}/questions/{questionId}"
  @GetMapping("/surveys/{surveyId}/questions/{questionId}")
  public Question retrieveDetailsForQuestion(@PathVariable String surveyId,
      @PathVariable String questionId) {
    return surveyService.retrieveQuestion(surveyId, questionId);
  }

  // /surveys/{surveyId}/questions
  @PostMapping("/surveys/{surveyId}/questions")
  public ResponseEntity<Void> addQuestionToSurvey(
      @PathVariable String surveyId, @RequestBody Question newQuestion) {

    Question question = surveyService.addQuestion(surveyId, newQuestion);

    if (question == null)
      return ResponseEntity.noContent().build();

    // Success - URI of the new resource in Response Header
    // Status - created
    // URI -> /surveys/{surveyId}/questions/{questionId}
    // question.getQuestionId()
    URI location = ServletUriComponentsBuilder.fromCurrentRequest().path(
        "/{id}").buildAndExpand(question.getId()).toUri();

    // Status
    return ResponseEntity.created(location).build();
  }

}
```
### src/main/java/com/in28minutes/springboot/jpa/User.java
```
package com.in28minutes.springboot.jpa;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {

  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long id;

  private String name;
  private String role;

  protected User() {
  }

  public User(String name, String role) {
    super();
    this.name = name;
    this.role = role;
  }

  public Long getId() {
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
    return "User [id=" + id + ", name=" + name + ", role=" + role + "]";
  }

}
```
### src/main/java/com/in28minutes/springboot/jpa/UserCommandLineRunner.java
```
package com.in28minutes.springboot.jpa;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class UserCommandLineRunner implements CommandLineRunner {

  private static final Logger log = LoggerFactory
      .getLogger(UserCommandLineRunner.class);

  @Autowired
  private UserRepository repository;

  @Override
  public void run(String... args) throws Exception {

    repository.save(new User("Ranga", "Admin"));
    repository.save(new User("Ravi", "User"));
    repository.save(new User("Satish", "Admin"));
    repository.save(new User("Raghu", "User"));

    for (User user : repository.findAll()) {
      log.info(user.toString());
    }

    log.info("Admin users are.....");
    log.info("____________________");
    for (User user : repository.findByRole("Admin")) {
      log.info(user.toString());
    }

  }

}
```
### src/main/java/com/in28minutes/springboot/jpa/UserRepository.java
```
package com.in28minutes.springboot.jpa;

import java.util.List;

import org.springframework.data.repository.CrudRepository;

public interface UserRepository extends CrudRepository<User, Long> {
  List<User> findByRole(String role);
}
```
### src/main/java/com/in28minutes/springboot/jpa/UserRestRepository.java
```
package com.in28minutes.springboot.jpa;

import java.util.List;

import org.springframework.data.repository.PagingAndSortingRepository;
import org.springframework.data.repository.query.Param;
import org.springframework.data.rest.core.annotation.RepositoryRestResource;

@RepositoryRestResource(path = "users", collectionResourceRel = "users")
public interface UserRestRepository extends
    PagingAndSortingRepository<User, Long> {
  List<User> findByRole(@Param("role") String role);
}
```
### src/main/java/com/in28minutes/springboot/model/Question.java
```
package com.in28minutes.springboot.model;

import java.util.List;

public class Question {
  private String id;
  private String description;
  private String correctAnswer;
  private List<String> options;

  // Needed by Caused by: com.fasterxml.jackson.databind.JsonMappingException:
  // Can not construct instance of com.in28minutes.springboot.model.Question:
  // no suitable constructor found, can not deserialize from Object value
  // (missing default constructor or creator, or perhaps need to add/enable
  // type information?)
  public Question() {

  }

  public Question(String id, String description, String correctAnswer,
      List<String> options) {
    super();
    this.id = id;
    this.description = description;
    this.correctAnswer = correctAnswer;
    this.options = options;
  }

  public String getId() {
    return id;
  }

  public void setId(String id) {
    this.id = id;
  }

  public String getDescription() {
    return description;
  }

  public String getCorrectAnswer() {
    return correctAnswer;
  }

  public List<String> getOptions() {
    return options;
  }

  @Override
  public String toString() {
    return String
        .format("Question [id=%s, description=%s, correctAnswer=%s, options=%s]",
            id, description, correctAnswer, options);
  }

  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + ((id == null) ? 0 : id.hashCode());
    return result;
  }

  @Override
  public boolean equals(Object obj) {
    if (this == obj)
      return true;
    if (obj == null)
      return false;
    if (getClass() != obj.getClass())
      return false;
    Question other = (Question) obj;
    if (id == null) {
      if (other.id != null)
        return false;
    } else if (!id.equals(other.id))
      return false;
    return true;
  }

}
```
### src/main/java/com/in28minutes/springboot/model/Survey.java
```
package com.in28minutes.springboot.model;

import java.util.List;

public class Survey {
  private String id;
  private String title;
  private String description;
  private List<Question> questions;

  public Survey(String id, String title, String description,
      List<Question> questions) {
    super();
    this.id = id;
    this.title = title;
    this.description = description;
    this.questions = questions;
  }

  public String getId() {
    return id;
  }

  public void setId(String id) {
    this.id = id;
  }

  public String getTitle() {
    return title;
  }

  public void setTitle(String title) {
    this.title = title;
  }

  public String getDescription() {
    return description;
  }

  public void setDescription(String description) {
    this.description = description;
  }

  public List<Question> getQuestions() {
    return questions;
  }

  public void setQuestions(List<Question> questions) {
    this.questions = questions;
  }

  @Override
  public String toString() {
    return "Survey [id=" + id + ", title=" + title + ", description="
        + description + ", questions=" + questions + "]";
  }

}
```
### src/main/java/com/in28minutes/springboot/security/SecurityConfig.java
```
package com.in28minutes.springboot.security;

import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {
  // Authentication : User --> Roles
  protected void configure(AuthenticationManagerBuilder auth)
      throws Exception {
    auth.inMemoryAuthentication().passwordEncoder(org.springframework.security.crypto.password.NoOpPasswordEncoder.getInstance()).withUser("user1").password("secret1")
        .roles("USER").and().withUser("admin1").password("secret1")
        .roles("USER", "ADMIN");
  }

  // Authorization : Role -> Access
  // survey -> USER
  protected void configure(HttpSecurity http) throws Exception {
    http.httpBasic().and().authorizeRequests().antMatchers("/surveys/**")
        .hasRole("USER").antMatchers("/users/**").hasRole("USER")
        .antMatchers("/**").hasRole("ADMIN").and().csrf().disable()
        .headers().frameOptions().disable();
  }

}
```
### src/main/java/com/in28minutes/springboot/service/SurveyService.java
```
package com.in28minutes.springboot.service;

import java.math.BigInteger;
import java.security.SecureRandom;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

import org.springframework.stereotype.Component;

import com.in28minutes.springboot.model.Question;
import com.in28minutes.springboot.model.Survey;

@Component
public class SurveyService {
  private static List<Survey> surveys = new ArrayList<>();
  static {
    Question question1 = new Question("Question1",
        "Largest Country in the World", "Russia", Arrays.asList(
            "India", "Russia", "United States", "China"));
    Question question2 = new Question("Question2",
        "Most Populus Country in the World", "China", Arrays.asList(
            "India", "Russia", "United States", "China"));
    Question question3 = new Question("Question3",
        "Highest GDP in the World", "United States", Arrays.asList(
            "India", "Russia", "United States", "China"));
    Question question4 = new Question("Question4",
        "Second largest english speaking country", "India", Arrays
            .asList("India", "Russia", "United States", "China"));

    List<Question> questions = new ArrayList<>(Arrays.asList(question1,
        question2, question3, question4));

    Survey survey = new Survey("Survey1", "My Favorite Survey",
        "Description of the Survey", questions);

    surveys.add(survey);
  }

  public List<Survey> retrieveAllSurveys() {
    return surveys;
  }

  public Survey retrieveSurvey(String surveyId) {
    for (Survey survey : surveys) {
      if (survey.getId().equals(surveyId)) {
        return survey;
      }
    }
    return null;
  }

  public List<Question> retrieveQuestions(String surveyId) {
    Survey survey = retrieveSurvey(surveyId);

    if (survey == null) {
      return null;
    }

    return survey.getQuestions();
  }

  public Question retrieveQuestion(String surveyId, String questionId) {
    Survey survey = retrieveSurvey(surveyId);

    if (survey == null) {
      return null;
    }

    for (Question question : survey.getQuestions()) {
      if (question.getId().equals(questionId)) {
        return question;
      }
    }

    return null;
  }

  private SecureRandom random = new SecureRandom();

  public Question addQuestion(String surveyId, Question question) {
    Survey survey = retrieveSurvey(surveyId);

    if (survey == null) {
      return null;
    }

    String randomId = new BigInteger(130, random).toString(32);
    question.setId(randomId);

    survey.getQuestions().add(question);

    return question;
  }
}
```
### src/main/java/com/in28minutes/springboot/WelcomeController.java
```
package com.in28minutes.springboot;

import java.util.HashMap;
import java.util.Map;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.in28minutes.springboot.configuration.BasicConfiguration;

@RestController
public class WelcomeController {

  //Auto wiring
  @Autowired
  private WelcomeService service;

  @Autowired
  private BasicConfiguration configuration;

  @RequestMapping("/welcome")
  public String welcome() {
    return service.retrieveWelcomeMessage();
  }

  @RequestMapping("/dynamic-configuration")
  public Map dynamicConfiguration() {
    Map map = new HashMap();
    map.put("message", configuration.getMessage());
    map.put("number", configuration.getNumber());
    map.put("value", configuration.isValue());

    return map;
  }

}
```
### src/main/java/com/in28minutes/springboot/WelcomeService.java
```
package com.in28minutes.springboot;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

//Spring to manage this bean and create an instance of this
@Component
public class WelcomeService {

  @Value("${welcome.message}")
  private String welcomeMessage;

  public String retrieveWelcomeMessage() {
    //Complex Method
    return welcomeMessage;
  }
}
```
### src/main/resources/application-dev.properties
```
logging.level.org.springframework: TRACE
```
### src/main/resources/application-prod.properties
```
logging.level.org.springframework: INFO
```
### src/main/resources/application.properties
```
logging.level.org.springframework: DEBUG
app.name=in28Minutes
welcome.message=Welcome message from property file! Welcome to ${app.name}

basic.value=true
basic.message=Welcome to in28minutes
basic.number=200
```
### src/test/java/com/in28minutes/springboot/controller/SurveyControllerIT.java
```
package com.in28minutes.springboot.controller;

import static org.junit.Assert.assertTrue;

import java.nio.charset.Charset;
import java.util.Arrays;
import java.util.List;

import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.skyscreamer.jsonassert.JSONAssert;
import org.springframework.boot.context.embedded.LocalServerPort;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.core.ParameterizedTypeReference;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.security.crypto.codec.Base64;
import org.springframework.test.context.junit4.SpringRunner;

import com.in28minutes.springboot.Application;
import com.in28minutes.springboot.model.Question;

@RunWith(SpringRunner.class)
@SpringBootTest(classes = Application.class,
    webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class SurveyControllerIT {

  @LocalServerPort
  private int port;

  TestRestTemplate restTemplate = new TestRestTemplate();

  HttpHeaders headers = new HttpHeaders();

  @Before
  public void before() {
    headers.add("Authorization", createHttpAuthenticationHeaderValue(
        "user1", "secret1"));
    headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
  }

  @Test
  public void testRetrieveSurveyQuestion() {

    HttpEntity<String> entity = new HttpEntity<String>(null, headers);

    ResponseEntity<String> response = restTemplate.exchange(
        createURLWithPort("/surveys/Survey1/questions/Question1"),
        HttpMethod.GET, entity, String.class);

    String expected = "{id:Question1,description:Largest Country in the World,correctAnswer:Russia}";

    JSONAssert.assertEquals(expected, response.getBody(), false);
  }

  @Test
  public void retrieveAllSurveyQuestions() throws Exception {

    ResponseEntity<List<Question>> response = restTemplate.exchange(
        createURLWithPort("/surveys/Survey1/questions"),
        HttpMethod.GET, new HttpEntity<String>("DUMMY_DOESNT_MATTER",
            headers),
        new ParameterizedTypeReference<List<Question>>() {
        });

    Question sampleQuestion = new Question("Question1",
        "Largest Country in the World", "Russia", Arrays.asList(
            "India", "Russia", "United States", "China"));

    assertTrue(response.getBody().contains(sampleQuestion));
  }

  @Test
  public void addQuestion() {

    Question question = new Question("DOESNTMATTER", "Question1", "Russia",
        Arrays.asList("India", "Russia", "United States", "China"));

    HttpEntity entity = new HttpEntity<Question>(question, headers);

    ResponseEntity<String> response = restTemplate.exchange(
        createURLWithPort("/surveys/Survey1/questions"),
        HttpMethod.POST, entity, String.class);

    String actual = response.getHeaders().get(HttpHeaders.LOCATION).get(0);

    assertTrue(actual.contains("/surveys/Survey1/questions/"));

  }

  private String createURLWithPort(final String uri) {
    return "http://localhost:" + port + uri;
  }

  private String createHttpAuthenticationHeaderValue(String userId,
      String password) {

    String auth = userId + ":" + password;

    byte[] encodedAuth = Base64.encode(auth.getBytes(Charset
        .forName("US-ASCII")));

    String headerValue = "Basic " + new String(encodedAuth);

    return headerValue;
  }

}
```
### src/test/java/com/in28minutes/springboot/controller/SurveyControllerTest.java
```
package com.in28minutes.springboot.controller;

import static org.junit.Assert.assertEquals;

import java.util.Arrays;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.Mockito;
import org.skyscreamer.jsonassert.JSONAssert;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.mock.web.MockHttpServletResponse;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.MvcResult;
import org.springframework.test.web.servlet.RequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

import com.in28minutes.springboot.model.Question;
import com.in28minutes.springboot.service.SurveyService;

@RunWith(SpringRunner.class)
@WebMvcTest(value = SurveyController.class, secure = false)
public class SurveyControllerTest {

  @Autowired
  private MockMvc mockMvc;

  // Mock @Autowired
  @MockBean
  private SurveyService surveyService;

  @Test
  public void retrieveDetailsForQuestion() throws Exception {
    Question mockQuestion = new Question("Question1",
        "Largest Country in the World", "Russia", Arrays.asList(
            "India", "Russia", "United States", "China"));

    Mockito.when(
        surveyService.retrieveQuestion(Mockito.anyString(), Mockito
            .anyString())).thenReturn(mockQuestion);

    RequestBuilder requestBuilder = MockMvcRequestBuilders.get(
        "/surveys/Survey1/questions/Question1").accept(
        MediaType.APPLICATION_JSON);

    MvcResult result = mockMvc.perform(requestBuilder).andReturn();

    String expected = "{id:Question1,description:Largest Country in the World,correctAnswer:Russia}";

    JSONAssert.assertEquals(expected, result.getResponse()
        .getContentAsString(), false);

    // Assert
  }

  @Test
  public void createSurveyQuestion() throws Exception {
    Question mockQuestion = new Question("1", "Smallest Number", "1",
        Arrays.asList("1", "2", "3", "4"));

    String questionJson = "{\"description\":\"Smallest Number\",\"correctAnswer\":\"1\",\"options\":[\"1\",\"2\",\"3\",\"4\"]}";
    //surveyService.addQuestion to respond back with mockQuestion
    Mockito.when(
        surveyService.addQuestion(Mockito.anyString(), Mockito
            .any(Question.class))).thenReturn(mockQuestion);

    //Send question as body to /surveys/Survey1/questions
    RequestBuilder requestBuilder = MockMvcRequestBuilders.post(
        "/surveys/Survey1/questions")
        .accept(MediaType.APPLICATION_JSON).content(questionJson)
        .contentType(MediaType.APPLICATION_JSON);

    MvcResult result = mockMvc.perform(requestBuilder).andReturn();

    MockHttpServletResponse response = result.getResponse();

    assertEquals(HttpStatus.CREATED.value(), response.getStatus());

    assertEquals("http://localhost/surveys/Survey1/questions/1", response
        .getHeader(HttpHeaders.LOCATION));
  }
}
```

# Automation Testing With Java and Selenium

## Complete Code Example
---

### /junit-basics/src/test/java/com/example/tests/FacebookLogin.java

```java
package com.example.tests;

import static org.junit.Assert.fail;

import java.util.concurrent.TimeUnit;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.NoAlertPresentException;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import io.github.bonigarcia.wdm.ChromeDriverManager;

public class FacebookLogin {
  private WebDriver driver;
  private String baseUrl;
  private boolean acceptNextAlert = true;
  private StringBuffer verificationErrors = new StringBuffer();

  @Before
  public void setUp() throws Exception {
      ChromeDriverManager.getInstance().setup();

    driver = new ChromeDriver();
    baseUrl = "https://www.katalon.com/";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
  }

  @Test
  public void testFacebookLogin() throws Exception {
    driver.get("https://www.facebook.com/");
    driver.findElement(By.id("email")).click();
    driver.findElement(By.id("email")).clear();
    driver.findElement(By.id("email")).sendKeys("in28minutes");
    driver.findElement(By.id("pass")).clear();
    driver.findElement(By.id("pass")).sendKeys("dummy");
    driver.findElement(By.id("pass")).sendKeys(Keys.ENTER);
  }

  @After
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

  private boolean isElementPresent(By by) {
    try {
      driver.findElement(by);
      return true;
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  private boolean isAlertPresent() {
    try {
      driver.switchTo().alert();
      return true;
    } catch (NoAlertPresentException e) {
      return false;
    }
  }

  private String closeAlertAndGetItsText() {
    try {
      Alert alert = driver.switchTo().alert();
      String alertText = alert.getText();
      if (acceptNextAlert) {
        alert.accept();
      } else {
        alert.dismiss();
      }
      return alertText;
    } finally {
      acceptNextAlert = true;
    }
  }
}
```
---

### /junit-basics/src/test/java/com/example/tests/GoogleSearchForIn28minutes.java

```java
package com.example.tests;

import static org.junit.Assert.fail;

import java.util.concurrent.TimeUnit;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.NoAlertPresentException;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import io.github.bonigarcia.wdm.ChromeDriverManager;

public class GoogleSearchForIn28minutes {
  private WebDriver driver;
  private String baseUrl;
  private boolean acceptNextAlert = true;
  private StringBuffer verificationErrors = new StringBuffer();

  @Before
  public void setUp() throws Exception {
    
      ChromeDriverManager.getInstance().setup();
      driver = new ChromeDriver();

      baseUrl = "https://www.katalon.com/";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
  }

  @Test
  public void testGoogleSearchForIn28minutes() throws Exception {
    driver.get("https://www.google.com/");
    driver.findElement(By.id("lst-ib")).click();
    driver.findElement(By.id("lst-ib")).clear();
    driver.findElement(By.id("lst-ib")).sendKeys("in28minutes");
    driver.findElement(By.id("lst-ib")).sendKeys(Keys.ENTER);
  }

  @After
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

  private boolean isElementPresent(By by) {
    try {
      driver.findElement(by);
      return true;
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  private boolean isAlertPresent() {
    try {
      driver.switchTo().alert();
      return true;
    } catch (NoAlertPresentException e) {
      return false;
    }
  }

  private String closeAlertAndGetItsText() {
    try {
      Alert alert = driver.switchTo().alert();
      String alertText = alert.getText();
      if (acceptNextAlert) {
        alert.accept();
      } else {
        alert.dismiss();
      }
      return alertText;
    } finally {
      acceptNextAlert = true;
    }
  }
}
```
---

### /junit-basics/src/test/java/com/in28minutes/tests/FirstJUnitTest.java

```java
package com.in28minutes.tests;

import static org.junit.Assert.*;

import org.junit.Test;

class SimpleClass {
    public int sum(int[] numbers) {
        int sum = 0;
        
        for(int i=0; i<numbers.length; i++) {
            sum += numbers[i];
        }
        
        return sum;
    }
}

public class FirstJUnitTest {

    @Test
    public void test() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {12, 15, 18});
        
        //Check the Output
        int expectedResult = 45;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

    @Test
    public void testFor0Elements() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {});
        
        //Check the Output
        int expectedResult = 0;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

    @Test
    public void testFor2Elements() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {12, 15});
        
        //Check the Output
        int expectedResult = 27;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

    @Test
    public void testFor5Elements() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {2, 6, 8, 15, 18});
        
        //Check the Output
        int expectedResult = 49;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

}
```
---

### /junit-basics/src/test/java/com/in28minutes/tests/FirstSeleniumJUnitTest.java

```java
package com.in28minutes.tests;

import static org.junit.Assert.assertEquals;

import org.junit.After;
import org.junit.Before;
import org.junit.Ignore;
import org.junit.Test;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import io.github.bonigarcia.wdm.WebDriverManager;

public class FirstSeleniumJUnitTest {

    WebDriver webDriver;

    @Before
    public void before() {
        // Execute the Code

        // Download the Web Driver Executable
        // Set the path to Web Driver Executable
        WebDriverManager.chromedriver().setup();

        // Create an instance of WebDriver

        webDriver = new ChromeDriver();

    }

    @Test
    public void testGoogleDotCom() {

        // WebDriver - Launch up http://www.google.com
        webDriver.get("http://www.google.com");

        // https://www.google.com/?gws_rd=ssl
        // System.out.println(webDriver.getCurrentUrl());

        // System.out.println(webDriver.getTitle());

        String actualTitle = webDriver.getTitle();

        String expectedTitle = "Google";

        // Check the output
        // WebDriver - Title is Google
        assertEquals(expectedTitle, actualTitle);

    }

    @Test
    public void testFacebookDotCom() {

        webDriver.get("http://www.facebook.com");

        String actualTitle = webDriver.getTitle();

        String expectedTitle = "Facebook – log in or sign up";

        // Check the output
        assertEquals(expectedTitle, actualTitle);

    }

    @Test
    @Ignore
    public void testSomeErrorScenarioCom() {

        webDriver.get("com");

        String actualTitle = webDriver.getTitle();

        String expectedTitle = "Facebook – log in or sign up";

        // Check the output
        assertEquals(expectedTitle, actualTitle);

    }

    @After
    public void after() {
        System.out.println("I'm, Executed");
        webDriver.quit();
    }

}

// org.openqa.selenium.WebDriverException:
// unknown error: unhandled inspector error:
// {"code":-32000,"message":"Cannot navigate to invalid URL"}
```
---


### /testng-basics/src/test/java/com/example/tests/FacebookLogin.java

```java
package com.example.tests;

import java.util.regex.Pattern;
import java.util.concurrent.TimeUnit;
import org.testng.annotations.*;

import io.github.bonigarcia.wdm.ChromeDriverManager;

import static org.testng.Assert.*;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.Select;

public class FacebookLogin {
  private WebDriver driver;
  private String baseUrl;
  private boolean acceptNextAlert = true;
  private StringBuffer verificationErrors = new StringBuffer();

  @BeforeClass(alwaysRun = true)
  public void setUp() throws Exception {
        ChromeDriverManager.getInstance().setup();
        driver = new ChromeDriver();
    baseUrl = "https://www.katalon.com/";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
  }

  @Test
  public void testFacebookLogin() throws Exception {
    driver.get("https://www.facebook.com/");
    driver.findElement(By.id("email")).click();
    driver.findElement(By.id("email")).clear();
    driver.findElement(By.id("email")).sendKeys("in28minutes");
    driver.findElement(By.id("pass")).clear();
    driver.findElement(By.id("pass")).sendKeys("dummy");
    driver.findElement(By.id("pass")).sendKeys(Keys.ENTER);
  }

  @AfterClass(alwaysRun = true)
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

  private boolean isElementPresent(By by) {
    try {
      driver.findElement(by);
      return true;
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  private boolean isAlertPresent() {
    try {
      driver.switchTo().alert();
      return true;
    } catch (NoAlertPresentException e) {
      return false;
    }
  }

  private String closeAlertAndGetItsText() {
    try {
      Alert alert = driver.switchTo().alert();
      String alertText = alert.getText();
      if (acceptNextAlert) {
        alert.accept();
      } else {
        alert.dismiss();
      }
      return alertText;
    } finally {
      acceptNextAlert = true;
    }
  }
}
```
---

### /testng-basics/src/test/java/com/example/tests/GoogleSearchForIn28minutes.java

```java
package com.example.tests;

import static org.testng.Assert.fail;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.NoAlertPresentException;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.ChromeDriverManager;

public class GoogleSearchForIn28minutes {
  private WebDriver driver;
  private String baseUrl;
  private boolean acceptNextAlert = true;
  private StringBuffer verificationErrors = new StringBuffer();

  @BeforeClass(alwaysRun = true)
  public void setUp() throws Exception {
    ChromeDriverManager.getInstance().setup();
    driver = new ChromeDriver();
    baseUrl = "https://www.katalon.com/";
    driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
  }

  @Test
  public void testGoogleSearchForIn28minutes() throws Exception {
    driver.get("https://www.google.com/");
    driver.findElement(By.id("lst-ib")).click();
    driver.findElement(By.id("lst-ib")).clear();
    driver.findElement(By.id("lst-ib")).sendKeys("in28minutes");
    driver.findElement(By.id("lst-ib")).sendKeys(Keys.ENTER);
  }

  @AfterClass(alwaysRun = true)
  public void tearDown() throws Exception {
    driver.quit();
    String verificationErrorString = verificationErrors.toString();
    if (!"".equals(verificationErrorString)) {
      fail(verificationErrorString);
    }
  }

  private boolean isElementPresent(By by) {
    try {
      driver.findElement(by);
      return true;
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  private boolean isAlertPresent() {
    try {
      driver.switchTo().alert();
      return true;
    } catch (NoAlertPresentException e) {
      return false;
    }
  }

  private String closeAlertAndGetItsText() {
    try {
      Alert alert = driver.switchTo().alert();
      String alertText = alert.getText();
      if (acceptNextAlert) {
        alert.accept();
      } else {
        alert.dismiss();
      }
      return alertText;
    } finally {
      acceptNextAlert = true;
    }
  }
}
```
---

### /testng-basics/src/test/java/com/in28minutes/test/testng/FirstSeleniumTestNgTest.java

```java
package com.in28minutes.test.testng;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Ignore;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class FirstSeleniumTestNgTest {

    WebDriver webDriver;

    @BeforeTest
    public void before() {
        // Execute the Code

        // Download the Web Driver Executable
        // Set the path to Web Driver Executable
        WebDriverManager.chromedriver().setup();

        // Create an instance of WebDriver

        webDriver = new ChromeDriver();

    }

    @Test
    public void testGoogleDotCom() {

        // WebDriver - Launch up http://www.google.com
        webDriver.get("http://www.google.com");

        // https://www.google.com/?gws_rd=ssl
        // System.out.println(webDriver.getCurrentUrl());

        // System.out.println(webDriver.getTitle());

        String actualTitle = webDriver.getTitle();

        String expectedTitle = "Google";

        // Check the output
        // WebDriver - Title is Google
        assertEquals(expectedTitle, actualTitle);

    }

    @Test
    public void testFacebookDotCom() {

        webDriver.get("http://www.facebook.com");

        String actualTitle = webDriver.getTitle();

        String expectedTitle = "Facebook – log in or sign up";

        // Check the output
        assertEquals(expectedTitle, actualTitle);

    }

    @Test
    @Ignore
    public void testSomeErrorScenarioCom() {

        webDriver.get("com");

        String actualTitle = webDriver.getTitle();

        String expectedTitle = "Facebook – log in or sign up";

        // Check the output
        assertEquals(expectedTitle, actualTitle);

    }

    @AfterTest
    public void after() {
        System.out.println("I'm, Executed");
        webDriver.quit();
    }

}

// org.openqa.selenium.WebDriverException:
// unknown error: unhandled inspector error:
// {"code":-32000,"message":"Cannot navigate to invalid URL"}
```
---

### /testng-basics/src/test/java/com/in28minutes/test/testng/FirstTestngTest.java

```java
package com.in28minutes.test.testng;

import static org.testng.Assert.assertEquals;

import org.testng.annotations.Test;

class SimpleClass {
    public int sum(int[] numbers) {
        int sum = 0;
        
        for(int i=0; i<numbers.length; i++) {
            sum += numbers[i];
        }
        
        return sum;
    }
}

public class FirstTestngTest {

    @Test
    public void test() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {12, 15, 18});
        
        //Check the Output
        int expectedResult = 45;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

    @Test
    public void testFor0Elements() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {});
        
        //Check the Output
        int expectedResult = 0;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

    @Test
    public void testFor2Elements() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {12, 15});
        
        //Check the Output
        int expectedResult = 27;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

    @Test
    public void testFor5Elements() {
        
        //Execute the Code
        SimpleClass simpleClass = new SimpleClass();
        
        int actualResult = simpleClass.sum( new int[] {2, 6, 8, 15, 18});
        
        //Check the Output
        int expectedResult = 49;
        
        //check expectedResult is equal to actualResult
        assertEquals(expectedResult, actualResult);
        
        
        //No checks
        //Checks
        //Absence of Failure is Success
    }

}
```
---

### /testng-basics/src/test/java/com/in28minutes/test/testng/MultipleBrowserTest.java

```java
package com.in28minutes.test.testng;

import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class MultipleBrowserTest {
  
    @Parameters("browser")
    @Test
    public void runInBrowser(String browser) {
        System.out.println(browser);
    }
}
```

---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/AbstractChromeWebDriverTest.java

```java
package com.in28minutes.webdriver.basics;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;

import io.github.bonigarcia.wdm.WebDriverManager;

public abstract class AbstractChromeWebDriverTest {

    protected WebDriver driver;

    public AbstractChromeWebDriverTest() {
        super();
    }

    @BeforeTest
    public void beforeTest() {
        //Download the web driver executable
        WebDriverManager.chromedriver().setup();
        
        //Create a instance of your web driver - chrome
        driver = new ChromeDriver();
    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
    
    public void sleep(int seconds) {
        try {
            Thread.sleep(seconds * 1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/form/FormElementCheckBoxTest.java

```java
package com.in28minutes.webdriver.basics.form;

import static org.testng.Assert.assertEquals;
import static org.testng.Assert.assertFalse;
import static org.testng.Assert.assertTrue;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class FormElementCheckBoxTest extends AbstractChromeWebDriverTest {

    @Test
    public void readFromACheckBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement checkboxElement1 = driver.findElement(By.name("checkboxElement1"));
        System.out.println(checkboxElement1.isSelected());//false
        assertFalse(checkboxElement1.isSelected());
        
        WebElement checkboxElement2 = driver.findElement(By.name("checkboxElement2"));
        System.out.println(checkboxElement2.isSelected());//true
        assertTrue(checkboxElement2.isSelected());
    }
    
    @Test
    public void setAValueIntoCheckBoxElement1() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement checkboxElement1 = driver.findElement(By.name("checkboxElement1"));
        sleep(4);
        checkboxElement1.click();
        sleep(4);
        WebElement checkboxElement3 = driver.findElement(By.name("checkboxElement3"));
        sleep(4);
        checkboxElement3.click();
        sleep(4);
    }

    @Test
    public void checkACheckBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        
        checkACheckBox("checkboxElement1");
        sleep(2);
        checkACheckBox("checkboxElement2");
        sleep(2);
        checkACheckBox("checkboxElement3");
        
        checkACheckBox("inlineCheckboxElement1");
        checkACheckBox("inlineCheckboxElement2");
        checkACheckBox("inlineCheckboxElement3");
        sleep(4);

    }

    @Test
    public void unCheckACheckBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        
        unCheckACheckBox("checkboxElement1");
        sleep(2);
        unCheckACheckBox("checkboxElement2");
        sleep(2);
        unCheckACheckBox("checkboxElement3");

        unCheckACheckBox("inlineCheckboxElement1");
        unCheckACheckBox("inlineCheckboxElement2");
        unCheckACheckBox("inlineCheckboxElement3");
        
        sleep(4);

    }

    private void checkACheckBox(String checkboxName) {
        WebElement checkboxElement1 = driver.findElement(By.name(checkboxName));
        
        boolean currentValue = checkboxElement1.isSelected();
        
        if(currentValue==false) {
            checkboxElement1.click();
        }
    }
    
    private void unCheckACheckBox(String checkboxName) {
        WebElement checkboxElement1 = driver.findElement(By.name(checkboxName));
        
        boolean currentValue = checkboxElement1.isSelected();
        
        if(currentValue==true) {
            checkboxElement1.click();
        }
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/form/FormElementRadioButtonTest.java

```java
package com.in28minutes.webdriver.basics.form;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class FormElementRadioButtonTest extends AbstractChromeWebDriverTest {

    @Test
    public void readFromARadioButton() {
        driver.get("http://localhost:8080/pages/forms.html");
        List<WebElement> options = driver.findElements(By.name("optionsRadios"));
        for (WebElement option : options) {
            System.out.println(option.getAttribute("value") + " " + option.isSelected());
        }
        // option1 false
        // option2 false
        // option3 true

    }

    @Test
    public void readFromARadioButtonWithAFrameworkMethod() {
        driver.get("http://localhost:8080/pages/forms.html");
        System.out.println(getSelectedRadioButtonValue("optionsRadios"));// option3
        System.out.println(getSelectedRadioButtonValue("optionsRadiosInline"));

    }

    @Test
    public void setValueForRadioButton() {
        driver.get("http://localhost:8080/pages/forms.html");
        List<WebElement> options = driver.findElements(By.name("optionsRadios"));
        sleep(4);
        for (WebElement option : options) {
            if (option.getAttribute("value").equals("option2")) {
                option.click();
            }
        }
        sleep(4);
    }

    @Test
    public void setValueForRadioButtonWithAFrameworkMethod() {
        driver.get("http://localhost:8080/pages/forms.html");
        sleep(4);
        setRadioButtonToValue("optionsRadios", "option2");
        sleep(4);
        setRadioButtonToValue("optionsRadiosInline", "inline-option1");
    }

    private void setRadioButtonToValue(String radioButtonName, String valueToSelect) {
        List<WebElement> options = driver.findElements(By.name(radioButtonName));
        for (WebElement option : options) {
            if (option.getAttribute("value").equals(valueToSelect)) {
                option.click();
            }
        }
    }

    private String getSelectedRadioButtonValue(String name) {

        List<WebElement> options = driver.findElements(By.name(name));

        for (WebElement option : options) {
            if (option.isSelected()) {
                return option.getAttribute("value");
            }
        }

        return null;
    }

    @Test
    public void setValueForRadioButtonWithAFrameworkMethod_UsingCSS() {
        driver.get("http://localhost:8080/pages/forms.html");
        sleep(4);
        setRadioButtonToValueUsingCSS("optionsRadios", "option2");
        sleep(4);
        setRadioButtonToValueUsingCSS("optionsRadiosInline", "inline-option1");
        sleep(4);
    }

    private void setRadioButtonToValueUsingCSS(String radioButtonName, String valueToSelect) {
        String cssSelector = "input[name='" + radioButtonName + "'][value='" + valueToSelect + "']";

        WebElement option = driver.findElement(By.cssSelector(cssSelector));
        option.click();
    }

    @Test
    public void setValueForRadioButtonWithAFrameworkMethod_UsingXPath() {
        driver.get("http://localhost:8080/pages/forms.html");
        sleep(4);
        setRadioButtonToValueUsingXPath("optionsRadios", "option2");
        sleep(4);
        setRadioButtonToValueUsingXPath("optionsRadiosInline", "inline-option1");
        sleep(4);
    }

    private void setRadioButtonToValueUsingXPath(String radioButtonName, String valueToSelect) {
        String cssSelector = "//input[@name='" + radioButtonName + "'][@value='" + valueToSelect + "']";

        WebElement option = driver.findElement(By.xpath(cssSelector));
        option.click();
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/form/FormElementSelectTest.java

```java
package com.in28minutes.webdriver.basics.form;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.Select;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class FormElementSelectTest extends AbstractChromeWebDriverTest {

    @Test
    public void readValueOfSelectBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement selectElement = driver.findElement(By.id("selectElement1"));
        Select select = new Select(selectElement);
        System.out.println(select.isMultiple());
        System.out.println(select.getFirstSelectedOption().getText());
    }
    
    @Test
    public void readValueFromMultiSelectBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement selectElement = driver.findElement(By.id("multiSelectElement"));
        Select select = new Select(selectElement);
        System.out.println(select.isMultiple());//true
        System.out.println(select.getFirstSelectedOption().getText());//One
        for (WebElement element : select.getAllSelectedOptions()) {
            System.out.println(element.getText());//One,Three
        }
    }
    
    @Test
    public void setValuesIntoSelectBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement selectElement = driver.findElement(By.id("selectElement1"));
        sleep(5);
        Select select = new Select(selectElement);
        select.selectByValue("2");
        sleep(5);
        select.selectByVisibleText("Five");
        sleep(5);
        select.selectByIndex(3);
        sleep(5);
        System.out.println(select.isMultiple());
        System.out.println(select.getFirstSelectedOption().getText());
    }

    @Test
    public void setValuesIntoMultiSelectBox() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement selectElement = driver.findElement(By.id("multiSelectElement"));
        sleep(5);
        Select select = new Select(selectElement);
        select.deselectAll();
        sleep(3);
        select.selectByValue("2");
        sleep(3);
        select.selectByVisibleText("Five");
        sleep(3);
        select.selectByIndex(3);
        sleep(3);
        select.deselectByVisibleText("Four");
        sleep(3);
        System.out.println(select.isMultiple());
        System.out.println(select.getFirstSelectedOption().getText());
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/form/FormElementTextTest.java

```java
package com.in28minutes.webdriver.basics.form;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class FormElementTextTest extends AbstractChromeWebDriverTest {

    @Test
    public void readFromATextElement() {
        driver.get("http://localhost:8080/pages/forms.html");
        assertEquals(
                driver.findElement(By.id("textElement")).getAttribute("value"), 
                "in28minutes");
    }
    
    @Test
    public void setASpecificValueIntoTextElement() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement textElement = driver.findElement(By.id("textElement"));
        sleep(4);
        textElement.clear();
        textElement.sendKeys("NewValue");
        sleep(4);
    }

    @Test
    public void writeAndReadAValueFromTextArea() {
        driver.get("http://localhost:8080/pages/forms.html");
        
        WebElement textArea = driver.findElement(By.id("textAreaElement"));
        
        assertEquals(textArea.getAttribute("value"),"");
        sleep(4);
        textArea.clear();
        textArea.sendKeys("FirstLine");
        textArea.sendKeys("\n");
        textArea.sendKeys("SecondLine");
        sleep(4);
        System.out.println(textArea.getAttribute("value"));
        assertEquals(textArea.getAttribute("value"),"FirstLine\nSecondLine");
        
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsPerformanceTest.java

```java
package com.in28minutes.webdriver.basics;

import static org.testng.Assert.assertEquals;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsPerformanceTest extends AbstractChromeWebDriverTest{
    
    @Test
    public void testCssSelectorForMultipleTableTd() {   
        driver.get("http://localhost:8080/pages/tables.html");
        WebElement browserRow1 = driver.findElement(
                By.cssSelector("#dataTables-example > tbody > tr:nth-child(1) > td:nth-child(2)"));
        WebElement browserRow2 = driver.findElement(
                By.cssSelector("#dataTables-example > tbody > tr:nth-child(2) > td:nth-child(2)"));
        WebElement browserRow3 = driver.findElement(
                By.cssSelector("#dataTables-example > tbody > tr:nth-child(3) > td:nth-child(2)"));
        assertEquals(browserRow1.getText(), "Firefox 1.0");     
        assertEquals(browserRow2.getText(), "Firefox 1.5");     
        assertEquals(browserRow3.getText(), "Firefox 2.0");     
    }
    
    @Test
    public void testCssSelectorForMultipleTableTd_MorePerformance() {   
        driver.get("http://localhost:8080/pages/tables.html");
        
        WebElement tableTbody = driver.findElement(
                By.cssSelector("#dataTables-example > tbody"));
        
        WebElement browserRow1 = 
                tableTbody.findElement(By.cssSelector("tr:nth-child(1) > td:nth-child(2)"));

        WebElement browserRow2 = 
                tableTbody.findElement(By.cssSelector("tr:nth-child(2) > td:nth-child(2)"));

        WebElement browserRow3 = 
                tableTbody.findElement(By.cssSelector("tr:nth-child(3) > td:nth-child(2)"));

        assertEquals(browserRow1.getText(), "Firefox 1.0");     
        assertEquals(browserRow2.getText(), "Firefox 1.5");     
        assertEquals(browserRow3.getText(), "Firefox 2.0");     
    }   

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithClassTest.java

```java
package com.in28minutes.webdriver.basics;

import static org.testng.Assert.assertEquals;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsWithClassTest extends AbstractChromeWebDriverTest{
    
    @Test
    public void testTitle() {   
        driver.get("http://localhost:8080/pages/index.html");
        WebElement title = driver.findElement(By.className("navbar-brand"));
        assertEquals(title.getText(), "SB Admin v2.0");     
    }
    
    //huge
    @Test
    public void testHugeTextElements() {    
        driver.get("http://localhost:8080/pages/index.html");
        List<WebElement> hugeElements = driver.findElements(By.className("huge"));
        for(WebElement element: hugeElements) {
            System.out.println(element.getText());
        }

    }
    
}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithCSSSelectorTest.java

```java
package com.in28minutes.webdriver.basics;

import static org.testng.Assert.assertEquals;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsWithCSSSelectorTest extends AbstractChromeWebDriverTest {

    @Test
    public void testCssSelectorForaTableTd() {
        driver.get("http://localhost:8080/pages/tables.html");

        WebElement browserRow1 = driver
                .findElement(By.cssSelector("#dataTables-example > tbody > tr:nth-child(1) > td:nth-child(2)"));
        assertEquals(browserRow1.getText(), "Firefox 1.0");
        
    }

    // $$("#dataTables-example > thead > tr > th:nth-child(2)")
    // [th.sorting]0: th.sortinglength: 1__proto__: Array(0)
    // $$("#dataTables-example > tbody > tr.gradeU.odd > td.sorting_1")
    // [td.sorting_1]

    @Test
    public void testCssSelectorForSortingAndCheckingFirstRow() {
        driver.get("http://localhost:8080/pages/tables.html");

        /*
         * <tr class="gradeA odd" role="row"> <td class="sorting_1">Gecko</td>
         * <td>Firefox 1.0</td> <td>Win 98+ / OSX.2+</td> <td class="center">1.7</td>
         * <td class="center">A</td> </tr>
         * 
         * 
         * <tr class="gradeU odd" role="row"> <td class="">Other browsers</td> <td
         * class="sorting_1">All others</td> <td>-</td> <td class="center">-</td> <td
         * class="center">U</td> </tr>
         */

        // #dataTables-example > tbody > tr:nth-child(1) > td:nth-child(2)
        // #dataTables-example > tbody > tr.gradeU.odd > td.sorting_1

        WebElement headerBrowser = driver
                .findElement(By.cssSelector("#dataTables-example > thead > tr > th:nth-child(2)"));

        headerBrowser.click();

        WebElement element = driver
                .findElement(By.cssSelector("#dataTables-example > tbody > tr.gradeU.odd > td.sorting_1"));

        assertEquals(element.getText(), "All others");
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithIdTest.java

```java
package com.in28minutes.webdriver.basics;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class WebDriverBasicsLocatorsWithIdTest extends AbstractChromeWebDriverTest{
    
    @Test
    public void testTitle() {
    
        //get the http://localhost:8080/login
        driver.get("http://localhost:8080/login");
        
        //assert the title
        assertEquals("First Web Application",
                driver.getTitle());//First Web Application
        
    }
    
    @Test
    public void testGetInformationAboutName() {
        driver.get("http://localhost:8080/login");
        WebElement nameElement = driver.findElement(By.id("name"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("type"));//text
        System.out.println(nameElement.getAttribute("value"));//EMPTY
    }

    @Test
    public void testGetInformationAboutPassword() {
        driver.get("http://localhost:8080/login");
        WebElement nameElement = driver.findElement(By.id("password"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("type"));//password
        System.out.println(nameElement.getAttribute("value"));//EMPTY
    }
    
    @Test
    public void testGetInformationAboutSubmitButton() {
        driver.get("http://localhost:8080/login");
        WebElement nameElement = driver.findElement(By.id("submit"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("type"));//submit
        System.out.println(nameElement.getAttribute("value"));//EMPTY
    }

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithLinkTextTest.java

```java
package com.in28minutes.webdriver.basics;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsWithLinkTextTest extends AbstractChromeWebDriverTest {
  
  @Test
  public void getIn28MinuteLinkAndClickIt() {
      driver.get("http://localhost:8080/login");
      WebElement link = driver.findElement(By.linkText("in28Minutes"));
      System.out.println(link.getAttribute("href"));//http://www.in28minutes.com/
      link.click();
      System.out.println(driver.getCurrentUrl());// http://www.in28minutes.com/
  }
  
  @Test
  public void getTableLinkAndClickIt() {
      driver.get("http://localhost:8080/pages/index.html");
      WebElement link = driver.findElement(By.linkText("Tables"));
      System.out.println(link.getAttribute("href"));
      link.click();
      System.out.println(driver.getCurrentUrl());
  }

  @Test
  public void getSBAdminLinkAndClickIt() {
      driver.get("http://localhost:8080/pages/index.html");
      WebElement link = driver.findElement(By.partialLinkText("SB Admin"));
      System.out.println(link.getAttribute("href"));
      link.click();
      System.out.println(driver.getCurrentUrl());
  }

  
}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithNameTest.java

```java
package com.in28minutes.webdriver.basics;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Ignore;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsWithNameTest extends AbstractChromeWebDriverTest {
    
    @Test
    public void testGetInformationAboutEmail() {
        driver.get("http://localhost:8080/pages/login.html");
        WebElement nameElement = driver.findElement(By.name("email"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("class"));//form-control
        System.out.println(nameElement.getAttribute("placeholder"));//E-mail
        System.out.println(nameElement.getAttribute("value"));//EMPTY
    }

    @Test
    public void testGetInformationAboutPassword() {
        driver.get("http://localhost:8080/pages/login.html");
        WebElement nameElement = driver.findElement(By.name("password"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("class"));//form-control
        System.out.println(nameElement.getAttribute("placeholder"));//Password
        System.out.println(nameElement.getAttribute("value"));//EMPTY
    }


    @Test
    public void testGetInformationAboutCheckbox() {
        driver.get("http://localhost:8080/pages/login.html");
        WebElement nameElement = driver.findElement(By.name("remember"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("class"));//
        System.out.println(nameElement.getAttribute("value"));//Remember Me
        System.out.println(nameElement.getAttribute("type"));//checkbox
    }
    
    @Test
    @Ignore
    public void testGetInformationAboutSubmitButton() {
        driver.get("http://localhost:8080/pages/login.html");
        WebElement nameElement = driver.findElement(By.id("submit"));
        System.out.println(nameElement.getTagName());//input
        System.out.println(nameElement.getAttribute("type"));//submit
        System.out.println(nameElement.getAttribute("value"));//EMPTY
    }

    //FAILED: testGetInformationAboutSubmitButton
    //org.openqa.selenium.NoSuchElementException: 
    //no such element: Unable to locate element: 
    //{"method":"id","selector":"submit"}

}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithTagTest.java

```java
package com.in28minutes.webdriver.basics;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsWithTagTest extends AbstractChromeWebDriverTest {
  
  @Test
  public void getDetailsAboutLoginButton() {
      driver.get("http://localhost:8080/pages/login.html");
      WebElement linkElement = driver.findElement(By.tagName("a"));
      System.out.println(linkElement.getText());//Login
      System.out.println(linkElement.getAttribute("class"));//btn btn-lg btn-success btn-block
      System.out.println(linkElement.getAttribute("href"));//http://localhost:8080/pages/index.html
  }
  
  @Test
  public void getDetailsAboutInputTags_FindElementWillReturnFirstElement() {
      driver.get("http://localhost:8080/pages/login.html");
      WebElement linkElement = driver.findElement(By.tagName("input"));
      System.out.println(linkElement.getAttribute("class"));//form-control
      System.out.println(linkElement.getAttribute("placeholder"));//E-mail
  }
  
  @Test
  public void getDetailsAboutInputTags_FindAllElements() {
      driver.get("http://localhost:8080/pages/login.html");
      
      List<WebElement> elements = driver.findElements(By.tagName("input"));
      
      for(WebElement element:elements) {
          System.out.println(element.getAttribute("class"));
          System.out.println(element.getAttribute("placeholder"));
      }
  }
  
  @Test
  public void getDetailsAboutInputTags_FindAllElements_Login() {
      driver.get("http://localhost:8080/login");
      
      List<WebElement> elements = driver.findElements(By.tagName("input"));
      
      for(WebElement element:elements) {
          System.out.println(element.getAttribute("type"));
          System.out.println(element.getAttribute("name"));
          sleep(3);
      }
  }
}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/basics/WebDriverBasicsLocatorsWithXPathSelectorTest.java

```java
package com.in28minutes.webdriver.basics;

import static org.testng.Assert.assertEquals;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

public class WebDriverBasicsLocatorsWithXPathSelectorTest extends AbstractChromeWebDriverTest{
    
    @Test
    public void testXpathSelectorForaTableTd() {
        driver.get("http://localhost:8080/pages/tables.html");
        //$x("//*[@id='dataTables-example']/tbody/tr[1]/td[2]")
        WebElement browserRow1 = driver.findElement(By.xpath("//*[@id='dataTables-example']/tbody/tr[1]/td[2]"));
        assertEquals(browserRow1.getText(), "Firefox 1.0");     
    }
    
//  $$("#dataTables-example > thead > tr > th:nth-child(2)")
//  [th.sorting]0: th.sortinglength: 1__proto__: Array(0)
//  $$("#dataTables-example > tbody > tr.gradeU.odd > td.sorting_1")
//  [td.sorting_1]
    
    @Test
    public void testXpathSelectorForSortingAndCheckingFirstRow() {
        
//      $x("//*[@id='dataTables-example']/thead/tr/th[2]")
//      [th.sorting]0: th.sortinglength: 1__proto__: Array(0)
//      $x("//*[@id='dataTables-example']/tbody/tr[1]/td[2]")
//      [td]
                
        driver.get("http://localhost:8080/pages/tables.html");
        
        WebElement headerBrowser = driver.findElement
                (By.xpath(
                "//*[@id='dataTables-example']/thead/tr/th[2]"));
        
        headerBrowser.click();

        WebElement element = driver.findElement
                (By.xpath(
                "//*[@id='dataTables-example']/tbody/tr[1]/td[2]"));

        assertEquals(element.getText(), "All others");      
    }
    
    
}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/login/FirstWebApplicationLoginTest.java

```java
package com.in28minutes.webdriver.login;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class FirstWebApplicationLoginTest extends AbstractChromeWebDriverTest{
  
  @Test
  public void login() {
      driver.get("http://localhost:8080/login");
      
      sleep(5);
      
      WebElement nameElement = driver.findElement(By.name("name"));
      nameElement.sendKeys("in28minutes");
      
      sleep(2);
      
      WebElement passwordElement = driver.findElement(By.id("password"));
      passwordElement.sendKeys("dummy");
      
      sleep(2);
      
      WebElement submitElement = driver.findElement(By.id("submit"));
      submitElement.click();
      
      sleep(2);
      
      WebElement welcomeMessageElement = 
              driver.findElement(By.id("welcome-message"));
      
      
      
      //Welcome in28minutes!! Click here to manage your todo's.
      System.out.println(welcomeMessageElement.getText());
      
  }
}
```
---

### /web-driver-1-basics/src/test/java/com/in28minutes/webdriver/login/StaticLoginTest.java

```java
package com.in28minutes.webdriver.login;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class StaticLoginTest extends AbstractChromeWebDriverTest{
  
  @Test
  public void login() {
      driver.get("http://localhost:8080/pages/login.html");
      
      sleep(5);
      
      WebElement emailElement = driver.findElement(By.name("email"));
      emailElement.sendKeys("in28minutes@gmail.com");
      
      sleep(2);
      
      WebElement passwordElement = driver.findElement(By.name("password"));
      passwordElement.sendKeys("dummy");
      
      sleep(2);
      
      WebElement loginElement = driver.findElement(By.tagName("a"));
      loginElement.click();
      
      sleep(2);
      
      //http://localhost:8080/pages/index.html
      System.out.println(driver.getCurrentUrl());
      
  }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/basics/AbstractChromeWebDriverTest.java

```java
package com.in28minutes.webdriver.basics;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;

import io.github.bonigarcia.wdm.WebDriverManager;

public abstract class AbstractChromeWebDriverTest {

  protected WebDriver driver;

  public AbstractChromeWebDriverTest() {
    super();
  }

  @BeforeTest
  public void beforeTest() {
    //Download the web driver executable
    WebDriverManager.chromedriver().setup();
    
    //Create a instance of your web driver - chrome
    driver = new ChromeDriver();
  }

  @AfterTest
  public void afterTest() {
    driver.quit();
  }
  
  public void sleep(int seconds) {
    try {
      Thread.sleep(seconds * 1000);
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
  }

}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/ActionsBasicTest.java

```java
package com.in28minutes.webdriver.scenarios;

import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.interactions.Actions;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class ActionsBasicTest extends AbstractChromeWebDriverTest {

    @Test
    public void testBasicActions() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement element = driver.findElement(By.id("textElement"));
        WebElement tablesLink = driver.findElement(By.linkText("Tables"));
        
        //element.sendKeys("abc");
        //tablesLink.click();
        
        Actions actions = new Actions(driver);
        actions.sendKeys(element, "Dummy Text").perform();
        sleep(5);
        actions.click(tablesLink).perform();
        sleep(5);
        
        
    }
    
    @Test
    public void testBasicActions_Combine() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement element = driver.findElement(By.id("textElement"));
        WebElement tablesLink = driver.findElement(By.linkText("Tables"));
        
        Actions actions = new Actions(driver);
        actions
            .sendKeys(element, "Dummy Text")
            .click(tablesLink)
            .perform();
        sleep(5);
    }

    @Test
    public void testBasicDragAndDrop() {
        driver.get("http://localhost:8080/pages/sortable.html");
        WebElement htmlElement = driver.findElement(By.id("html"));
        Actions actions = new Actions(driver);
        actions
            .dragAndDropBy(htmlElement, 50, 200)
            .perform();
        
        sleep(5);
    }


    @Test
    public void testBasicDragAndDrop_Complicated() {
        driver.get("http://localhost:8080/pages/sortable.html");
        WebElement htmlElement = driver.findElement(By.id("html"));
        
        Actions actions = new Actions(driver);
        actions
            .clickAndHold(htmlElement)
            .moveByOffset(50, 200)
            .release()
            .perform();
        
        sleep(5);
    }

}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/CheckElementStylesTest.java

```java
package com.in28minutes.webdriver.scenarios;

import static org.testng.Assert.assertFalse;

import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class CheckElementStylesTest extends AbstractChromeWebDriverTest {

    @Test
    public void getCSSStylesForErrorElement() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement errorField = driver.findElement(By.id("inputError"));

        System.out.println(errorField.getCssValue("color"));// rgba(85, 85, 85, 1)
        System.out.println(errorField.getCssValue("display"));// block
        System.out.println(errorField.getCssValue("border-color"));// rgb(169, 68, 66)
        System.out.println(errorField.getCssValue("height"));// 34px
        System.out.println(errorField.getCssValue("font-size"));// 14px
        System.out.println(errorField.getCssValue("background-color"));// rgba(255, 255, 255, 1)
        System.out.println(errorField.getCssValue("border"));// 1px solid rgb(169, 68, 66)

    }

    @Test
    public void getCSSStylesForSuccessElement() {
        driver.get("http://localhost:8080/pages/forms.html");
        WebElement errorField = driver.findElement(By.id("inputSuccess"));
        System.out.println(errorField.getCssValue("color"));// rgba(85, 85, 85, 1)
        System.out.println(errorField.getCssValue("display"));// block
        System.out.println(errorField.getCssValue("border-color"));// rgb(60, 118, 61)
        System.out.println(errorField.getCssValue("height"));// 34px
        System.out.println(errorField.getCssValue("font-size"));// 14px
        System.out.println(errorField.getCssValue("background-color"));// rgba(255, 255, 255, 1)
        System.out.println(errorField.getCssValue("border"));// 1px solid rgb(60, 118, 61)
    }

    @Test
    public void checkIfAnElementIsEnabled() {
        driver.get("http://localhost:8080/pages/forms.html");
        
        WebElement errorField = driver.findElement(By.id("disabledInput"));
        
        assertFalse(errorField.isEnabled());
        System.out.println(errorField.isEnabled());//false
        
    }
    
    @Test
    public void exploreWebElementInterface() {
        driver.get("http://localhost:8080/pages/forms.html");
        
        WebElement errorField = driver.findElement(By.id("disabledInput"));
        System.out.println(errorField.getAttribute("placeholder"));//Disabled input
        
        System.out.println(errorField.getLocation());//(740, 311)
        System.out.println(errorField.getSize());//(414, 34)
        
        WebElement textElement = driver.findElement(By.id("textElement"));      
        System.out.println(textElement.getLocation());//(297, 242)
        System.out.println(textElement.getSize());//(414, 34)

        WebElement textAreaElement = driver.findElement(By.id("textAreaElement"));      
        System.out.println(textAreaElement.getLocation());//(297, 549)
        System.out.println(textAreaElement.getSize());//(414, 74)

        WebElement inputWarning = driver.findElement(By.id("inputWarning"));        
        System.out.println(inputWarning.getLocation());//(740, 666)
        System.out.println(inputWarning.getSize());//(414, 34)

        //findElements, findElement

    }

}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/FramesTest.java

```java
package com.in28minutes.webdriver.scenarios;

import org.openqa.selenium.By;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class FramesTest extends AbstractChromeWebDriverTest {

    @Test
    public void testFrames() {
        driver.get("http://localhost:8080/pages/frames-example.html");
        
        driver.switchTo().frame(0);
        
        System.out.println(  
                "0 - " + driver.findElement(By.tagName("h1")).getText()
                );//0 - Frames Example Left
        
        //org.openqa.selenium.NoSuchFrameException: no such frame
        //driver.switchTo().frame(1);
        
        driver.switchTo().parentFrame();
        
        driver.switchTo().frame(1);
        
        System.out.println(  
                "1 - " + driver.findElement(By.tagName("h1")).getText()
                );//1 - Frames Example Right

        
    }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/framework/TableReader.java

```java
package com.in28minutes.webdriver.scenarios.framework;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

public class TableReader {
    private WebDriver driver;
    private String id;
    private WebElement tbody;

    public TableReader(WebDriver driver, String id) {
        this.driver = driver;
        this.id = id;
        tbody = driver.findElement(By.cssSelector("#"
                + id
                + " > tbody"));
    }

    public String getData(int row, int col) {
        return tbody.findElement(By.cssSelector("tr:nth-child("
                + row
                + ") > td:nth-child("
                + col
                + ")")).getText();
    }

}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/JavaScriptAlertTest.java

```java
package com.in28minutes.webdriver.scenarios;

import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class JavaScriptAlertTest extends AbstractChromeWebDriverTest {

    @Test
    public void testForAlert() {
        driver.get("http://localhost:8080/pages/notifications.html");
        driver.findElement(By.id("alertButton")).click();

        //org.openqa.selenium.UnhandledAlertException: 
        //unexpected alert open: {Alert text : Enter Something}
        //driver.findElement(By.id("modalButton")).click();
        
        Alert alertQuestion = driver.switchTo().alert();
        alertQuestion.sendKeys("Some Message");
        alertQuestion.accept();
        
        Alert alertMessage = driver.switchTo().alert();
        System.out.println(alertMessage.getText());
        alertMessage.accept();      
    }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/NewWindowTest.java

```java
package com.in28minutes.webdriver.scenarios;

import org.openqa.selenium.By;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class NewWindowTest extends AbstractChromeWebDriverTest {

    @Test
    public void testForWindows() {

        driver.get("http://localhost:8080/pages/notifications.html");

        // 0 - [CDwindow-C62544C6B928D4C97EE4F2E54D9B7FE2]
        System.out.println("0 - " + driver.getWindowHandles());

        driver.findElement(By.id("newPageButton")).click();
        // Window Handle
        // 1 - CDwindow-C62544C6B928D4C97EE4F2E54D9B7FE2
        System.out.println("1 - " + driver.getWindowHandle());

        // 2 - [CDwindow-C62544C6B928D4C97EE4F2E54D9B7FE2,
        // CDwindow-F3E3A57A563CF50F3A063A72C4B23768]
        System.out.println("2 - " + driver.getWindowHandles());

    }

    @Test
    public void findWindowHandleOfSecondWindow() {

        driver.get("http://localhost:8080/pages/notifications.html");

        String firstWindowHandle = driver.getWindowHandle();

        System.out.println(firstWindowHandle);

        driver.findElement(By.id("newPageButton")).click();

        String secondWindowHandle = findSecondWindowHandle(firstWindowHandle);

        System.out.println(secondWindowHandle);
    }

    private String findSecondWindowHandle(String firstWindowHandle) {
        for (String handle : driver.getWindowHandles()) {
            if (!firstWindowHandle.equals(handle)) {
                return handle;
            }
        }
        return null;
    }

    @Test
    public void switchToSecondWindow() {

        driver.get("http://localhost:8080/pages/notifications.html");

        String firstWindowHandle = driver.getWindowHandle();

        System.out.println(firstWindowHandle);

        driver.findElement(By.id("newPageButton")).click();

        String secondWindowHandle = findSecondWindowHandle(firstWindowHandle);

        System.out.println(secondWindowHandle);

        System.out.println(driver.findElement(By.tagName("h1")).getText());// Notifications

        driver.switchTo().window(secondWindowHandle);

        System.out.println(driver.findElement(By.tagName("h1")).getText());// Forms

        driver.switchTo().window(firstWindowHandle);

        System.out.println(driver.findElement(By.tagName("h1")).getText());// Notifications

        System.out.println(driver.getCurrentUrl());// http://localhost:8080/pages/notifications.html

        driver.close();

        // org.openqa.selenium.NoSuchWindowException: no such window: target window
        // already closed
        // System.out.println(driver.getCurrentUrl());

        driver.switchTo().window(secondWindowHandle);

        System.out.println(driver.getCurrentUrl());// http://localhost:8080/pages/forms.html
    }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/PlayingWithModalWindowAndWaitsTest.java

```java
package com.in28minutes.webdriver.scenarios;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.ElementNotVisibleException;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.annotations.Ignore;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

import io.github.bonigarcia.wdm.WebDriverManager;

public class PlayingWithModalWindowAndWaitsTest extends AbstractChromeWebDriverTest {

    @Test(expectedExceptions = ElementNotVisibleException.class)
    public void playingWithModalWindows_expectingAException() {
        driver.get("http://localhost:8080/pages/notifications.html");
        // Button id - modalButton
        // Modal Wdw id - myModal, myModalLabel, myModalBody, myModalCloseButton
        driver.findElement(By.id("modalButton")).click();

        // org.openqa.selenium.ElementNotVisibleException: element not visible
        driver.findElement(By.id("myModalCloseButton")).click();

    }

    @Test
    public void playingWithModalWindows_FixingWithSleep() {

        driver.get("http://localhost:8080/pages/notifications.html");

        // Button id - modalButton
        // Modal Wdw id - myModal, myModalLabel, myModalBody, myModalCloseButton
        driver.findElement(By.id("modalButton")).click();

        sleep(1);

        System.out.println(driver.findElement(By.id("myModalLabel")).getText());// Modal title

        driver.findElement(By.id("myModalCloseButton")).click();

        // sleep(10);
    }

    @Test
    @Ignore("implicit wait fails on Chrome")
    // https://github.com/SeleniumHQ/selenium-google-code-issue-archive/issues/711
    public void playingWithModalWindows_implicitWait() {

        driver.manage().timeouts().implicitlyWait(1, TimeUnit.SECONDS);

        driver.get("http://localhost:8080/pages/notifications.html");

        // Button id - modalButton
        // Modal Wdw id - myModal, myModalLabel, myModalBody, myModalCloseButton
        driver.findElement(By.id("modalButton")).click();

        // sleep(1);

        System.out.println(driver.findElement(By.id("myModalLabel")).getText());// Modal title

        driver.findElement(By.id("myModalCloseButton")).click();

        // sleep(10);
    }

    @Test
    public void playingWithModalWindows_ExplicitWait() {

        driver.get("http://localhost:8080/pages/notifications.html");

        // Button id - modalButton
        // Modal Wdw id - myModal, myModalLabel, myModalBody, myModalCloseButton
        driver.findElement(By.id("modalButton")).click();

        // sleep(10);
        // Max - 10
        // Wait for myModalLabel to load

        WebDriverWait webDriverWait = new WebDriverWait(driver, 10);
        
        webDriverWait.withMessage("Waited for 10 Seconds but still myModalLabel not available");
        
        WebElement modalLabel = 
                webDriverWait.until(
                        ExpectedConditions.visibilityOf(
                                driver.findElement(By.id("myModalLabel"))
                                )
                        );// By.id("myModalLabel")


        System.out.println(modalLabel.getText());// Modal title

        driver.findElement(By.id("myModalCloseButton")).click();

        // sleep(10);
    }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/PlayingWithScreenWindowTest.java

```java
package com.in28minutes.webdriver.scenarios;

import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.Point;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class PlayingWithScreenWindowTest extends AbstractChromeWebDriverTest {
    
    @Test
    public void playingWithWindows() {
        driver.get("http://localhost:8080/pages/forms.html");
        
        System.out.println(driver.manage().window().getPosition());//(22, 22)
        System.out.println(driver.manage().window().getSize());//(1200, 752)
        sleep(3);
        //failed to change window state to normal, current state is maximized
        driver.manage().window().setPosition(new Point(200,200));
        sleep(3);
        driver.manage().window().setSize(new Dimension(200,200));
        sleep(3);
        driver.manage().window().maximize();
        sleep(3);
        driver.manage().window().fullscreen();
        sleep(3);

    }
    
    @Test
    public void backForwardAndNavigation() {
        driver.get("http://localhost:8080/pages/forms.html");
        sleep(3);
        driver.get("http://localhost:8080/pages/tables.html");
        sleep(3);
        driver.get("http://localhost:8080/pages/login.html");
        sleep(3);
        driver.get("http://localhost:8080/pages/index.html");
        sleep(3);
        driver.navigate().back();
        sleep(3);
        driver.navigate().back();
        sleep(3);
        driver.navigate().back();
        sleep(3);
        driver.navigate().forward();
        sleep(3);
        driver.navigate().refresh();
        sleep(3);
        driver.navigate().back();
        sleep(3);
    }   
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/ReadTablesTest.java

```java
package com.in28minutes.webdriver.scenarios;

import java.io.IOException;

import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebElement;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;
import com.in28minutes.webdriver.scenarios.framework.TableReader;

public class ReadTablesTest extends AbstractChromeWebDriverTest {

    @Test
    public void testReadingOfTables() throws IOException {
        
        driver.get("http://localhost:8080/pages/tables.html");
        
        TableReader reader = new TableReader(driver, "dataTables-example");
        System.out.println(reader.getData(1,2));
        System.out.println(reader.getData(2,2));
        System.out.println(reader.getData(5,4));
        System.out.println(reader.getData(6,3));

        TableReader reader2 = new TableReader(driver, "dataTables-example-2");
        System.out.println(reader2.getData(1, 2));
        
        //1,2
        //2,3
        //WebElement tbody = driver.findElement(By.cssSelector("#dataTables-example > tbody"));
        
        //String t12 = tbody.findElement(By.cssSelector("tr:nth-child(1) > td:nth-child(2)")).getText();
        
        //String t22 = tbody.findElement(By.cssSelector("tr:nth-child(2) > td:nth-child(2)")).getText();
        
        //System.out.println(t12);
        //System.out.println(t22);
        
        //#dataTables-example > tbody > tr:nth-child(1) > td:nth-child(2)
        //#dataTables-example > tbody > tr:nth-child(2) > td:nth-child(2)
        //#dataTables-example > tbody > tr:nth-child(1) > td:nth-child(3)
        
    }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/RunJavaScriptTest.java

```java
package com.in28minutes.webdriver.scenarios;

import java.io.IOException;

import org.openqa.selenium.JavascriptExecutor;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class RunJavaScriptTest extends AbstractChromeWebDriverTest {

    @Test
    public void testRunningOfJavaScript() throws IOException {
        
        driver.get("http://localhost:8080/pages/tables.html");
        
        JavascriptExecutor js = (JavascriptExecutor)driver;
        
        String title = (String)js.executeScript("return document.title;");
        
        sleep(3);
        
        js.executeScript("window.scrollBy(0,200)");
        
        sleep(3);
        
        js.executeScript("window.scrollBy(0,200)");
        
        sleep(3);
        
        js.executeScript("window.scrollBy(0,200)");

        sleep(3);
        System.out.println(title);
        
    }
}
```
---

### /web-driver-2-more-scenarios/src/test/java/com/in28minutes/webdriver/scenarios/TakesScreenshotTest.java

```java
package com.in28minutes.webdriver.scenarios;

import java.io.File;
import java.io.IOException;

import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.testng.annotations.Test;

import com.in28minutes.webdriver.basics.AbstractChromeWebDriverTest;

public class TakesScreenshotTest extends AbstractChromeWebDriverTest {

    @Test
    public void testFrames() throws IOException {
        
        driver.get("http://localhost:8080/pages/frames-example.html");
        
        //Operations
        
        File screenshot = ((TakesScreenshot)driver)
                .getScreenshotAs(OutputType.FILE);

        FileUtils.copyFile(screenshot,
                new File("./target/" + driver + "-screenshot.png"));
    }
}
```
---

### /web-driver-3-cross-browser-framework/src/test/java/com/in28minutes/selenium/crossbrowser/CrossBrowserBasicsTest.java

```java
package com.in28minutes.selenium.crossbrowser;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.ie.InternetExplorerDriver;
import org.openqa.selenium.safari.SafariDriver;
import org.testng.annotations.Ignore;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class CrossBrowserBasicsTest {
    @Test
    public void chromeBrowser() {
        // Chrome

        // Chrome Web Driver EXE
        WebDriverManager.chromedriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new ChromeDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }
    
    @Test
    public void firefoxBrowser() {
        // Firefox

        // Firefox Web Driver EXE
        WebDriverManager.firefoxdriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new FirefoxDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }

    @Test
    public void safariBrowser() {
        // Safari
        // Make sure you set Develop | Allow Remote Automation option from Safari's main
        // menu
        
        // Could not create a session: You must enable the 'Allow Remote Automation'
        // option in Safari's Develop menu to control Safari via WebDriver.

        // Safari Web Driver EXE
        //WebDriverManager.safaridriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new SafariDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }
    
    @Test
    @Ignore
    public void ieBrowser() {
        
        WebDriverManager.iedriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new InternetExplorerDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }


    @Test
    @Ignore
    public void edgeBrowser() {
        
        WebDriverManager.edgedriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new EdgeDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }

    private void sleep(int i) {
        
        try {
            Thread.sleep(i * 1000);
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }

    }
}
```
---

### /web-driver-3-cross-browser-framework/src/test/java/com/in28minutes/selenium/crossbrowser/framework/CrossBrowserFrameworkTest.java

```java
package com.in28minutes.selenium.crossbrowser.framework;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Optional;
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class CrossBrowserFrameworkTest {
    
    WebDriver driver = null;
    
    @Parameters("browser")
    @BeforeTest
    public void before(@Optional("chrome") String browser) {
        if(browser.equals("chrome")) {
            WebDriverManager.chromedriver().setup();
            driver = new ChromeDriver();
        } else if(browser.equals("firefox")){
            WebDriverManager.firefoxdriver().setup();
            driver = new FirefoxDriver();
        } else {
            throw new RuntimeException("Does not support browser + " + browser);
        }       
    }
        
    @Test
    public void launchTablesPage() {
        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

    }
    
    @Test
    public void launchIndexPage() {
        // Launch a web page
        driver.get("http://localhost:8080/pages/index.html");

    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```
---

### /web-driver-3-cross-browser-framework/src/test/java/com/in28minutes/selenium/crossbrowser/HeadlessBrowserBasicsTest.java

```java
package com.in28minutes.selenium.crossbrowser;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.firefox.FirefoxOptions;
import org.openqa.selenium.phantomjs.PhantomJSDriver;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class HeadlessBrowserBasicsTest {

    @Test
    public void chromeBrowser() {
        // Chrome

        // Chrome Web Driver EXE
        WebDriverManager.chromedriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new ChromeDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }

    @Test
    public void chromeBrowserHeadlessBrowsing() {
        // Chrome

        // Chrome Web Driver EXE
        WebDriverManager.chromedriver().setup();

        ChromeOptions options = new ChromeOptions();
        options.setHeadless(true);
        
        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new ChromeDriver(options);

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }

    @Test
    public void firefoxBrowser() {
        // Firefox

        // Firefox Web Driver EXE
        WebDriverManager.firefoxdriver().setup();

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new FirefoxDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }
    

    @Test
    public void firefoxBrowserHeadlessBrowsing() {
        // Firefox

        // Firefox Web Driver EXE
        WebDriverManager.firefoxdriver().setup();
        
        FirefoxOptions options = new FirefoxOptions();
        options.setHeadless(true);

        // WebDriver Interface - Create an instance of the web driver of the browser
        WebDriver driver = new FirefoxDriver(options);

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }

    @Test
    public void phanthomJS() {
        WebDriverManager.phantomjs().setup();

        WebDriver driver = new PhantomJSDriver();

        // Launch a web page
        driver.get("http://localhost:8080/pages/tables.html");

        sleep(5);

        driver.quit();
    }
    


    private void sleep(int i) {
        
        try {
            Thread.sleep(i * 1000);
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }

    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/ExcelReadUtil.java

```java
package com.in28minutes.datadriventests;
import java.io.File;

import org.apache.poi.openxml4j.opc.OPCPackage;
import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Workbook;
import org.apache.poi.ss.usermodel.WorkbookFactory;

public class ExcelReadUtil {
  public static String[][] readExcelInto2DArray(String excelFilePath, 
          String sheetName, int totalCols) {

    File file = new File(excelFilePath);

    String[][] tabArray = null;

    try {
      OPCPackage opcPackage = OPCPackage.open(file.getAbsolutePath());

      Workbook wb = WorkbookFactory.create(opcPackage);

      Sheet sheet = wb.getSheet(sheetName);

      int totalRows = sheet.getLastRowNum() + 1;

      tabArray = new String[totalRows][totalCols];

      for (int i = 0; i < totalRows; i++) {
        for (int j = 0; j < totalCols; j++) {
          
            Cell cell = sheet.getRow(i).getCell(j);
          //System.out.println(cell + " " + i + " " + j);

          if (cell == null)
            continue;

          switch (cell.getCellType()) {
          case Cell.CELL_TYPE_BOOLEAN:
            tabArray[i][j] = String.valueOf(cell.getBooleanCellValue());
            break;
          case Cell.CELL_TYPE_NUMERIC:
            tabArray[i][j] = String.valueOf(cell.getNumericCellValue());
            break;
          case Cell.CELL_TYPE_STRING:
            tabArray[i][j] = cell.getStringCellValue();
            break;
          default:
            tabArray[i][j] = "";
            break;
          }
        }
      }
    } catch (Exception e) {
      e.printStackTrace();
      throw new RuntimeException(e);
    }

    return tabArray;
  }

}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/LoginDataProviderCompleteCsvTest.java

```java
package com.in28minutes.datadriventests;

import static org.testng.Assert.assertEquals;
import static org.testng.Assert.assertTrue;

import java.io.FileReader;
import java.io.IOException;
import java.util.Arrays;
import java.util.Iterator;
import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import com.opencsv.CSVReader;

import io.github.bonigarcia.wdm.WebDriverManager;

public class LoginDataProviderCompleteCsvTest {
    
    //Data Provider public java.util.List com.in28minutes.datadriventests.
    //LoginDataProviderCompleteCsvTest.userIdsAndPasswordsCSVDataProvider() 
    //must return either Object[][] or Object[] or Iterator<Object[]> 
    //or Iterator<Object>, not interface java.util.List

    // Create the Data Provider and give the data provider a name
    @DataProvider(name = "user-ids-passwords-csv-data-provider")
    public Iterator<String[]> userIdsAndPasswordsCSVDataProvider() {
        return readFromCSVFile("./src/test/resources/login-data.csv").iterator();
    }

    // Use the data provider
    @Test(dataProvider = "user-ids-passwords-csv-data-provider")
    public void testLoginForAllScenarios(String userId, String password, String isLoginExpectedToBeSuccessfulString) {
        
        boolean isLoginExpectedToBeSuccessful = Boolean.valueOf(isLoginExpectedToBeSuccessfulString);
        
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys(userId);
        // driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys(password);
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        if (isLoginExpectedToBeSuccessful) {
            String welcomeMessageText = driver.findElement(By.id("welcome-message")).getText();
            assertTrue(welcomeMessageText.contains("Welcome " + userId));
        } else {
            String errorMessageText = driver.findElement(By.id("error-message")).getText();
            assertEquals(errorMessageText, "Invalid Credentials");
        }

        driver.quit();
    }

    @Test
    public void testReadingDataFromCSV() throws IOException {
        List<String[]> data = readFromCSVFile("./src/test/resources/login-data.csv");
        for (String[] row : data) {
            System.out.println(Arrays.toString(row));
        }

    }

    private List<String[]> readFromCSVFile(String csvFilePath) {
        try {
            CSVReader reader = new CSVReader(new FileReader(csvFilePath));
            List<String[]> data = reader.readAll();
            return data;
        } catch (Exception e) {
            e.printStackTrace();
            throw new RuntimeException(e);
        }
    }

}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/LoginDataProviderCompleteExcelTest.java

```java
package com.in28minutes.datadriventests;

import static org.testng.Assert.assertEquals;
import static org.testng.Assert.assertTrue;

import java.util.Arrays;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class LoginDataProviderCompleteExcelTest {
        
    //Create the Data Provider and give the data provider a name
    @DataProvider(name="user-ids-passwords-excel-data-provider")
    public String[][] userIdsAndPasswordsDataProvider() {
        return ExcelReadUtil.readExcelInto2DArray(
                "./src/test/resources/login-data.xlsx", "Sheet1", 3);
    }   
    
    //Use the data provider
    @Test(dataProvider="user-ids-passwords-excel-data-provider")
    public void testLoginForAllScenarios(String userId, 
            String password, String isLoginExpectedToBeSuccessfulString) {
        
        boolean isLoginExpectedToBeSuccessful = 
                Boolean.valueOf(isLoginExpectedToBeSuccessfulString);
        
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys(userId);
        //driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys(password);
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        if(isLoginExpectedToBeSuccessful) {
            String welcomeMessageText = driver.findElement(By.id("welcome-message")).getText();
            assertTrue(welcomeMessageText.contains("Welcome " + userId));
        } else {
            String errorMessageText = driver.findElement(By.id("error-message")).getText();
            assertEquals(errorMessageText,"Invalid Credentials");           
        }
        
        driver.quit();
    }
    
    @Test
    public void readFromExcel() {
        //[[in28minutes, dummy, true], [adam, adam, false], 
        //[adam, adam@123, true], [eve, eve, false]]
        String[][] data = ExcelReadUtil.readExcelInto2DArray(
                "./src/test/resources/login-data.xlsx", "Sheet1", 3);
        System.out.println(Arrays.deepToString(data));
        
    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/LoginDataProviderCompleteTest.java

```java
package com.in28minutes.datadriventests;

import static org.testng.Assert.assertEquals;
import static org.testng.Assert.assertTrue;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class LoginDataProviderCompleteTest {
        
    //Create the Data Provider and give the data provider a name
    @DataProvider(name="user-ids-passwords-data-provider")
    public Object[][] userIdsAndPasswordsDataProvider() {
        return new Object[][]{
                {"in28minutes","dummy", true},
                {"adam","adam", false},
                {"adam","adam@123", true},
                {"eve","eve",false},
                {"eve","eve@123", true},
            };
    }   
    
    //Use the data provider
    @Test(dataProvider="user-ids-passwords-data-provider")
    public void testLoginForAllScenarios(String userId, 
            String password, boolean isLoginExpectedToBeSuccessful) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys(userId);
        //driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys(password);
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        if(isLoginExpectedToBeSuccessful) {
            String welcomeMessageText = driver.findElement(By.id("welcome-message")).getText();
            assertTrue(welcomeMessageText.contains("Welcome " + userId));
        } else {
            String errorMessageText = driver.findElement(By.id("error-message")).getText();
            assertEquals(errorMessageText,"Invalid Credentials");           
        }
        
        driver.quit();
    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/SuccessfulLoginBasicTest.java

```java
package com.in28minutes.datadriventests;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class SuccessfulLoginBasicTest {

    @Test
    public void testLoginWithIn28Minutes() {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys("dummy");
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        // welcome-message
        System.out.println(driver.findElement(By.id("welcome-message")).getText());
        driver.quit();
    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/UnSuccessfulLoginBasicTest.java

```java
package com.in28minutes.datadriventests;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UnSuccessfulLoginBasicTest {

    @Test
    public void testUnsuccessfulLoginWithIn28Minutes() {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys("");
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        // welcome-message
        String errorMessageText = driver.findElement(By.id("error-message")).getText();
        System.out.println(errorMessageText);
        assertEquals(errorMessageText,"Invalid Credentials");
        driver.quit();
    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/UnSuccessfulLoginDataDrivenBasicTest.java

```java
package com.in28minutes.datadriventests;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UnSuccessfulLoginDataDrivenBasicTest {
        
    //Create the Data Provider and give the data provider a name
    @DataProvider(name="user-ids-data-provider")
    public String[] userIdsDataProvider() {
        return new String[]{"in28minutes","adam","eve"};
    }   
    
    //Use the data provider
    @Test(dataProvider="user-ids-data-provider")
    public void testUnsuccessfulLoginWithIn28Minutes(String userId) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys(userId);
        //driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys("");
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        // welcome-message
        String errorMessageText = driver.findElement(By.id("error-message")).getText();
        System.out.println(errorMessageText);
        assertEquals(errorMessageText,"Invalid Credentials");
        driver.quit();
    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/java/com/in28minutes/datadriventests/UnSuccessfulLoginDataDrivenLevel1Test.java

```java
package com.in28minutes.datadriventests;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UnSuccessfulLoginDataDrivenLevel1Test {
        
    //Create the Data Provider and give the data provider a name
    @DataProvider(name="user-ids-passwords-data-provider")
    public String[][] userIdsAndPasswordsDataProvider() {
        return new String[][]{
                {"in28minutes","in28minutes"},
                {"adam","adam"},
                {"eve","eve"},
            };
    }   
    
    //Use the data provider
    @Test(dataProvider="user-ids-passwords-data-provider")
    public void testUnsuccessfulLoginWithIn28Minutes(String userId, String password) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/login");
        driver.findElement(By.id("name")).sendKeys(userId);
        //driver.findElement(By.id("name")).sendKeys("in28minutes");
        WebElement passwordElement = driver.findElement(By.id("password"));
        passwordElement.sendKeys(password);
        passwordElement.submit();
        // driver.findElement(By.id("submit")).click();

        // welcome-message
        String errorMessageText = driver.findElement(By.id("error-message")).getText();
        System.out.println(errorMessageText);
        assertEquals(errorMessageText,"Invalid Credentials");
        driver.quit();
    }
}
```
---

### /web-driver-4-data-driven-tests/src/test/resources/login-data.csv

```
in28minutes,dummy,true
adam,adam,false
adam,adam@123,true
eve,eve,false
eve,eve@123,true
in28minutes,eve@123,false
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/ListTodoPage.java

```java
package com.in28minutes.pageobjects.updatetodo;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class ListTodoPage {
    
    private WebDriver driver;
    
    public ListTodoPage(WebDriver driver) {
        super();
        this.driver = driver;
    }

    //get description for id
    //desc- + id
    public String getDescription(String id) {
        return driver.findElement(By.id("desc-" + id)).getText();
    }
    
    //get target date for id
    public String getTargetDate(String id) {
        return driver.findElement(By.id("targetdate-" + id)).getText();
    }
    
    //click update for a id
    public void clickUpdateFor(String id) {
        driver.findElement(By.id("update-" + id)).click();
    }
    
    //delete a id

}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/LoginPage.java

```java
package com.in28minutes.pageobjects.updatetodo;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.FindBy;

public class LoginPage {
    
    private WebDriver driver;
    
    public LoginPage(WebDriver driver) {
        super();
        driver.get("http://localhost:8080/login");
        this.driver = driver;
    }

    //Name Text Box
    @FindBy(id="name")
    WebElement name;
    
    //Password Text Box
    @FindBy(id="password")
    WebElement password;
    
    //Submit Button
    @FindBy(id="submit")
    WebElement submitButton;
    
    //enterName
    public void enterName(String nameToEnter) {
        name.sendKeys(nameToEnter);
    }

    //enterPassword
    public void enterPassword(String passwordToEnter) {
        password.sendKeys(passwordToEnter);
    }

    //submit
    public void submit() {
        submitButton.submit();
    }
    
    public void login(String name, String password) {
        enterName(name);
        enterPassword(password);
        submit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/TodoPage.java

```java
package com.in28minutes.pageobjects.updatetodo;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.FindBy;

public class TodoPage {

    private WebDriver driver;
    
    public TodoPage(WebDriver driver) {
        super();
        this.driver = driver;
    }
    
    @FindBy(id="desc")
    private WebElement description;
    
    @FindBy(id="targetDate")
    private WebElement targetDate;
    
    @FindBy(id="save")
    private WebElement saveButton;
    
    public void enterDescription(String desc) {
        description.clear();
        description.sendKeys(desc);
    }
    
    public void enterTargetDate(String date) {
        targetDate.clear();
        targetDate.sendKeys(date);
    }
    
    public void submit() {
        saveButton.submit();
    }
    
    public void enterDetailsAndSubmit(String desc,String targetDate) {
        enterDescription(desc);
        enterTargetDate(targetDate);
        submit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/UpdateTodoBasicTest.java

```java
package com.in28minutes.pageobjects.updatetodo;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.PageFactory;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UpdateTodoBasicTest {
    
    WebDriver driver;
    
    @BeforeTest
    public void beforeTest() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
    }

    @Test
    public void loginPageObject() {
        
        driver.get("http://localhost:8080/login");
        
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        
        //driver.findElement(By.id("name")).getAttribute("type")
        System.out.println(page.name.getAttribute("type"));//text
        
        //driver.findElement(By.id("password")).getAttribute("type")
        System.out.println(page.password.getAttribute("type"));//password
        
    }
    
    @Test
    public void updateTodo() {      
        
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        page.login("in28minutes", "dummy");
                    
        driver.findElement(By.linkText("Click here")).click();
        
        ListTodoPage listTodoPage = new ListTodoPage(driver);
        listTodoPage.clickUpdateFor("10002");
        
        TodoPage todoPage = PageFactory.initElements(driver, TodoPage.class);
        todoPage.enterDescription("Become a Tech Guru - 2");
        todoPage.enterTargetDate("12/09/2019");
        todoPage.submit();
        
        assertEquals(listTodoPage.getDescription("10002"), 
                            "Become a Tech Guru - 2");
        assertEquals(listTodoPage.getTargetDate("10002"), "12/09/2019");
        
    }
    
    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/UpdateTodoBasicTest1BeforePageObjects.java

```java
package com.in28minutes.pageobjects.updatetodo;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UpdateTodoBasicTest1BeforePageObjects {
    
    WebDriver driver;
    
    @BeforeTest
    public void beforeTest() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
    }

    @Test
    public void updateTodo() {
        
        driver.get("http://localhost:8080/login");
        
        //      LoginPage page = PageFactory.initElements(driver, LoginPage.class);

        driver.findElement(By.id("name")).sendKeys("in28minutes");
        driver.findElement(By.id("password")).sendKeys("dummy");
        driver.findElement(By.id("submit")).submit();
        
        //Click here - Link Text - click
        driver.findElement(By.linkText("Click here")).click();
        
        //id update-10002 click
        driver.findElement(By.id("update-10002")).click();
        
        //id desc
        WebElement desc = driver.findElement(By.id("desc"));
        desc.clear();
        desc.sendKeys("Become a Tech Guru - 2");
        
        //id targetDate
        WebElement targetDate = driver.findElement(By.id("targetDate"));
        targetDate.clear();
        targetDate.sendKeys("12/09/2019");
        
        //save submit
        driver.findElement(By.id("save")).submit();
        
        //check desc-10002
        String updatedDesc = driver.findElement(By.id("desc-10002")).getText();
        //check targetdate-10002
        String updatedTargetDate = driver.findElement(By.id("targetdate-10002")).getText();
        
        //Become a Tech Guru - 2
        //12/09/2019

        assertEquals(updatedDesc, "Become a Tech Guru - 2");
        assertEquals(updatedTargetDate, "12/09/2019");
        
    }
    
    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/UpdateTodoBasicTest2AfterLoginPage.java

```java
package com.in28minutes.pageobjects.updatetodo;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.PageFactory;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UpdateTodoBasicTest2AfterLoginPage {
    
    WebDriver driver;
    
    @BeforeTest
    public void beforeTest() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
    }

    @Test
    public void loginPageObject() {
        
        driver.get("http://localhost:8080/login");
        
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        
        //driver.findElement(By.id("name")).getAttribute("type")
        System.out.println(page.name.getAttribute("type"));//text
        
        //driver.findElement(By.id("password")).getAttribute("type")
        System.out.println(page.password.getAttribute("type"));//password
        
    }
    
    @Test
    public void updateTodo() {
        
        driver.get("http://localhost:8080/login");
        
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        page.login("in28minutes", "dummy");
            
        //page.enterName("in28minutes");
        //page.enterPassword("dummy");
        //page.submit();
        
        //page.name.sendKeys("in28minutes");
        //page.password.sendKeys("dummy");
        //page.submitButton.submit();
        
        //Click here - Link Text - click
        driver.findElement(By.linkText("Click here")).click();
        
        //id update-10002 click
        driver.findElement(By.id("update-10002")).click();
        
        //id desc
        WebElement desc = driver.findElement(By.id("desc"));
        desc.clear();
        desc.sendKeys("Become a Tech Guru - 2");
        
        //id targetDate
        WebElement targetDate = driver.findElement(By.id("targetDate"));
        targetDate.clear();
        targetDate.sendKeys("12/09/2019");
        
        //save submit
        driver.findElement(By.id("save")).submit();
        
        //check desc-10002
        String updatedDesc = driver.findElement(By.id("desc-10002")).getText();
        //check targetdate-10002
        String updatedTargetDate = driver.findElement(By.id("targetdate-10002")).getText();
        
        //Become a Tech Guru - 2
        //12/09/2019

        assertEquals(updatedDesc, "Become a Tech Guru - 2");
        assertEquals(updatedTargetDate, "12/09/2019");
        
    }
    
    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/UpdateTodoBasicTest3AfterListTodoPage.java

```java
package com.in28minutes.pageobjects.updatetodo;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.PageFactory;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UpdateTodoBasicTest3AfterListTodoPage {
    
    WebDriver driver;
    
    @BeforeTest
    public void beforeTest() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
    }

    @Test
    public void loginPageObject() {
        
        driver.get("http://localhost:8080/login");
        
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        
        //driver.findElement(By.id("name")).getAttribute("type")
        System.out.println(page.name.getAttribute("type"));//text
        
        //driver.findElement(By.id("password")).getAttribute("type")
        System.out.println(page.password.getAttribute("type"));//password
        
    }
    
    @Test
    public void updateTodo() {
        
        driver.get("http://localhost:8080/login");
        
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        page.login("in28minutes", "dummy");
                    
        //Click here - Link Text - click
        driver.findElement(By.linkText("Click here")).click();
        
        //id update-10002 click
        driver.findElement(By.id("update-10002")).click();
        
        TodoPage todoPage = PageFactory.initElements(driver, TodoPage.class);
        todoPage.enterDescription("Become a Tech Guru - 2");
        todoPage.enterTargetDate("12/09/2019");     
        todoPage.submit();
        
        //check desc-10002
        String updatedDesc = driver.findElement(By.id("desc-10002")).getText();
        //check targetdate-10002
        String updatedTargetDate = driver.findElement(By.id("targetdate-10002")).getText();
        
        //Become a Tech Guru - 2
        //12/09/2019

        assertEquals(updatedDesc, "Become a Tech Guru - 2");
        assertEquals(updatedTargetDate, "12/09/2019");
        
    }
    
    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/UpdateTodoBasicTest5AfterExercises.java

```java
package com.in28minutes.pageobjects.updatetodo;

import static org.testng.Assert.assertEquals;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.PageFactory;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class UpdateTodoBasicTest5AfterExercises {

    WebDriver driver;

    @BeforeTest
    public void beforeTest() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
    }

    @Test
    public void loginPageObject() {

        driver.get("http://localhost:8080/login");

        LoginPage page = PageFactory.initElements(driver, LoginPage.class);

        // driver.findElement(By.id("name")).getAttribute("type")
        System.out.println(page.name.getAttribute("type"));// text

        // driver.findElement(By.id("password")).getAttribute("type")
        System.out.println(page.password.getAttribute("type"));// password

    }

    @Test
    public void updateTodo() {
        LoginPage page = PageFactory.initElements(driver, LoginPage.class);
        page.login("in28minutes", "dummy");

        new WelcomePage(driver).clickTodosLink();

        ListTodoPage listTodoPage = new ListTodoPage(driver);
        listTodoPage.clickUpdateFor("10002");

        TodoPage todoPage = PageFactory.initElements(driver, TodoPage.class);
        todoPage.enterDetailsAndSubmit("Become a Tech Guru - 2", "12/09/2019");

        assertEquals(listTodoPage.getDescription("10002"), "Become a Tech Guru - 2");
        assertEquals(listTodoPage.getTargetDate("10002"), "12/09/2019");
    }

    @AfterTest
    public void afterTest() {
        driver.quit();
    }
}
```
---

### /web-driver-5-page-object-model/src/test/java/com/in28minutes/pageobjects/updatetodo/WelcomePage.java

```java
package com.in28minutes.pageobjects.updatetodo;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class WelcomePage {
    
    private WebDriver driver;
    
    public WelcomePage(WebDriver driver) {
        super();
        this.driver = driver;
    }

    public void clickTodosLink() {
        driver.findElement(By.linkText("Click here")).click();
    }
}
```
---

### /web-driver-6-stand-alone-and-grid/src/test/java/com/in28minutes/SeleniumHubTest.java

```java
package com.in28minutes;

import java.net.MalformedURLException;
import java.net.URL;

import org.openqa.selenium.Platform;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class SeleniumHubTest {
    //selenium-standalone start -- -role hub

    //Nodes should register to http://192.168.8.69:4444/grid/register/
    
    //Clients should connect to http://192.168.8.69:4444/wd/hub
    
    //selenium-standalone start -- -role node -hub http://192.168.8.69:4444/grid/register/ 
    
    //selenium-standalone start -- -role node -port 5556 -hub http://192.168.8.69:4444/grid/register/ 

    @Test(threadPoolSize=2, invocationCount=4)
    public void hub_chrome() throws MalformedURLException, InterruptedException {
        
        DesiredCapabilities capabilites = new DesiredCapabilities();
        
        //chrome, firefox, htmlunit, internet explorer, iphone, opera
        capabilites.setBrowserName("chrome");
        //capabilites.setPlatform(Platform.EL_CAPITAN);
        
        //WebDriverManager.chromedriver().setup();
        //WebDriver driver = new ChromeDriver();
        WebDriver remoteDriver = new RemoteWebDriver(
                new URL("http://localhost:4444/wd/hub"), capabilites);
        
        //RemoteWebDriver
        //  Location of Standaloneserver
        //  Which Browser? Which OS? => Capabilities
        
        remoteDriver.get("http://localhost:8080/pages/index.html");
        System.out.println(remoteDriver.getCurrentUrl());
        System.out.println(remoteDriver.getTitle());
        Thread.sleep(10000);
        remoteDriver.quit();
    }

    @Test(threadPoolSize=2, invocationCount=4)
    public void hub_firefox() throws MalformedURLException, InterruptedException {
        
        DesiredCapabilities capabilites = new DesiredCapabilities();
        
        //chrome, firefox, htmlunit, internet explorer, iphone, opera
        capabilites.setBrowserName("firefox");
        
        //WebDriverManager.chromedriver().setup();
        //WebDriver driver = new ChromeDriver();
        WebDriver remoteDriver = new RemoteWebDriver(
                new URL("http://localhost:4444/wd/hub"), capabilites);
        
        //RemoteWebDriver
        //  Location of Standaloneserver
        //  Which Browser? Which OS? => Capabilities
        
        remoteDriver.get("http://localhost:8080/pages/index.html");
        System.out.println(remoteDriver.getCurrentUrl());
        System.out.println(remoteDriver.getTitle());
        Thread.sleep(10000);
        remoteDriver.quit();
    }
    
}
```
---

### /web-driver-6-stand-alone-and-grid/src/test/java/com/in28minutes/SeleniumStandAloneTest.java

```java
package com.in28minutes;

import java.net.MalformedURLException;
import java.net.URL;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.testng.annotations.Test;

import io.github.bonigarcia.wdm.WebDriverManager;

public class SeleniumStandAloneTest {
    
    @Test
    public void basic() {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        driver.get("http://localhost:8080/pages/index.html");
        System.out.println(driver.getCurrentUrl());
        System.out.println(driver.getTitle());
        driver.quit();
    }
    
    @Test
    public void standalone() throws MalformedURLException, InterruptedException {
        
        DesiredCapabilities capabilites = new DesiredCapabilities();
        
        //chrome, firefox, htmlunit, internet explorer, iphone, opera
        capabilites.setBrowserName("chrome");
        
        //WebDriverManager.chromedriver().setup();
        //WebDriver driver = new ChromeDriver();
        WebDriver remoteDriver = new RemoteWebDriver(
                new URL("http://localhost:4444/wd/hub"), capabilites);
        
        //RemoteWebDriver
        //  Location of Standaloneserver
        //  Which Browser? Which OS? => Capabilities
        
        remoteDriver.get("http://localhost:8080/pages/index.html");
        System.out.println(remoteDriver.getCurrentUrl());
        System.out.println(remoteDriver.getTitle());
        Thread.sleep(15000);
        remoteDriver.quit();
    }
    
}
```
---

# Your First Full Stack Application with Angular and Spring Boot

## Complete Code Example

---

### /frontend/todo/src/app/app-routing.module.ts

```
import { TodoComponent } from './todo/todo.component';
import { RouteGuardService } from './service/route-guard.service';
import { LogoutComponent } from './logout/logout.component';
import { ListTodosComponent } from './list-todos/list-todos.component';
import { WelcomeComponent } from './welcome/welcome.component';
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { LoginComponent } from './login/login.component';
import { ErrorComponent } from './error/error.component';

// welcome 
const routes: Routes = [
  { path: '', component: LoginComponent  },//canActivate, RouteGuardService
  { path: 'login', component: LoginComponent },
  { path: 'welcome/:name', component: WelcomeComponent, canActivate:[RouteGuardService]},
  { path: 'todos', component: ListTodosComponent, canActivate:[RouteGuardService] },
  { path: 'logout', component: LogoutComponent, canActivate:[RouteGuardService] },
  { path: 'todos/:id', component: TodoComponent, canActivate:[RouteGuardService] },

  { path: '**', component: ErrorComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```
---

### /frontend/todo/src/app/app.component.css

```css
```
---

### /frontend/todo/src/app/app.component.html

```html
<!--<app-welcome></app-welcome>-->

<!-- <app-login></app-login> -->
<!--
<div>Component Content</div>-->

<app-menu></app-menu>

<div class="container">
    <router-outlet></router-outlet>
</div>

<app-footer></app-footer>
```
---

### /frontend/todo/src/app/app.component.ts

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  //template: '<h1>{{title}}<h1>',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'todo';
  message = 'Welcome to in28Minutes';
}
```
---

### /frontend/todo/src/app/app.constants.ts

```
export const API_URL = "http://localhost:8080"
export const TODO_JPA_API_URL = "http://localhost:8080/jpa"
```
---

### /frontend/todo/src/app/app.module.ts

```
import { HttpIntercepterBasicAuthService } from './service/http/http-intercepter-basic-auth.service';
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { WelcomeComponent } from './welcome/welcome.component';
import { LoginComponent } from './login/login.component';
import { ErrorComponent } from './error/error.component';
import { ListTodosComponent } from './list-todos/list-todos.component';
import { MenuComponent } from './menu/menu.component';
import { FooterComponent } from './footer/footer.component';
import { LogoutComponent } from './logout/logout.component';
import { TodoComponent } from './todo/todo.component';

@NgModule({
  declarations: [
    AppComponent,
    WelcomeComponent,
    LoginComponent,
    ErrorComponent,
    ListTodosComponent,
    MenuComponent,
    FooterComponent,
    LogoutComponent,
    TodoComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [
     {provide: HTTP_INTERCEPTORS, useClass: HttpIntercepterBasicAuthService, multi: true }
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
---

### /frontend/todo/src/app/error/error.component.css

```css
```
---

### /frontend/todo/src/app/error/error.component.html

```html
{{errorMessage}}
```
---

### /frontend/todo/src/app/error/error.component.ts

```
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-error',
  templateUrl: './error.component.html',
  styleUrls: ['./error.component.css']
})
export class ErrorComponent implements OnInit {

  errorMessage = 'An Error Occured! Contact Support at *** - ***'

  constructor() { }

  ngOnInit() {
  }

}
```
---

### /frontend/todo/src/app/footer/footer.component.css

```css
.footer {
    position: absolute;
    bottom: 0;
    width:100%;
    height: 40px;
    background-color: #222222;
}
```
---

### /frontend/todo/src/app/footer/footer.component.html

```html
<footer class="footer">
    <div class="container">
        <span class="text-muted">All Rights Reserved 2018 @in28minutes</span>
    </div>

</footer>
```
---

### /frontend/todo/src/app/footer/footer.component.ts

```
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-footer',
  templateUrl: './footer.component.html',
  styleUrls: ['./footer.component.css']
})
export class FooterComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

}
```
---

### /frontend/todo/src/app/list-todos/list-todos.component.css

```css
```
---

### /frontend/todo/src/app/list-todos/list-todos.component.html

```html
<h1> Todo </h1>

<div class="alert alert-success" *ngIf='message'>{{message}}</div>

<div class="container">
  <table class="table">
    <thead>
      <tr>
        <th>Description</th>
        <th>Target Date</th>
        <th>is Completed?</th>
        <th>Update</th>
        <th>Delete</th>
      </tr>
    </thead>
    <tbody>
      <!--   for (Todo todo: todos) {  -->
              <tr *ngFor="let todo of todos">
                <td>{{todo.description}}</td>
                <td>{{todo.targetDate | date | uppercase}}</td>
                <td>{{todo.done}}</td>
                <td><button (click)="updateTodo(todo.id)" class="btn btn-success">Update</button></td>
                <td><button (click)="deleteTodo(todo.id)" class="btn btn-warning">Delete</button></td>
              </tr>
      <!-- } -->
    </tbody>

  </table>

  <div class="row">
      <button (click)="addTodo()" class="btn btn-success">Add</button>
  </div>

</div>
```
---

### /frontend/todo/src/app/list-todos/list-todos.component.ts

```
import { TodoDataService } from './../service/data/todo-data.service';
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

export class Todo {
  constructor(
    public id: number,
    public description: string,
    public done: boolean,
    public targetDate: Date
  ){

  }
}

@Component({
  selector: 'app-list-todos',
  templateUrl: './list-todos.component.html',
  styleUrls: ['./list-todos.component.css']
})
export class ListTodosComponent implements OnInit {

  todos: Todo[]

  message: string

  // = [
  //   new Todo(1, 'Learn to Dance', false, new Date()),
  //   new Todo(2, 'Become an Expert at Angular', false, new Date()),
  //   new Todo(3, 'Visit India', false, new Date())
  //   // {id : 1, description : },
  //   // {id : 2, description : ''},
  //   // {id : 3, description : 'Visit India'}
  // ]

  // todo = {
  //     id : 1,
  //     description: 'Learn to Dance'
  // }

  constructor(
    private todoService:TodoDataService,
    private router : Router
  ) { }

  ngOnInit() {
    this.refreshTodos();
  }

  refreshTodos(){
    this.todoService.retrieveAllTodos('in28minutes').subscribe(
      response => {
        console.log(response);
        this.todos = response;
      }
    )
  }

  deleteTodo(id) {
    console.log(`delete todo ${id}` )
    this.todoService.deleteTodo('in28minutes', id).subscribe (
      response => {
        console.log(response);
        this.message = `Delete of Todo ${id} Successful!`;
        this.refreshTodos();
      }
    )
  }

  updateTodo(id) {
    console.log(`update ${id}`)
    this.router.navigate(['todos',id])
  }

  addTodo() {
    this.router.navigate(['todos',-1])
  }
}
```
---

### /frontend/todo/src/app/login/login.component.css

```css
```
---

### /frontend/todo/src/app/login/login.component.html

```html
<H1>Login!</H1>

<div class="container">
  <div class="alert alert-warning" *ngIf='invalidLogin'>{{errorMessage}}</div>

  <div>
    User Name : <input type="text" name="username" [(ngModel)]="username">
    Password  : <input type="password" name="password" [(ngModel)]="password">

    <!-- User Name : {{username}} -->

    <!-- <button (click)=handleLogin() class="btn btn-success">Login</button> -->
    <!-- <button (click)=handleBasicAuthLogin() class="btn btn-success">Login</button> -->
    <button (click)=handleJWTAuthLogin() class="btn btn-success">Login</button>
    
  </div>
</div>
```
---

### /frontend/todo/src/app/login/login.component.ts

```
import { BasicAuthenticationService } from './../service/basic-authentication.service';
import { HardcodedAuthenticationService } from './../service/hardcoded-authentication.service';
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css']
})
export class LoginComponent implements OnInit {

  username = 'in28minutes'
  password = ''
  errorMessage = 'Invalid Credentials'
  invalidLogin = false

  //Router
  //Angular.giveMeRouter
  //Dependency Injection
  constructor(private router: Router,
    private hardcodedAuthenticationService: HardcodedAuthenticationService,
    private basicAuthenticationService: BasicAuthenticationService) { }

  ngOnInit() {
  }

  handleLogin() {
    // console.log(this.username);
    //if(this.username==="in28minutes" && this.password === 'dummy') {
    if(this.hardcodedAuthenticationService.authenticate(this.username, this.password)) {
      //Redirect to Welcome Page
      this.router.navigate(['welcome', this.username])
      this.invalidLogin = false
    } else {
      this.invalidLogin = true
    }
  }

  handleBasicAuthLogin() {
    // console.log(this.username);
    //if(this.username==="in28minutes" && this.password === 'dummy') {
    this.basicAuthenticationService.executeAuthenticationService(this.username, this.password)
        .subscribe(
          data => {
            console.log(data)
            this.router.navigate(['welcome', this.username])
            this.invalidLogin = false      
          },
          error => {
            console.log(error)
            this.invalidLogin = true
          }
        )
  }

  handleJWTAuthLogin() {
    this.basicAuthenticationService.executeJWTAuthenticationService(this.username, this.password)
        .subscribe(
          data => {
            console.log(data)
            this.router.navigate(['welcome', this.username])
            this.invalidLogin = false      
          },
          error => {
            console.log(error)
            this.invalidLogin = true
          }
        )
  }

}
```
---

### /frontend/todo/src/app/logout/logout.component.css

```css
```
---

### /frontend/todo/src/app/logout/logout.component.html

```html
<H1>You are logged out</H1>
<div class="container">
  Thank You For Using Our Application.
</div>
```
---

### /frontend/todo/src/app/logout/logout.component.ts

```
import { HardcodedAuthenticationService } from './../service/hardcoded-authentication.service';
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-logout',
  templateUrl: './logout.component.html',
  styleUrls: ['./logout.component.css']
})
export class LogoutComponent implements OnInit {

  constructor(
    private hardcodedAuthenticationService: HardcodedAuthenticationService
  ) { }

  ngOnInit() {
    this.hardcodedAuthenticationService.logout();
  }

}
```
---

### /frontend/todo/src/app/menu/menu.component.css

```css
```
---

### /frontend/todo/src/app/menu/menu.component.html

```html
<header>
    <nav class="navbar navbar-expand-md navbar-dark bg-dark">
        <div><a href="https://www.in28minutes.com" class="navbar-brand">
            in28minutes</a></div>

        <ul class="navbar-nav">
            <li><a *ngIf="hardcodedAuthenticationService.isUserLoggedIn()" routerLink="/welcome/in28minutes" class="nav-link">Home</a></li>
            <li><a *ngIf="hardcodedAuthenticationService.isUserLoggedIn()" routerLink="/todos" class="nav-link">Todos</a></li>
        </ul>

        <ul class="navbar-nav navbar-collapse justify-content-end">
                <li><a *ngIf="!hardcodedAuthenticationService.isUserLoggedIn()" routerLink="/login" class="nav-link">Login</a></li>
                <li><a *ngIf="hardcodedAuthenticationService.isUserLoggedIn()" routerLink="/logout" class="nav-link">Logout</a></li>
        </ul>
    </nav>
</header>
```
---

### /frontend/todo/src/app/menu/menu.component.ts

```
import { HardcodedAuthenticationService } from './../service/hardcoded-authentication.service';
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-menu',
  templateUrl: './menu.component.html',
  styleUrls: ['./menu.component.css']
})
export class MenuComponent implements OnInit {
  //isUserLoggedIn: boolean = false;

  constructor(private hardcodedAuthenticationService 
    : HardcodedAuthenticationService) { }

  ngOnInit() {
    //this.isUserLoggedIn = this.hardcodedAuthenticationService.isUserLoggedIn();
  }

}
```
---

### /frontend/todo/src/app/service/basic-authentication.service.ts

```
import { API_URL } from './../app.constants';
import { HttpHeaders, HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import {map} from 'rxjs/operators';

export const TOKEN = 'token'
export const AUTHENTICATED_USER = 'authenticaterUser'

@Injectable({
  providedIn: 'root'
})
export class BasicAuthenticationService {

  constructor(private http: HttpClient) { }

  executeJWTAuthenticationService(username, password) {
    
    return this.http.post<any>(
      `${API_URL}/authenticate`,{
        username,
        password
      }).pipe(
        map(
          data => {
            sessionStorage.setItem(AUTHENTICATED_USER, username);
            sessionStorage.setItem(TOKEN, `Bearer ${data.token}`);
            return data;
          }
        )
      );
    //console.log("Execute Hello World Bean Service")
  }


  executeAuthenticationService(username, password) {
    
    let basicAuthHeaderString = 'Basic ' + window.btoa(username + ':' + password);

    let headers = new HttpHeaders({
        Authorization: basicAuthHeaderString
      })

    return this.http.get<AuthenticationBean>(
      `${API_URL}/basicauth`,
      {headers}).pipe(
        map(
          data => {
            sessionStorage.setItem(AUTHENTICATED_USER, username);
            sessionStorage.setItem(TOKEN, basicAuthHeaderString);
            return data;
          }
        )
      );
    //console.log("Execute Hello World Bean Service")
  }

  getAuthenticatedUser() {
    return sessionStorage.getItem(AUTHENTICATED_USER)
  }

  getAuthenticatedToken() {
    if(this.getAuthenticatedUser())
      return sessionStorage.getItem(TOKEN)
  }

  isUserLoggedIn() {
    let user = sessionStorage.getItem(AUTHENTICATED_USER)
    return !(user === null)
  }

  logout(){
    sessionStorage.removeItem(AUTHENTICATED_USER)
    sessionStorage.removeItem(TOKEN)
  }

}

export class AuthenticationBean{
  constructor(public message:string) { }
}
```
---

### /frontend/todo/src/app/service/data/todo-data.service.ts

```
import { TODO_JPA_API_URL } from './../../app.constants';
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Todo } from '../../list-todos/list-todos.component';

@Injectable({
  providedIn: 'root'
})
export class TodoDataService {

  constructor(
    private http:HttpClient
  ) { }

  retrieveAllTodos(username) {
    return this.http.get<Todo[]>(`${TODO_JPA_API_URL}/users/${username}/todos`);
    //console.log("Execute Hello World Bean Service")
  }

  deleteTodo(username, id){
    return this.http.delete(`${TODO_JPA_API_URL}/users/${username}/todos/${id}`);
  }

  retrieveTodo(username, id){
    return this.http.get<Todo>(`${TODO_JPA_API_URL}/users/${username}/todos/${id}`);
  }

  updateTodo(username, id, todo){
    return this.http.put(
          `${TODO_JPA_API_URL}/users/${username}/todos/${id}`
                , todo);
  }

  createTodo(username, todo){
    return this.http.post(
              `${TODO_JPA_API_URL}/users/${username}/todos`
                , todo);
  }

}
```
---

### /frontend/todo/src/app/service/data/welcome-data.service.ts

```
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Injectable } from '@angular/core';

export class HelloWorldBean {
  constructor(public message:string){ }
}

@Injectable({
  providedIn: 'root'
})
export class WelcomeDataService {

  constructor(
    private http:HttpClient
  ) { }

  executeHelloWorldBeanService() {
    return this.http.get<HelloWorldBean>('http://localhost:8080/hello-world-bean');
    //console.log("Execute Hello World Bean Service")
  }
  //http://localhost:8080/hello-world/path-variable/in28minutes

  executeHelloWorldServiceWithPathVariable(name) {
    // let basicAuthHeaderString = this.createBasicAuthenticationHttpHeader();

    // let headers = new HttpHeaders({
    //     Authorization: basicAuthHeaderString
    //   })

    return this.http.get<HelloWorldBean>(
      `http://localhost:8080/hello-world/path-variable/${name}`,
      //{headers}
      );
    //console.log("Execute Hello World Bean Service")
  }

  // createBasicAuthenticationHttpHeader() {
  //   let username = 'in28minutes'
  //   let password = 'dummy'
  //   let basicAuthHeaderString = 'Basic ' + window.btoa(username + ':' + password);
  //   return basicAuthHeaderString;
  // }
  //Access to XMLHttpRequest at 
  //'http://localhost:8080/hello-world/path-variable/in28minutes' 
  //from origin 'http://localhost:4200' has been blocked by CORS policy: 
  //No 'Access-Control-Allow-Origin' header is present on the requested resource.

  //Access to XMLHttpRequest at 'http://localhost:8080/hello-world/path-variable/in28minutes' from origin 'http://localhost:4200' 
  //has been blocked by CORS policy: 
  //Response to preflight request doesn't pass 
  //access control check: It does not have HTTP ok status
}
```
---

### /frontend/todo/src/app/service/hardcoded-authentication.service.ts

```
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class HardcodedAuthenticationService {

  constructor() { }

  authenticate(username, password) {
    //console.log('before ' + this.isUserLoggedIn());
    if(username==="in28minutes" && password === 'dummy') {
      sessionStorage.setItem('authenticaterUser', username);
      //console.log('after ' + this.isUserLoggedIn());
      return true;
    }
    return false;
  }

  isUserLoggedIn() {
    let user = sessionStorage.getItem('authenticaterUser')
    return !(user === null)
  }

  logout(){
    sessionStorage.removeItem('authenticaterUser')
  }

}
```
---

### /frontend/todo/src/app/service/http/http-intercepter-basic-auth.service.ts

```
import { BasicAuthenticationService } from './../basic-authentication.service';
import { HttpInterceptor, HttpHandler, HttpRequest } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class HttpIntercepterBasicAuthService implements HttpInterceptor{

  constructor(
    private basicAuthenticationService : BasicAuthenticationService
  ) { }

  intercept(request: HttpRequest<any>, next: HttpHandler){
    // let username = 'in28minutes'
    // let password = 'dummy'
    //let basicAuthHeaderString = 'Basic ' + window.btoa(username + ':' + password);
    let basicAuthHeaderString = this.basicAuthenticationService.getAuthenticatedToken();
    let username = this.basicAuthenticationService.getAuthenticatedUser()

    if(basicAuthHeaderString && username) { 
      request = request.clone({
        setHeaders : {
            Authorization : basicAuthHeaderString
          }
        }) 
    }
    return next.handle(request);
  }


}
```
---

### /frontend/todo/src/app/service/route-guard.service.ts

```
import { HardcodedAuthenticationService } from './hardcoded-authentication.service';
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class RouteGuardService implements CanActivate {

  constructor(
    private hardcodedAuthenticationService: HardcodedAuthenticationService,
    private router: Router) {

  }

  canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot) {

    if (this.hardcodedAuthenticationService.isUserLoggedIn())
      return true;

    this.router.navigate(['login']);

    return false;
  }
}
```
---

### /frontend/todo/src/app/todo/todo.component.css

```css
.ng-invalid:not(form) {
    border-left: 5px solid red;
}
```
---

### /frontend/todo/src/app/todo/todo.component.html

```html
<H1>Todo</H1>

<div class="container">
  <div class="alert alert-warning" *ngIf="todoForm.dirty && todoForm.invalid">Enter valid values</div>
  <div class="alert alert-warning" *ngIf="todoForm.dirty && targetDate.invalid">Enter valid Target Date</div>
  <div class="alert alert-warning" *ngIf="todoForm.dirty && description.invalid">Enter atleast 5 characters in Description</div>
  
  <form (ngSubmit)="!todoForm.invalid && saveTodo()" #todoForm="ngForm">
    <fieldset class="form-group">
      <label>Description</label>
      <input type="text" #description="ngModel" 
            [(ngModel)]="todo.description" class="form-control" 
                name="description" required="required" minlength="5">
    </fieldset>

    <fieldset class="form-group">
        <label>Target Date</label>
        <input type="date" #targetDate="ngModel"
        [ngModel]="todo.targetDate | date:'yyyy-MM-dd' "
        (ngModelChange)="todo.targetDate = $event"
        class="form-control" name="targetDate" required="required" >
    </fieldset>

    <button type="submit" class="btn btn-success">Save</button>
  </form>  
</div>
```
---

### /frontend/todo/src/app/todo/todo.component.ts

```
import { ActivatedRoute, Router } from '@angular/router';
import { TodoDataService } from './../service/data/todo-data.service';
import { Component, OnInit } from '@angular/core';
import { Todo } from '../list-todos/list-todos.component';

@Component({
  selector: 'app-todo',
  templateUrl: './todo.component.html',
  styleUrls: ['./todo.component.css']
})
export class TodoComponent implements OnInit {

  id:number
  todo: Todo

  constructor(
    private todoService: TodoDataService,
    private route: ActivatedRoute,
    private router: Router
  ) { }

  ngOnInit() {
    
    this.id = this.route.snapshot.params['id'];
    
    this.todo = new Todo(this.id,'',false,new Date());
    
    if(this.id!=-1) {
      this.todoService.retrieveTodo('in28minutes', this.id)
          .subscribe (
            data => this.todo = data
          )
    }
  }

  saveTodo() {
    if(this.id == -1) { //=== ==
      this.todoService.createTodo('in28minutes', this.todo)
          .subscribe (
            data => {
              console.log(data)
              this.router.navigate(['todos'])
            }
          )
    } else {
      this.todoService.updateTodo('in28minutes', this.id, this.todo)
          .subscribe (
            data => {
              console.log(data)
              this.router.navigate(['todos'])
            }
          )
    }
  }

}
```
---

### /frontend/todo/src/app/welcome/welcome.component.css

```css
```
---

### /frontend/todo/src/app/welcome/welcome.component.html

```html
<H1>Welcome!</H1>

<div class="container">
  Welcome {{name}}. You can manage your todos <a routerLink="/todos">here</a>
</div>

<div class="container">
  Click here to get a customized welcome message 
  <button (click)="getWelcomeMessageWithParameter()" class="btn btn-success">Get Welcome Message</button>
</div>

<div class="container" *ngIf="welcomeMessageFromService">
    <H2>Your Customized Welcome Message</H2>
    {{welcomeMessageFromService}}
  </div>
```
---

### /frontend/todo/src/app/welcome/welcome.component.ts

```
import { WelcomeDataService } from './../service/data/welcome-data.service';
import { ActivatedRoute } from '@angular/router';
//package com.in28minutes.springboot.web;

//import org.springframework.boot.SpringApplication;
import { Component, OnInit } from '@angular/core';//'./app.component';
//import { AppComponent } from '../app.component';

//@ComponentScan(
//      value = "com.in28minutes.springboot.web")
@Component({
  selector: 'app-welcome',
  templateUrl: './welcome.component.html',
  styleUrls: ['./welcome.component.css']
})

//public class SpringBootFirstWebApplication implements SomeInterface{
export class WelcomeComponent implements OnInit {

  message = 'Some Welcome Message'
  welcomeMessageFromService:string
  name = ''
  //String message = "Some Welcome Message"
  
  //public SpringBootFirstWebApplication() {	

  //ActivatedRoute
  constructor(
    private route:ActivatedRoute,
    private service:WelcomeDataService) { 

  }

  // void init() {
  ngOnInit(){
    //COMPILATION ERROR this.message = 5
    //console.log(this.message)
    // console.log(this.route.snapshot.params['name'])
    this.name = this.route.snapshot.params['name'];
    
  }

  getWelcomeMessage() {
    //console.log(this.service.executeHelloWorldBeanService());
    
    this.service.executeHelloWorldBeanService().subscribe(
      response => this.handleSuccessfulResponse(response),
      error => this.handleErrorResponse(error)
    );
    
    //console.log('last line of getWelcomeMessage')

    //console.log("get welcome message");
  }

  getWelcomeMessageWithParameter() {
    //console.log(this.service.executeHelloWorldBeanService());
    
    this.service.executeHelloWorldServiceWithPathVariable(this.name).subscribe(
      response => this.handleSuccessfulResponse(response),
      error => this.handleErrorResponse(error)
    );
    
    //console.log('last line of getWelcomeMessage')

    //console.log("get welcome message");
  }


  handleSuccessfulResponse(response){
    this.welcomeMessageFromService = response.message
    //console.log(response);
    //console.log(response.message);
  }

  handleErrorResponse(error) {
    //console.log(error);
    //console.log(error.error);
    //console.log(error.error.message);
    this.welcomeMessageFromService = error.error.message
  }
}

export class Class1 {

}

export class Class2 {
  
}
```
---

### /frontend/todo/src/browserslist

```
# This file is currently used by autoprefixer to adjust CSS to support the below specified browsers
# For additional information regarding the format and rule options, please see:
# https://github.com/browserslist/browserslist#queries
#
# For IE 9-11 support, please remove 'not' from the last line of the file and adjust as needed

> 0.5%
last 2 versions
Firefox ESR
not dead
not IE 9-11
```
---

### /frontend/todo/src/environments/environment.prod.ts

```
export const environment = {
  production: true
};
```
---

### /frontend/todo/src/environments/environment.ts

```
// This file can be replaced during build by using the `fileReplacements` array.
// `ng build --prod` replaces `environment.ts` with `environment.prod.ts`.
// The list of file replacements can be found in `angular.json`.

export const environment = {
  production: false
};

/*
 * For easier debugging in development mode, you can import the following file
 * to ignore zone related error stack frames such as `zone.run`, `zoneDelegate.invokeTask`.
 *
 * This import should be commented out in production mode because it will have a negative impact
 * on performance if an error is thrown.
 */
// import 'zone.js/dist/zone-error';  // Included with Angular CLI.
```
---

### /frontend/todo/src/index.html

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>My Todos Application</title>
  <base href="/">

  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
  <!-- <div>Index HTML Content</div> -->
</body>
</html>
```

### /frontend/todo/src/main.ts

```
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```
---

### /frontend/todo/src/styles.css

```css
/* You can add global styles to this file, and also import other style files */
@import url(https://unpkg.com/bootstrap@4.1.0/dist/css/bootstrap.min.css)
```
---

### /frontend/todo/src/test.ts

```
// This file is required by karma.conf.js and loads recursively all the .spec and framework files

import 'zone.js/dist/zone-testing';
import { getTestBed } from '@angular/core/testing';
import {
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting
} from '@angular/platform-browser-dynamic/testing';

declare const require: any;

// First, initialize the Angular testing environment.
getTestBed().initTestEnvironment(
  BrowserDynamicTestingModule,
  platformBrowserDynamicTesting()
);
// Then we find all the tests.
const context = require.context('./', true, /\.spec\.ts$/);
// And load the modules.
context.keys().map(context);
```
---

### /frontend/todo/src/todos.txt

```
- <script type="text/javascript" src="runtime.js">
</script><script type="text/javascript" src="polyfills.js"></script><script type="text/javascript" src="styles.js">
</script><script type="text/javascript" src="vendor.js"></script><script type="text/javascript" src="main.js"></script>
```

### /frontend/todo/package.json

```json
{
  "name": "todo",
  "version": "0.0.0",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
  "private": true,
  "dependencies": {
    "@angular/animations": "~7.0.0",
    "@angular/common": "~7.0.0",
    "@angular/compiler": "~7.0.0",
    "@angular/core": "~7.0.0",
    "@angular/forms": "~7.0.0",
    "@angular/http": "~7.0.0",
    "@angular/platform-browser": "~7.0.0",
    "@angular/platform-browser-dynamic": "~7.0.0",
    "@angular/router": "~7.0.0",
    "core-js": "^2.5.4",
    "rxjs": "~6.3.3",
    "zone.js": "~0.8.26"
  },
  "devDependencies": {
    "@angular-devkit/build-angular": "~0.10.0",
    "@angular/cli": "~7.0.3",
    "@angular/compiler-cli": "~7.0.0",
    "@angular/language-service": "~7.0.0",
    "@types/node": "~8.9.4",
    "@types/jasmine": "~2.8.8",
    "@types/jasminewd2": "~2.0.3",
    "codelyzer": "~4.5.0",
    "jasmine-core": "~2.99.1",
    "jasmine-spec-reporter": "~4.2.1",
    "karma": "~3.0.0",
    "karma-chrome-launcher": "~2.2.0",
    "karma-coverage-istanbul-reporter": "~2.0.1",
    "karma-jasmine": "~1.1.2",
    "karma-jasmine-html-reporter": "^0.2.2",
    "protractor": "~5.4.0",
    "ts-node": "~7.0.0",
    "tslint": "~5.11.0",
    "typescript": "~3.1.1"
  }
}
```
---


### /restful-web-services/src/main/java/com/in28minutes/rest/basic/auth/AuthenticationBean.java

```java
package com.in28minutes.rest.basic.auth;

public class AuthenticationBean {

	private String message;

	public AuthenticationBean(String message) {
		this.message = message;
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	@Override
	public String toString() {
		return String.format("HelloWorldBean [message=%s]", message);
	}

}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/basic/auth/BasicAuthenticationController.java

```java
package com.in28minutes.rest.basic.auth;

import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

//Controller
@CrossOrigin(origins="http://localhost:4200")
@RestController
public class BasicAuthenticationController {

	@GetMapping(path = "/basicauth")
	public AuthenticationBean helloWorldBean() {
		//throw new RuntimeException("Some Error has Happened! Contact Support at ***-***");
		return new AuthenticationBean("You are authenticated");
	}	
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/basic/auth/SpringSecurityConfigurationBasicAuth.java

```java
package com.in28minutes.rest.basic.auth;

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
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/BcryptEncoderTest.java

```java
package com.in28minutes.rest.webservices.restfulwebservices;

import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

public class BcryptEncoderTest {

	public static void main(String[] args) {
		BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();
		
		for(int i=1; i<=10; i++) {
			String encodedString = encoder.encode("password@!23@#!");
			System.out.println(encodedString);
		}
		
		// TODO Auto-generated method stub

	}

}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/helloworld/HelloWorldBean.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.helloworld;

public class HelloWorldBean {

	private String message;

	public HelloWorldBean(String message) {
		this.message = message;
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	@Override
	public String toString() {
		return String.format("HelloWorldBean [message=%s]", message);
	}

}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/helloworld/HelloWorldController.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.helloworld;

import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

//Controller
@CrossOrigin(origins="http://localhost:4200")
@RestController
public class HelloWorldController {

	@GetMapping(path = "/hello-world")
	public String helloWorld() {
		return "Hello World";
	}

	@GetMapping(path = "/hello-world-bean")
	public HelloWorldBean helloWorldBean() {
		//throw new RuntimeException("Some Error has Happened! Contact Support at ***-***");
		return new HelloWorldBean("Hello World - Changed");
	}
	
	///hello-world/path-variable/in28minutes
	@GetMapping(path = "/hello-world/path-variable/{name}")
	public HelloWorldBean helloWorldPathVariable(@PathVariable String name) {
		return new HelloWorldBean(String.format("Hello World, %s", name));
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/JwtInMemoryUserDetailsService.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;

@Service
public class JwtInMemoryUserDetailsService implements UserDetailsService {

	static List<JwtUserDetails> inMemoryUserList = new ArrayList<>();

	static {
		inMemoryUserList.add(new JwtUserDetails(1L, "in28minutes",
				"$2a$10$3zHzb.Npv1hfZbLEU5qsdOju/tk2je6W6PnNnY.c1ujWPcZh4PL6e", "ROLE_USER_2"));
		inMemoryUserList.add(new JwtUserDetails(2L, "ranga",
				"$2a$10$IetbreuU5KihCkDB6/r1DOJO0VyU9lSiBcrMDT.biU7FOt2oqZDPm", "ROLE_USER_2"));
		
		//$2a$10$IetbreuU5KihCkDB6/r1DOJO0VyU9lSiBcrMDT.biU7FOt2oqZDPm
	}

	@Override
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
		Optional<JwtUserDetails> findFirst = inMemoryUserList.stream()
				.filter(user -> user.getUsername().equals(username)).findFirst();

		if (!findFirst.isPresent()) {
			throw new UsernameNotFoundException(String.format("USER_NOT_FOUND '%s'.", username));
		}

		return findFirst.get();
	}

}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/JwtTokenAuthorizationOncePerRequestFilter.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt;

import java.io.IOException;

import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import io.jsonwebtoken.ExpiredJwtException;

@Component
public class JwtTokenAuthorizationOncePerRequestFilter extends OncePerRequestFilter {

	private final Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired
	private UserDetailsService jwtInMemoryUserDetailsService;

	@Autowired
	private JwtTokenUtil jwtTokenUtil;

	@Value("${jwt.http.request.header}")
	private String tokenHeader;

	@Override
	protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
			throws ServletException, IOException {
		logger.debug("Authentication Request For '{}'", request.getRequestURL());

		final String requestTokenHeader = request.getHeader(this.tokenHeader);

		String username = null;
		String jwtToken = null;
		if (requestTokenHeader != null && requestTokenHeader.startsWith("Bearer ")) {
			jwtToken = requestTokenHeader.substring(7);
			try {
				username = jwtTokenUtil.getUsernameFromToken(jwtToken);
			} catch (IllegalArgumentException e) {
				logger.error("JWT_TOKEN_UNABLE_TO_GET_USERNAME", e);
			} catch (ExpiredJwtException e) {
				logger.warn("JWT_TOKEN_EXPIRED", e);
			}
		} else {
			logger.warn("JWT_TOKEN_DOES_NOT_START_WITH_BEARER_STRING");
		}

		logger.debug("JWT_TOKEN_USERNAME_VALUE '{}'", username);
		if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {

			UserDetails userDetails = this.jwtInMemoryUserDetailsService.loadUserByUsername(username);

			if (jwtTokenUtil.validateToken(jwtToken, userDetails)) {
				UsernamePasswordAuthenticationToken usernamePasswordAuthenticationToken = new UsernamePasswordAuthenticationToken(
						userDetails, null, userDetails.getAuthorities());
				usernamePasswordAuthenticationToken
						.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
				SecurityContextHolder.getContext().setAuthentication(usernamePasswordAuthenticationToken);
			}
		}

		chain.doFilter(request, response);
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/JwtTokenUtil.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt;

import java.io.Serializable;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Component;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Clock;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.impl.DefaultClock;

@Component
public class JwtTokenUtil implements Serializable {

	static final String CLAIM_KEY_USERNAME = "sub";
	static final String CLAIM_KEY_CREATED = "iat";
	private static final long serialVersionUID = -3301605591108950415L;
	private Clock clock = DefaultClock.INSTANCE;

	@Value("${jwt.signing.key.secret}")
	private String secret;

	@Value("${jwt.token.expiration.in.seconds}")
	private Long expiration;

	public String getUsernameFromToken(String token) {
		return getClaimFromToken(token, Claims::getSubject);
	}

	public Date getIssuedAtDateFromToken(String token) {
		return getClaimFromToken(token, Claims::getIssuedAt);
	}

	public Date getExpirationDateFromToken(String token) {
		return getClaimFromToken(token, Claims::getExpiration);
	}

	public <T> T getClaimFromToken(String token, Function<Claims, T> claimsResolver) {
		final Claims claims = getAllClaimsFromToken(token);
		return claimsResolver.apply(claims);
	}

	private Claims getAllClaimsFromToken(String token) {
		return Jwts.parser().setSigningKey(secret).parseClaimsJws(token).getBody();
	}

	private Boolean isTokenExpired(String token) {
		final Date expiration = getExpirationDateFromToken(token);
		return expiration.before(clock.now());
	}

	private Boolean ignoreTokenExpiration(String token) {
		// here you specify tokens, for that the expiration is ignored
		return false;
	}

	public String generateToken(UserDetails userDetails) {
		Map<String, Object> claims = new HashMap<>();
		return doGenerateToken(claims, userDetails.getUsername());
	}

	private String doGenerateToken(Map<String, Object> claims, String subject) {
		final Date createdDate = clock.now();
		final Date expirationDate = calculateExpirationDate(createdDate);

		return Jwts.builder().setClaims(claims).setSubject(subject).setIssuedAt(createdDate)
				.setExpiration(expirationDate).signWith(SignatureAlgorithm.HS512, secret).compact();
	}

	public Boolean canTokenBeRefreshed(String token) {
		return (!isTokenExpired(token) || ignoreTokenExpiration(token));
	}

	public String refreshToken(String token) {
		final Date createdDate = clock.now();
		final Date expirationDate = calculateExpirationDate(createdDate);

		final Claims claims = getAllClaimsFromToken(token);
		claims.setIssuedAt(createdDate);
		claims.setExpiration(expirationDate);

		return Jwts.builder().setClaims(claims).signWith(SignatureAlgorithm.HS512, secret).compact();
	}

	public Boolean validateToken(String token, UserDetails userDetails) {
		JwtUserDetails user = (JwtUserDetails) userDetails;
		final String username = getUsernameFromToken(token);
		return (username.equals(user.getUsername()) && !isTokenExpired(token));
	}

	private Date calculateExpirationDate(Date createdDate) {
		return new Date(createdDate.getTime() + expiration * 1000);
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/JwtUnAuthorizedResponseAuthenticationEntryPoint.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt;

import java.io.IOException;
import java.io.Serializable;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.security.core.AuthenticationException;
import org.springframework.security.web.AuthenticationEntryPoint;
import org.springframework.stereotype.Component;

@Component
public class JwtUnAuthorizedResponseAuthenticationEntryPoint implements AuthenticationEntryPoint, Serializable {

	private static final long serialVersionUID = -8970718410437077606L;

	@Override
	public void commence(HttpServletRequest request, HttpServletResponse response,
			AuthenticationException authException) throws IOException {
		response.sendError(HttpServletResponse.SC_UNAUTHORIZED,
				"You would need to provide the Jwt Token to Access This resource");
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/JwtUserDetails.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import com.fasterxml.jackson.annotation.JsonIgnore;

public class JwtUserDetails implements UserDetails {

	private static final long serialVersionUID = 5155720064139820502L;

	private final Long id;
	private final String username;
	private final String password;
	private final Collection<? extends GrantedAuthority> authorities;

	public JwtUserDetails(Long id, String username, String password, String role) {
		this.id = id;
		this.username = username;
		this.password = password;

		List<SimpleGrantedAuthority> authorities = new ArrayList<SimpleGrantedAuthority>();
		authorities.add(new SimpleGrantedAuthority(role));

		this.authorities = authorities;
	}

	@JsonIgnore
	public Long getId() {
		return id;
	}

	@Override
	public String getUsername() {
		return username;
	}

	@JsonIgnore
	@Override
	public boolean isAccountNonExpired() {
		return true;
	}

	@JsonIgnore
	@Override
	public boolean isAccountNonLocked() {
		return true;
	}

	@JsonIgnore
	@Override
	public boolean isCredentialsNonExpired() {
		return true;
	}

	@JsonIgnore
	@Override
	public String getPassword() {
		return password;
	}

	@Override
	public Collection<? extends GrantedAuthority> getAuthorities() {
		return authorities;
	}

	@Override
	public boolean isEnabled() {
		return true;
	}

}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/JWTWebSecurityConfig.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.builders.WebSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class JWTWebSecurityConfig extends WebSecurityConfigurerAdapter {

	@Autowired
	private JwtUnAuthorizedResponseAuthenticationEntryPoint jwtUnAuthorizedResponseAuthenticationEntryPoint;

	@Autowired
	private UserDetailsService jwtInMemoryUserDetailsService;

	@Autowired
	private JwtTokenAuthorizationOncePerRequestFilter jwtAuthenticationTokenFilter;

	@Value("${jwt.get.token.uri}")
	private String authenticationPath;

	@Autowired
	public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
		auth.userDetailsService(jwtInMemoryUserDetailsService).passwordEncoder(passwordEncoderBean());
	}

	@Bean
	public PasswordEncoder passwordEncoderBean() {
		return new BCryptPasswordEncoder();
	}

	@Bean
	@Override
	public AuthenticationManager authenticationManagerBean() throws Exception {
		return super.authenticationManagerBean();
	}

	@Override
	protected void configure(HttpSecurity httpSecurity) throws Exception {
		httpSecurity.csrf().disable().exceptionHandling()
				.authenticationEntryPoint(jwtUnAuthorizedResponseAuthenticationEntryPoint).and().sessionManagement()
				.sessionCreationPolicy(SessionCreationPolicy.STATELESS).and().authorizeRequests().anyRequest()
				.authenticated();

		httpSecurity.addFilterBefore(jwtAuthenticationTokenFilter, UsernamePasswordAuthenticationFilter.class);

		httpSecurity.headers().frameOptions().sameOrigin() // H2 Console Needs this setting
				.cacheControl(); // disable caching
	}

	@Override
	public void configure(WebSecurity webSecurity) throws Exception {
		webSecurity.ignoring().antMatchers(HttpMethod.POST, authenticationPath)
				.antMatchers(HttpMethod.OPTIONS, "/**")
				.and().ignoring()
				.antMatchers(HttpMethod.GET, "/" // Other Stuff You want to Ignore
				).and().ignoring()
				.antMatchers("/h2-console/**/**");// Should not be done in Production!
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/resource/AuthenticationException.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt.resource;

public class AuthenticationException extends RuntimeException {
	public AuthenticationException(String message, Throwable cause) {
		super(message, cause);
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/resource/JwtAuthenticationRestController.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt.resource;

import java.util.Objects;

import javax.servlet.http.HttpServletRequest;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.BadCredentialsException;
import org.springframework.security.authentication.DisabledException;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import com.in28minutes.rest.webservices.restfulwebservices.jwt.JwtTokenUtil;
import com.in28minutes.rest.webservices.restfulwebservices.jwt.JwtUserDetails;

@RestController
@CrossOrigin(origins = "http://localhost:4200")
public class JwtAuthenticationRestController {

	@Value("${jwt.http.request.header}")
	private String tokenHeader;

	@Autowired
	private AuthenticationManager authenticationManager;

	@Autowired
	private JwtTokenUtil jwtTokenUtil;

	@Autowired
	private UserDetailsService jwtInMemoryUserDetailsService;

	@RequestMapping(value = "${jwt.get.token.uri}", method = RequestMethod.POST)
	public ResponseEntity<?> createAuthenticationToken(@RequestBody JwtTokenRequest authenticationRequest)
			throws AuthenticationException {

		authenticate(authenticationRequest.getUsername(), authenticationRequest.getPassword());

		final UserDetails userDetails = jwtInMemoryUserDetailsService
				.loadUserByUsername(authenticationRequest.getUsername());

		final String token = jwtTokenUtil.generateToken(userDetails);

		return ResponseEntity.ok(new JwtTokenResponse(token));
	}

	@RequestMapping(value = "${jwt.refresh.token.uri}", method = RequestMethod.GET)
	public ResponseEntity<?> refreshAndGetAuthenticationToken(HttpServletRequest request) {
		String authToken = request.getHeader(tokenHeader);
		final String token = authToken.substring(7);
		String username = jwtTokenUtil.getUsernameFromToken(token);
		JwtUserDetails user = (JwtUserDetails) jwtInMemoryUserDetailsService.loadUserByUsername(username);

		if (jwtTokenUtil.canTokenBeRefreshed(token)) {
			String refreshedToken = jwtTokenUtil.refreshToken(token);
			return ResponseEntity.ok(new JwtTokenResponse(refreshedToken));
		} else {
			return ResponseEntity.badRequest().body(null);
		}
	}

	@ExceptionHandler({ AuthenticationException.class })
	public ResponseEntity<String> handleAuthenticationException(AuthenticationException e) {
		return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body(e.getMessage());
	}

	private void authenticate(String username, String password) {
		Objects.requireNonNull(username);
		Objects.requireNonNull(password);

		try {
			authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(username, password));
		} catch (DisabledException e) {
			throw new AuthenticationException("USER_DISABLED", e);
		} catch (BadCredentialsException e) {
			throw new AuthenticationException("INVALID_CREDENTIALS", e);
		}
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/resource/JwtTokenRequest.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt.resource;

import java.io.Serializable;

public class JwtTokenRequest implements Serializable {

	private static final long serialVersionUID = -5616176897013108345L;

	private String username;
	private String password;

	public JwtTokenRequest() {
		super();
	}

	public JwtTokenRequest(String username, String password) {
		this.setUsername(username);
		this.setPassword(password);
	}

	public String getUsername() {
		return this.username;
	}

	public void setUsername(String username) {
		this.username = username;
	}

	public String getPassword() {
		return this.password;
	}

	public void setPassword(String password) {
		this.password = password;
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/jwt/resource/JwtTokenResponse.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.jwt.resource;

import java.io.Serializable;

public class JwtTokenResponse implements Serializable {

	private static final long serialVersionUID = 8317676219297719109L;

	private final String token;

	public JwtTokenResponse(String token) {
		this.token = token;
	}

	public String getToken() {
		return this.token;
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/RestfulWebServicesApplication.java

```java
package com.in28minutes.rest.webservices.restfulwebservices;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class RestfulWebServicesApplication {

	public static void main(String[] args) {
		SpringApplication.run(RestfulWebServicesApplication.class, args);
	}
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/todo/Todo.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.todo;

import java.util.Date;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Todo {
	
	@Id
	@GeneratedValue
	private Long id;
	
	private String username;
	private String description;
	private Date targetDate;
	private boolean isDone;
	
	protected Todo() {
		
	}
	
	public Todo(long id, String username, String description, Date targetDate, boolean isDone) {
		super();
		this.id = id;
		this.username = username;
		this.description = description;
		this.targetDate = targetDate;
		this.isDone = isDone;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getUsername() {
		return username;
	}

	public void setUsername(String username) {
		this.username = username;
	}

	public String getDescription() {
		return description;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	public Date getTargetDate() {
		return targetDate;
	}

	public void setTargetDate(Date targetDate) {
		this.targetDate = targetDate;
	}

	public boolean isDone() {
		return isDone;
	}

	public void setDone(boolean isDone) {
		this.isDone = isDone;
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + (int) (id ^ (id >>> 32));
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Todo other = (Todo) obj;
		if (id != other.id)
			return false;
		return true;
	}

	
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/todo/TodoHardcodedService.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.todo;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

import org.springframework.stereotype.Service;


@Service
public class TodoHardcodedService {
	
	private static List<Todo> todos = new ArrayList<>();
	private static long idCounter = 0;
	
	static {
		todos.add(new Todo(++idCounter, "in28minutes","Learn to Dance 2", new Date(), false ));
		todos.add(new Todo(++idCounter, "in28minutes","Learn about Microservices 2", new Date(), false ));
		todos.add(new Todo(++idCounter, "in28minutes","Learn about Angular", new Date(), false ));
	}
	
	public List<Todo> findAll() {
		return todos;
	}

	public Todo save(Todo todo) {
		if(todo.getId()==-1 || todo.getId()==0) {
			todo.setId(++idCounter);
			todos.add(todo);
		} else {
			deleteById(todo.getId());
			todos.add(todo);
		}
		return todo;
	}
	
	public Todo deleteById(long id) {
		Todo todo = findById(id);
		
		if(todo==null) return null;
		
		if(todos.remove(todo)) {
			return todo;
		}
		
		return null;
	}

	public Todo findById(long id) {
		for(Todo todo:todos) {
			if(todo.getId() == id) {
				return todo;
			}
		}
		
		return null;
	}
	
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/todo/TodoJpaRepository.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.todo;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface TodoJpaRepository extends JpaRepository<Todo, Long>{
	List<Todo> findByUsername(String username);
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/todo/TodoJpaResource.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.todo;

import java.net.URI;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

import com.in28minutes.rest.webservices.restfulwebservices.todo.Todo;

@CrossOrigin(origins="http://localhost:4200")
@RestController
public class TodoJpaResource {
	
	@Autowired
	private TodoHardcodedService todoService;

	@Autowired
	private TodoJpaRepository todoJpaRepository;

	
	@GetMapping("/jpa/users/{username}/todos")
	public List<Todo> getAllTodos(@PathVariable String username){
		return todoJpaRepository.findByUsername(username);
		//return todoService.findAll();
	}

	@GetMapping("/jpa/users/{username}/todos/{id}")
	public Todo getTodo(@PathVariable String username, @PathVariable long id){
		return todoJpaRepository.findById(id).get();
		//return todoService.findById(id);
	}

	//DELETE /users/{username}/todos/{id}
	@DeleteMapping("/jpa/users/{username}/todos/{id}")
	public ResponseEntity<Void> deleteTodo(
			@PathVariable String username, @PathVariable long id){
		
		//Todo todo = todoService.deleteById(id);
		todoJpaRepository.deleteById(id);
		
		return ResponseEntity.noContent().build();
		//return ResponseEntity.notFound().build();
	}
	

	//Edit/Update a Todo
	//PUT /users/{user_name}/todos/{todo_id}
	@PutMapping("/jpa/users/{username}/todos/{id}")
	public ResponseEntity<Todo> updateTodo(
			@PathVariable String username,
			@PathVariable long id, @RequestBody Todo todo){
		
		//Todo todoUpdated = todoService.save(todo);
		Todo todoUpdated = todoJpaRepository.save(todo);
		
		return new ResponseEntity<Todo>(todo, HttpStatus.OK);
	}
	
	@PostMapping("/jpa/users/{username}/todos")
	public ResponseEntity<Void> createTodo(
			@PathVariable String username, @RequestBody Todo todo){
		
		//Todo createdTodo = todoService.save(todo);
		todo.setUsername(username);
		Todo createdTodo = todoJpaRepository.save(todo);
		
		//Location
		//Get current resource url
		///{id}
		URI uri = ServletUriComponentsBuilder.fromCurrentRequest()
				.path("/{id}").buildAndExpand(createdTodo.getId()).toUri();
		
		return ResponseEntity.created(uri).build();
	}
		
}
```
---

### /restful-web-services/src/main/java/com/in28minutes/rest/webservices/restfulwebservices/todo/TodoResource.java

```java
package com.in28minutes.rest.webservices.restfulwebservices.todo;

import java.net.URI;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;

import com.in28minutes.rest.webservices.restfulwebservices.todo.Todo;

@CrossOrigin(origins="http://localhost:4200")
@RestController
public class TodoResource {
	
	@Autowired
	private TodoHardcodedService todoService;
	
	@GetMapping("/users/{username}/todos")
	public List<Todo> getAllTodos(@PathVariable String username){
		return todoService.findAll();
	}

	@GetMapping("/users/{username}/todos/{id}")
	public Todo getTodo(@PathVariable String username, @PathVariable long id){
		return todoService.findById(id);
	}

	//DELETE /users/{username}/todos/{id}
	@DeleteMapping("/users/{username}/todos/{id}")
	public ResponseEntity<Void> deleteTodo(
			@PathVariable String username, @PathVariable long id){
		
		Todo todo = todoService.deleteById(id);
		
		if(todo!=null) {
			return ResponseEntity.noContent().build();
		}
		
		return ResponseEntity.notFound().build();
	}
	

	//Edit/Update a Todo
	//PUT /users/{user_name}/todos/{todo_id}
	@PutMapping("/users/{username}/todos/{id}")
	public ResponseEntity<Todo> updateTodo(
			@PathVariable String username,
			@PathVariable long id, @RequestBody Todo todo){
		
		Todo todoUpdated = todoService.save(todo);
		
		return new ResponseEntity<Todo>(todo, HttpStatus.OK);
	}
	
	@PostMapping("/users/{username}/todos")
	public ResponseEntity<Void> updateTodo(
			@PathVariable String username, @RequestBody Todo todo){
		
		Todo createdTodo = todoService.save(todo);
		
		//Location
		//Get current resource url
		///{id}
		URI uri = ServletUriComponentsBuilder.fromCurrentRequest()
				.path("/{id}").buildAndExpand(createdTodo.getId()).toUri();
		
		return ResponseEntity.created(uri).build();
	}
		
}
```
---

### /restful-web-services/src/main/resources/application.properties

```properties
logging.level.org.springframework = info

#spring.security.user.name=in28minutes
#spring.security.user.password=dummy

jwt.signing.key.secret=mySecret
jwt.get.token.uri=/authenticate
jwt.refresh.token.uri=/refresh
jwt.http.request.header=Authorization
jwt.token.expiration.in.seconds=604800

spring.jpa.show-sql=true
spring.h2.console.enabled=true
```
---

### /restful-web-services/src/main/resources/data.sql

```
insert into todo(id, username,description,target_date,is_done)
values(10001, 'in28minutes', 'Learn JPA', sysdate(), false);

insert into todo(id, username,description,target_date,is_done)
values(10002, 'in28minutes', 'Learn Data JPA', sysdate(), false);

insert into todo(id, username,description,target_date,is_done)
values(10003, 'in28minutes', 'Learn Microservices', sysdate(), false);
```
---

### /restful-web-services/src/test/java/com/in28minutes/rest/webservices/restfulwebservices/RestfulWebServicesApplicationTests.java

```java
package com.in28minutes.rest.webservices.restfulwebservices;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class RestfulWebServicesApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

# Learn Java Programming in 250 Steps

## Code Snippets

```java
3*4
System.out.println(3*4)
System.out.println("5 * 2 = 10")
3.0/2
System.out.println("5 * 2")
System.out.println(5 * 2)
System.out.println("Hello World")
System.out.println(5*3)
System.out.println("5 * 3")
System.out.println(5*3)
System.out.println("5 * 1 = 5")
System.out.println("5 * 2 = 5")
System.out.println("5 * 3 = 5")
System.out.println("24 * 60 * 60")
System.out.println(24 * 60 * 60)
System.out.println("Hello World")
System.out.println("Hello     World")
System.out.println(24   *    60    *    60)
System.out.println("Hello World")
System.out.println("HelloWorld")
System.out.println("hello world")
System.out.println("hello \"world")
System.out.println("hello \"world")
System.out.println("hello n world")
System.out.println("hello \n world")
System.out.println("hello \nworld")
System.out.println("hello\nworld")
System.out.println("hello\tworld")
System.out.println("hello \\ world")
System.out.println("hello \\\\ world")
Math.random()
System.out.println("hello \n world")
Math.min(23,45)
Math.min(23,4)
Math.max(23,4)
System.out.println("5 * 2 = 5")
System.out.println("5 * 2 = 10")
5*2
System.out.printf("5 * 2 = 10")
System.out.printf("5 * 2 = 10").println()
System.out.printf("5 * 2 = 10 %d", 5*2).println()
System.out.printf("5 * 2 = %d", 5*2).println()
System.out.printf("%d %d %d", 5, 7, 5 * 7).println()
System.out.printf("%d * %d = %d", 5, 7, 5 * 7).println()
System.out.printf("%d + %d + %d = %d", 5, 6, 7, 5 + 6 + 7).println()
System.out.printf("%d + %d + %d = %d", 5, 6, 7).println()
System.out.printf("%d + %d + %d", 5, 6, 7).println()
System.out.printf("%d + %d + %d", 5, 6).println()
System.out.printf("%d + %d + %d", 5, 6, 7, 8).println()
System.out.printf("Print %s", "Testing").println()
System.out.printf("%d + %d + %d", 5.5, 6.5, 7.5).println()
System.out.printf("%f + %f + %f", 5.5, 6.5, 7.5).println()
System.out.printf("5 * 2 = 10")
System.out.printf("%d * %d = %d", 5, 2, 5 * 2).println()
System.out.println("5 * 2 = 10")
System.out.printf("%d * %d = %d", 5, 2, 5 * 2).println()
System.out.printf("%d * %d = %d", 5, 1, 5 * 1).println()
System.out.printf("%d * %d = %d", 5, 2, 5 * 2).println()
System.out.printf("%d * %d = %d", 5, 3, 5 * 3).println()
System.out.printf("%d * %d = %d", 5, 4, 5 * 4).println()
number = 11
number
number = 12
number
number2 = 100
System.out.printf("%d * %d = %d", 5, 4, 5 * 4).println()
System.out.printf("%d * %d = %d", 5, i, 5 * i).println()
i
5 * i
i = 2
System.out.printf("%d * %d = %d", 5, i, 5 * i).println()
i = 3
System.out.printf("%d * %d = %d", 5, i, 5 * i).println()
i = 10
System.out.printf("%d * %d = %d", 5, i, 5 * i).println()
System.out.printf("a + b + c = a+b+c").println()
System.out.printf("%d + %d + %d = %d", a, b, c ,a+b+c).println()
a = 50
System.out.printf("%d + %d + %d = %d", a, b, c ,a+b+c).println()
b = 60
System.out.printf("%d + %d + %d = %d", a, b, c ,a+b+c).println()
int newVariable;
newVariable
int undeclaredVariable;
undeclaredVariable
5 * undeclaredVariable
a = 100
a = c
int noOfGoals;
int NoOfGoals;
int score;
short s;
float f = 4.0f;
float f2 = 4.5f;
double dbl = 4.5;
i = j
i
j
i = j
i = j * 2
i = i * 2
i = i + i
i = i - i
i = i - 1
i++
i
i++
i
i--
number = number + 1
number++
number--
++number
--number
number--
number
i = i + 2
i += 2
i -= 1
i *= 5
i
i /= 4
i %= 2
;
long l = 6_000_000_000l;
short numberOfGoals;
numberOfGoals++
numberOfGoals
numberOfGoals++
numberOfGoals
long populationOfTheWorld;
double average;
char ch = 'A';
ch = 'B'
char grade = 'C';
grade = 'A'
grade
boolean isEven;
isEven = true
boolean isPrime;
boolean isItRainingToday;
boolean areYouEnjoyingTheCourse;
areYouEnjoyingTheCourse = true
System.out.printf("%d * %d = %d", 5, i, 5*i);
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
i = 7
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
i = 10
i < 5
i > 5
i <= 5
i <= 10
i >= 10
System.out.println("i is less than 5");
i
if (i<5)
   System.out.println("i is less than 5");
i
i = 4
if (i<5)
   System.out.println("i is less than 5");
int number1 = 5;
int number2 = 7;
if (number2>number1)
System.out.println("number2 is greater than number1");
number2 = 3
if (number2>number1)
System.out.println("number2 is greater than number1");
int a = 1;
int b = 2;
int c = 3;
int d = 1;
if(a+b > c +d)
System.out.println("a+b is greater than c+d");
a = 6
if(a+b > c +d)
System.out.println("a+b is greater than c+d");
if ( a + b > c + d )
    System.out.println("a+b is greater than c+d");
int angle1 = 20;
int angle2 = 60;
int angle3 = 50;
if(angle1 + angle2 + angle3 == 180)
    System.out.println("Valid Triangle");
angle3 += 50
angle3
angle1
angle2
if(angle1 + angle2 + angle3 == 180)
    System.out.println("Valid Triangle");
int number = 10;
number % 2
9 % 2
8 % 2
if (number % 2 == 0)
System.out.println("number is even");
if (number % 2 == 0)
System.out.println("number is even");
number = 9
if (number % 2 == 0)
System.out.println("number is even");
i > 5
i = 5
i == 5
i == 6
if(i==5)
System.out.println("i is odd");
if(i==5)
System.out.println("i is odd");
 System.out.println("i is prime");
i == 6
i = 6
if(i==5)
System.out.println("i is odd");
 System.out.println("i is prime");
if(i==5) {
System.out.println("i is odd");
System.out.println("i is prime");
}
if(i==5) {
System.out.println("i is prime");
}
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
i = i + 1
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
i = i + 1
System.out.printf("%d * %d = %d", 5, i, 5*i).println()
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", 5, i, 5*i).println();
}
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", 6, i, 6*i).println();
}
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", 7, i, 7*i).println();
}
int table = 7;
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", table, i, table*i).println();
}
table = 8
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", table, i, table*i).println();
}
table = 8
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", table, i, table*i).println();
}
table = 9
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", table, i, table*i).println();
}
for(i =1; i<=10; i++) {
   System.out.printf("%d", i).println();
}
for(i=10; i<=1  ;i--) {
   System.out.printf("%d", i).println();
}
for(i=10; i>=1  ;i--) {
   System.out.printf("%d", i).println();
}
for(i=10; i>=1  ;i = i - 2) {
   System.out.printf("%d", i).println();
}
for(i=9; i>=1  ;i = i - 2) {
   System.out.printf("%d", i).println();
}
for(i =1; i<=10; i++) {
   System.out.printf("%d", i * i).println();
}
for(i =2; i<=10; i = i + 2) {
   System.out.printf("%d", i * i).println();
}
for(i =2; i<=20; i = i + 2) {
   System.out.printf("%d", i * i).println();
}
for(i =1; i<=10; i++) {
   System.out.printf("%d", (2 * i) * (2 * i) ).println();
}
for(i =1; i<=20; i = i + 2) {
   System.out.printf("%d", i * i).println();
}
int i = 1;
for ( ;i<=10 ;i++ );
i
for (i=1 ;i<=10 ;i++ );
int j;
for (i=1, j=2 ;i<=10 ;i++, j++ );
i
j
for (i=1, j=2 ;i<=10 ;i++, j--);
i
j
for(;;);
for(int i=1; i<=10; i++) {
System.out.println("No 1");
System.out.println("No 2");
}
for(int i=1; i<=10; i++) {
System.out.println("No 1");
System.out.println("No 2");
}
   System.out.println("i is less than 5");
```

## 02-IntroductionToMethods-MultiplicationTable

## Steps
- Step 00 - Section 02 - Methods - An Introduction
- Step 01 - Your First Java Method - Hello World Twice and Exercise Statements
- Step 02 - Introduction to Java Methods - Exercises and Puzzles
- Step 03 - Programming Tip - Editing Methods with JShell
- Step 04 - Introduction to Java Methods - Arguments and Parameters
- Step 05 - Introduction to Java Method Arguments - Exercises
- Step 06 - Introduction to Java Method Arguments - Puzzles and Tips
- Step 07 - Getting back to Multiplication Table - Creating a method
- Step 08 - Print Multiplication Table with a Parameter and Method Overloading
- Step 09 - Passing Multiple Parameters to a Java Method
- Step 10 - Returning from a Java Method - An Introduction
- Step 11 - Returning from a Java Method - Exercises
- Step 99 - Methods - Section Review

## Exercises

#### Methods - Basics
- Write and execute a method named ```sayHelloWorldThrice``` to print ```Hello World``` thrice.
- Write and execute a method that prints the following four statements:
   - ```I've created my first variable```
   - ```I've created my first loop```
   - ```I've created my first method```
   - ```I'm excited to learn Java```  

### Method Parameters
1. Write a method ```printNumbers(int n)``` that prints all successive integers from ```1``` to ```n```.
2. Write a method ```printSquaresOfNumbers(int n)``` that prints the squares of all successive integers from ```1``` to ```n```.

### Return value from Methods
1. Write a method that returns the sum of three integers.
2. Write a method that takes as input two integers representing two angles of a triangle, and computes the third angle. *Hint: The sum of the three angles of a triangle is 180 degrees*. 

## Code Snippets

```java
3 * 4
$2
$2 * 3
for( i =1; i<=10; i++) {
System.out.printf("%d * %d = %d", table, i, table*i).println();
}
for( i =1; i<=10; i++) {
    System.out.printf("%d * %d = %d", table, i, table*i).println();
}
for( i =1; i<=10; i++) {
    System.out.printf("%d * %d = %d", table, i, table*i).println();
}
for( i =1; i<=10; i++) {
   System.out.printf("%d * %d = %d", table, i, table*i).println();
}
int table = 7;
for( i =1; i<=10; i++) {
System.out.printf("%d * %d = %d", table, i, table*i).println();
}
table = 8
for( i =1; i<=10; i++) {
System.out.printf("%d * %d = %d", table, i, table*i).println();
}
System.out.println("Hello World")
System.out.println("Hello World")
System.out.println("Hello World")
System.out.println("Hello World");
 System.out.println("Hello World");
System.out.println("Hello World");
 System.out.println("Hello World");
sayHelloWorldTwice()
sayHelloWorldTwice()
void sayHelloWorldThrice(){
 System.out.println("Hello World");
 System.out.println("Hello World");
 System.out.println("Hello World");
}
sayHelloWorldThrice()
printLearningExperience()
printLearningExperience()
void NameOfMethod(){
}
void nameOfMethod(){
}
void sayHelloWorldTwice(){
   System.out.println("HelloWorld");
   System.out.println("HelloWorld");
}
sayHelloWorldTwice()
void printLearningExperience() {
System.out.println("I've created sdf first variable");
System.out.println("I've created fsadjf first method");
System.out.println("I've created fsajdfl first loop");
System.out.println("I'm excited fasdflkjfskfsd learn Java");
}
printLearningExperience()
sayHelloWorldThrice()
sayHelloWorldTwice()
sayHelloWorld(1)
sayHelloWorld(1)
sayHelloWorld(2)
sayHelloWorld(2)
sayHelloWorld(4)
sayHelloWorld(6)
void sayHelloWorld(int noOfTimes) {
	for(int i=1; i<=noOfTimes; i++) {
		System.out.println("Hello World");
	}
}
sayHelloWorld(6)
sayHelloWorld(3)
sayHelloWorld(2)
void printNumbers(int n) {
    for(int i=1; i<=n; i++) {
	    System.out.println(i);
    }
}
printNumbers(10)
printNumbers(3)
void printSquaresOfNumbers(int n) {
    for(int i=1; i<=n; i++) {
         System.out.println(i*i);
    }
}
printSquaresOfNumbers(5)
printSquaresOfNumbers(3)
sayHelloWorld(4)
for( i =1; i<=10; i++) {
	System.out.printf("%d * %d = %d", table, i, table*i).println();
}
int i;
for(i=1;i<=10;i++)
    System.out.printf("%d * %d = %d", 5, i, 5 * i).println();
for(i=1;i<=10;i++) {
    System.out.printf("%d * %d = %d", 5, i, 5 * i).println();
}
void printMultiplicationTable() {
	for(int i=1;i<=10;i++) {
		System.out.printf("%d * %d = %d", 5, i, 5 * i).println();
	}
}
printMultiplicationTable()

void printMultiplicationTable(int table) {
	for(int i=1;i<=10;i++) {
		System.out.printf("%d * %d = %d", table, i, table * i).println();
	}
}

printMultiplicationTable(6)
printMultiplicationTable(7)
printMultiplicationTable()
printMultiplicationTable(6)
Math.max(1,2)
void sum(int firstNumber,int secondNumber) {
     int sum = firstNumber + secondNumber;
     System.out.println(sum);
}
sum(5, 10)
void sum(int firstNumber,int secondNumber, int thirdNumber) {
     int sum = firstNumber + secondNumber + thirdNumber;
     System.out.println(sum);
}
sum(5, 10, 15)
Math.max(4,5)
$110
int max = Math.max(15, 25);
max
sum(1, 10)
int sumOfTwoNumbers(int firstNumber, int secondNumber) {
    int sum = firstNumber + secondNumber;
    return sum;
}
sumOfTwoNumbers(1,1)
int sum = sumOfThreeNumbers(2,3,4);
calculateThirdAngle(20, 50)
int sumOfThreeNumbers(int firstNumber, int secondNumber, int thirdNumber) {
      int sum = firstNumber + secondNumber + thirdNumber;
      return sum;
}
sumOfThreeNumbers(1,2,3)
sumOfThreeNumbers(15,2,3)
int calculateThirdAngle(int angle1, int angle2) {
       int angle3 = 180 - (angle1 + angle2);
       return angle3;
}
calculateThirdAngle(20, 20)
calculateThirdAngle(20, 20)
```


### 03-IntroductionToJavaPlatform

## Steps
- Step 00 - Section 03 - Overview Of Java Platform - Section Overview
- Step 01 - Overview Of Java Platform - An Introduction - java, javac, bytecode and JVM
- Step 02 - Java Class and Object - First Look
- Step 03 - Create a method in a Java class
- Step 04 - Create and Compile Planet.java class
- Step 05 - Run Planet calss with Java - Using a main method
- Step 06 - Play and Learn with Planet Class
- Step 07 - JDK vs JRE vs JVM

## Code Snippets (Including Output)

```java
jshell> System.out.println("I love JShell");
I love JShell

jshell> class Country {
   ...> }
|  created class Country

jshell> Country india = new Country()
india ==> Country@6e06451e

jshell> Country usa = new Country()
usa ==> Country@6e1567f1

jshell> class Planet {
   ...> }
|  created class Planet

jshell> Planet planet = new Planet()
planet ==> Planet@56ef9176

jshell> Planet earth = new Planet()
earth ==> Planet@1ed4004b

jshell> Planet venus = new Planet()
venus ==> Planet@25bbe1b6

jshell> void printMultiplicationTable() {
   ...>     for(int i=1;i<=10;i++) {
   ...>         System.out.printf("%d * %d = %d", 5, i, 5 * i).println();
   ...>     }
   ...> }
|  created method printMultiplicationTable()

jshell> void printMultiplicationTable(int table) {
   ...>     for(int i=1;i<=10;i++) {
   ...>         System.out.printf("%d * %d = %d", table, i, table * i).println();
   ...>     }
   ...> }
|  created method printMultiplicationTable(int)

jshell> 
 
jshell> /methods
|    void |    void printMultiplicationTable()
|    void printMultiplicationTable(int)

jshell>  
jshell> class Planet {
   ...> }
|  modified class Planet

jshell> Planet earth = new Planet()
earth ==> Planet@73846619

jshell> Planet venus = new Planet()
venus ==> Planet@4bec1f0c

jshell> class Planet {
   ...>      void revolve() {
   ...>           System.out.println("Revolve");
   ...>      }
   ...> }
|  replaced class Planet
|    update replaced variable planet, reset to null
|    update replaced variable earth, reset to null
|    update replaced variable venus, reset to null

jshell> Planet earth = new Planet()
earth ==> Planet@192b07fd

jshell> Planet venus = new Planet()
venus ==> Planet@64bfbc86

jshell> Planet.revolve()
|  Error:
|  non-static method revolve() cannot be referenced from a static context
|  Planet.revolve()
|  ^------------^

jshell> earth.revolve()
Revolve

jshell> venus.revolve()
Revolve

jshell> class Country {
   ...>    void comingSoon() {
   ...>       System.out.println("Coming Soon");
   ...>    }
   ...> }
|  replaced class Country
|    update replaced variable country, reset to null
|    update replaced variable india, reset to null
|    update replaced variable usa, reset to null

jshell> Country india = new Country()
india ==> Country@60c6f5b

jshell> Country netherlands = new Country()
netherlands ==> Country@3c0f93f1

jshell> india.comingSoon()
Coming Soon

jshell> netherlands.comingSoon()
Coming Soon

jshell> /list Country

  27 : class Country {
          void comingSoon() {
             System.out.println("Coming Soon");
          }
       }

jshell> /list Planet

  22 : class Planet {
            void revolve() {
                 System.out.println("Revolve");
            }
       }

jshell> 
```


### /03-IntroductionToJavaPlatform/Planet.java

```java
class Planet {

    void revolve() {
         System.out.println("Revolve");
    }

    public static void main(String[] args) {
    	Planet earth = new Planet();
    	earth.revolve();
    }
}
```

## 04-IntroductionToEclipse-FirstJavaProject

## Steps
- Step 00 - Intro to Section and Installing Eclipse
- Step 01 - Creating a New Java Project with Eclipse
- Step 02 - Your first Java class with Eclipse
- Step 03 - Writing Multiplication Table Java Program with Eclipse
- Step 04 - Adding more methods for Multiplication Table Program
- Step 05 - Programming Tip 1 : Refactoring with Eclipse
- Step 06 - Programming Tip 2 : Debugging with Eclipse
- Step 07 - Programming Tip 3 : Eclipse vs JShell - How to choose?

## Code Examples

### /04-IntroductionToEclipse-FirstJavaProject/src/com/in28minutes/firstjavaproject/HelloWorld.java

```java
package com.in28minutes.firstjavaproject;

public class HelloWorld {

	public static void main(String[] args) {
		
	}

}
```


### /04-IntroductionToEclipse-FirstJavaProject/src/com/in28minutes/firstjavaproject/KeyboardShortcuts.java

```java
package com.in28minutes.firstjavaproject;

public class KeyboardShortcuts {
	public static void main(String[] args) {
		int i = 0;
		System.out.println(i);
	}
}
```


### /04-IntroductionToEclipse-FirstJavaProject/src/com/in28minutes/firstjavaproject/MultiplicationTable.java

```java
package com.in28minutes.firstjavaproject;

public class MultiplicationTable {
	
	void print() {
		print(5);
	}
	
	void print(int table) {
		print(table, 1, 10);
	}
	
	void print(int table, int from, int to) {
		for (int i = from; i <= to; i++) {
			System.out.printf("%d X %d = %d", table, i, table * i).println();
		}
	}
}
```


### /04-IntroductionToEclipse-FirstJavaProject/src/com/in28minutes/firstjavaproject/MultiplicationTableRunner.java

```java
package com.in28minutes.firstjavaproject;

public class MultiplicationTableRunner {

	public static void main(String[] args) {
		MultiplicationTable table = new MultiplicationTable();
		table.print();
		
		//table.print(6);
		//table.print(6, 11, 20);
	}

}
```


### /04-IntroductionToEclipse-FirstJavaProject/src/com/in28minutes/firstjavaproject/MutliplicationTableBeforeRefactoring.java

```java
package com.in28minutes.firstjavaproject;

public class MutliplicationTableBeforeRefactoring {
	void print() {
		for (int i = 1; i <= 10; i++) {
			System.out.printf("%d X %d = %d", 5, i, 5 * i).println();
		}
	}

	void print(int table) {
		for (int i = 1; i <= 10; i++) {
			System.out.printf("%d X %d = %d", table, i, table * i).println();
		}
	}

	void print(int table, int from, int to) {
		for (int i = from; i <= to; i++) {
			System.out.printf("%d X %d = %d", table, i, table * i).println();
		}
	}
}
```


## 05-IntroductionToObjectOrientedProgramming

## Steps
- Step 00 - Introduction to Object Oriented Programming - Section Overview
- Step 01 - Introduction to Object Oriented Programming - Basics
- Step 02 - Introduction to Object Oriented Programming - Terminology - Class, Object, State and Behavior
- Step 03 - Introduction to Object Oriented Programming - Exercise - Online Shopping System and Person
- Step 04 - Create Motor Bike Java Class and a couple of objects
- Step 05 - Exercise Solutions - Book class and Three instances
- Step 06 - Introducing State of an object with speed variable
- Step 07 - Understanding basics of Encapsulation with Setter methods
- Step 08 - Exercises and Tips - Getters and Generating Getters and Setters with Eclipse
- Step 09 - Puzzles on this and initialization of member variables
- Step 10 - First Advantage of Encapsulation
- Step 11 - Introduction to Encapsulation - Level 2
- Step 12 - Encapsulation Exercises - Better Validation and Book class
- Step 13 - Introdcution to Abstraction
- Step 14 - Introduction to Java Constructors
- Step 15 - Introduction to Java Constructors - Exercises and Puzzles
- Step 16 - Introduction to Object Oriented Programming - Conclusion

## Exercises
- In each of the following systems, identify the basic entities involved, and organize them using object oriented terminology:
     - Online Shopping System
     - Person
- Provide Better Encapsulation and Validation for Book and MotorBike class
- Create a constructor for Book class and create three instances

## Code Examples

### /05-IntroductionToObjectOrientedProgramming/src/com/in28minutes/oops/Book.java

```java
package com.in28minutes.oops;

public class Book {
	
	private int noOfCopies;

	public Book(int noOfCopies) {
		this.noOfCopies = noOfCopies;
	}

	public void setNoOfCopies(int noOfCopies) {
		if (noOfCopies > 0)
			this.noOfCopies = noOfCopies;
	}

	public void increaseNoOfCopies(int howMuch) {
		setNoOfCopies(this.noOfCopies + howMuch);
	}

	public void decreaseNoOfCopies(int howMuch) {
		setNoOfCopies(this.noOfCopies - howMuch);
	}

}
```


### /05-IntroductionToObjectOrientedProgramming/src/com/in28minutes/oops/BookRunner.java

```java
package com.in28minutes.oops;

public class BookRunner {

	public static void main(String[] args) {
		// Create a new class called Book 
		// Create three instances
		Book artOfComputerProgramming = new Book(100);
		Book effectiveJava = new Book(50);
		Book cleanCode = new Book(40);
		
		artOfComputerProgramming.setNoOfCopies(100);
		effectiveJava.setNoOfCopies(50);
		cleanCode.setNoOfCopies(45);
	}

}
```


### /05-IntroductionToObjectOrientedProgramming/src/com/in28minutes/oops/MotorBike.java

```java
package com.in28minutes.oops;

public class MotorBike {
	//state
	private int speed; //member variable
	

	//constructors
	MotorBike() {
		this(5);
	}
	
	MotorBike(int speed) {
		this.speed = speed;
	}
	
	//behavior
	public int getSpeed() {
		return speed;
	}

	public void setSpeed(int speed) {
		if(speed > 0 )
			this.speed = speed;
	}

	public void increaseSpeed(int howMuch) {
		setSpeed(this.speed + howMuch);
	}

	public void decreaseSpeed(int howMuch) {
		setSpeed(this.speed - howMuch);
	}
	
	void start() {
		System.out.println("Bike Started");
	}
}
```


### /05-IntroductionToObjectOrientedProgramming/src/com/in28minutes/oops/MotorBikeRunner.java

```java
package com.in28minutes.oops;

public class MotorBikeRunner {

	public static void main(String[] args) {
		
		MotorBike ducati = new MotorBike(100);
		
		MotorBike honda = new MotorBike(200);
		
		MotorBike somethingElse = new MotorBike();
		
		System.out.println(ducati.getSpeed());
		
		System.out.println(honda.getSpeed());
		
		System.out.println(somethingElse.getSpeed());

		
		ducati.start();

		honda.start();
		
		//ducati.setSpeed(100);
		
		ducati.increaseSpeed(100);
				
		honda.increaseSpeed(100);
		
		ducati.decreaseSpeed(250);
		
		honda.decreaseSpeed(250);
		
		System.out.println(ducati.getSpeed());
		
		System.out.println(honda.getSpeed());
	}

}

// Create a new class called Book 
// Create three instances
// Art Of Computer Programming
// Effective Java
// Clean Code
```

### /05-IntroductionToObjectOrientedProgramming/entireoutput-constructor-puzzles.txt

```java
Last login: Mon Jan 29 10:33:44 on ttys000
Rangas-MacBook-Pro:~ rangaraokaranam$ jshell
|  Welcome to JShell -- Version 9.0.1
|  For an introduction type: /help intro

jshell> class Cart {
   ...> };
|  created class Cart

jshell> Cart cart1 = new Cart();
cart1 ==> Cart@3f49dace

jshell> class Cart {
   ...>     Cart() {
   ...>     }
   ...> };
|  replaced class Cart
|    update replaced variable cart1, reset to null

jshell> Cart cart1 = new Cart();
cart1 ==> Cart@59494225

jshell> class Cart {
   ...>     Cart() {
   ...>         System.out.println("Constructor is called");
   ...>     }
   ...> }
|  modified class Cart

jshell> Cart cart1 = new Cart();
Constructor is called
cart1 ==> Cart@6e1567f1

jshell> 
```


#  06-PrimitiveDataTypesAndAlternatives

## Steps
- Step 00 - Primitive Data Types in Depth - Section Overview
- Step 01 - Basics about Java Integer Data Types - Casting, Operators and More
- Step 02 - Java Integer Data Types - Puzzles - Octal, Hexadecimal, Post and Pre increment
- Step 03 - Java Integer Data Types - Exercises - BiNumber - add, multiply and double
- Step 04 - Java Floating Point Data Types - Casting , Conversion and Accuracy
- Step 05 - Introduction to BigDecimal Java Class
- Step 06 - BigDecimal Puzzles - Adding Integers
- Step 07 - BigDecimal Exercises - Simple Interest Calculation
- Step 08 - Java Boolean Data Type - Relational and Logical Operators
- Step 09 - Java Boolean Data Type - Puzzles - Short Circuit Operators
- Step 10 - Java Character Data Type char - Representation and Conversion
- Step 11 - Java char Data Type - Exercises 1 - isVowel
- Step 12 - Java char Data Type - Exercises 2 - isDigit
- Step 13 - Java char Data Type - Exercises 3 - isConsonant, List Upper Case and Lower Case Characters
- Step 14 - Primitive Data Types in Depth - Conclusion

## Exercises

#### Big Decimal

- Calculate formula for Simple Interest Formula
   - Total Amount = principal + principal * interest * noOfYears;

```java
 SimpleInterestCalculator calculator = 
        new SimpleInterestCalculator("4500.00", "7.5");
 BigDecimal totalValue = 
        calculator.calculateTotalValue(5);// 5 years
 System.out.println(totalSum);
```

#### char data type

Implement MyChar class

```java
MyChar myChar = new MyChar('c');
System.out.println(myChar.isVowel());
        //'a', 'e', 'i', 'o', 'u' and Capitals
System.out.println(myChar.isDigit());
System.out.println(myChar.isAlphabet());
MyChar.printLowerCaseAlphabets();
MyChar.printUpperCaseAlphabets();
```

## Code Examples

### /06-PrimitiveDataTypesAndAlternatives/commands.txt

```java
Byte.SIZE
Byte.BYTES
Byte.MAX_VALUE
Byte.MIN_VALUE
Short.BYTES
Integer.BYTES
Long.BYTES
Integer.MAX_VALUE
Short.MAX_VALUE
Byte.SIZE
Byte.MIN_VALUE
Byte.MAX_VALUE
Short.BYTES
Integer.BYTES
Long.BYTES
Integer.MAX_VALUE
byte c = 13;
long l = 50000000000l;
i = (int) l
l = i
int eight = 010;
int sixteen = 0x10;
int fifteen = 0XF;
int big = 0XBBAACC;
Short.MAX_VALUE
short s = (short) i;
int i1 = s;
i
i
i
i
34.5
34.56789
double dbl = 34.5678;
float f2 = (float)dbl;
dbl++
dbl--
dbl % 5
float f = i;
34.56789876 + 34.2234
number1.add(number2);
number1
BigDecimal number3 = number1.add(number2);
number1
BigDecimal number1 = new BigDecimal("34.56789876");
BigDecimal number10 = new BigDecimal(34.2234);
BigDecimal number11 = new BigDecimal("34.56789876");
number10.add(number11)
number10.multiply(number11)
BigDecimal number = new BigDecimal("11.5");
BigDecimal number2 = new BigDecimal("23.45678");
number.add(number2)
number.add(new BigDecimal(i))
number.multiply(new BigDecimal(i))
number.divide(new BigDecimal(100))
number.divide(new BigDecimal("100.01234"))
number.divide(new BigDecimal("100.012"))
number.divide(new BigDecimal("100.12"))
number.divide(new BigDecimal("100.1"))
number.divide(new BigDecimal("1001"))
number.divide(new BigDecimal("100"))
boolean isValue = false;
i > 7
i >= 7
i < 7
i <= 7
i == 6
i == 7
i == 8
i = 8
i = 7
i == 7
i > 15
i >= 15
i <= 25
i >= 15 && i <= 25
i = 30
i >= 15 && i <= 25
i = 5
i >= 15 && i <= 25
true && true
true && false
false && true
false && false
false || true
false || true
true || false
true || true
false || false
false ^ false
false ^ true
true ^ false
true ^ true
!true
!false
int x = 6;
!(x>7)
!(x>7)
true || ++i==11
i
int i = 10;
int j = 15;
j > 15 && i++ > 5
j
i
j > 15 & i++ > 5
j
i
i++;
i++;
char ch2 = '\u0022';
char ch3 = '\u00A2';
ch++
ch
++ch
++ch
ch + 5
ch
(int)ch
ch
System.out.println(ch);
char ch = '\t';
System.out.println(ch);
System.out.println(ch);
(int)'1'
(int)'0'
(int)'9'
(int)'2'
(int)'a'
(int)'z'
(int)'A'
(int)'Z'
		for (char ch = 'A'; ch <= 'Z'; ch++) {
			System.out.println(ch);

}
		for (char ch = 'A'; ch <= 'Z'; ch++) {
			System.out.println(ch);
}
		for (char ch = 'A'; ch <= 'C'; ch++) {
			System.out.println(ch);
}
```


### /06-PrimitiveDataTypesAndAlternatives/src/com/in28minutes/primitive/datatypes/BiNumber.java

```java
package com.in28minutes.primitive.datatypes;

public class BiNumber {
	private int number1;
	private int number2;

	public int getNumber1() {
		return number1;
	}

	public void setNumber1(int number1) {
		this.number1 = number1;
	}

	public int getNumber2() {
		return number2;
	}

	public void setNumber2(int number2) {
		this.number2 = number2;
	}

	public BiNumber(int number1, int number2) {
		this.number1 = number1;
		this.number2 = number2;
	}

	public int add() {
		return number1 + number2;
	}

	public int multiply() {
		return number1 * number2;
	}

	public void doubleValue() {
		this.number1 *= 2;
		this.number2 *= 2;
	}
}
```


### /06-PrimitiveDataTypesAndAlternatives/src/com/in28minutes/primitive/datatypes/BiNumberRunner.java

```java
package com.in28minutes.primitive.datatypes;

public class BiNumberRunner {

	public static void main(String[] args) {
		BiNumber numbers = new BiNumber(2, 3);
		
		System.out.println(numbers.add());//2+3
		System.out.println(numbers.multiply());//2*3
		
		numbers.doubleValue();//Double both numbers 
		
		System.out.println(numbers.getNumber1());//4
		System.out.println(numbers.getNumber2());//6
	}

}
```


### /06-PrimitiveDataTypesAndAlternatives/src/com/in28minutes/primitive/datatypes/MyChar.java

```java
package com.in28minutes.primitive.datatypes;

public class MyChar {

	private char ch;

	public MyChar(char ch) {
		this.ch = ch;
	}

	public boolean isVowel() {
		//'a' e i o u or A E I O U
		if(ch == 'a' || ch == 'A')
			return true;

		if(ch == 'e' || ch == 'E')
			return true;
		
		if(ch == 'i' || ch == 'E')
			return true;
		
		if(ch == 'o' || ch == 'O')
			return true;
		
		if(ch == 'u' || ch == 'U')
			return true;
		
		return false;
	}

	public boolean isDigit() {
		if(ch >= 48 && ch <=57) //between '0' and '9'  
		  return true;
		
		return false;
	}

	public boolean isAlphabet() {
		if(ch >= 97 && ch <=122) //between 'a' and 'z'  
		  return true;

		if(ch >= 65 && ch <=90) //between 'A' and 'Z'  
			  return true;

		return false;
	}

	public boolean isConsonant() {
		//Alphabet and it is not VOWEL
		//! [a , e, i ,o , u]
		if(isAlphabet() && !isVowel()) 
			return true;
		
		return false;
		
	}

	public static void printLowerCaseAlphabets() {
		//'a' to 'z'
		for (char ch = 'a'; ch <= 'z'; ch++) {
			System.out.println(ch);
		}
	}

	public static void printUpperCaseAlphabets() {
		for (char ch = 'A'; ch <= 'Z'; ch++) {
			System.out.println(ch);
		}
		
	}
}
```


### /06-PrimitiveDataTypesAndAlternatives/src/com/in28minutes/primitive/datatypes/MyCharRunner.java

```java
package com.in28minutes.primitive.datatypes;

public class MyCharRunner {

	public static void main(String[] args) {
		MyChar myChar = new MyChar('B');
		System.out.println(myChar.isVowel());
		
		//'a', 'e', 'i', 'o', 'u' and Capitals
		System.out.println(myChar.isDigit());
		System.out.println(myChar.isAlphabet()); //'a' to 'z' or 'A' to 'Z'

		System.out.println(myChar.isConsonant());
		
		MyChar.printLowerCaseAlphabets();
		MyChar.printUpperCaseAlphabets();
	}

}
```


### /06-PrimitiveDataTypesAndAlternatives/src/com/in28minutes/primitive/datatypes/SimpleInterestCalculator.java

```java
package com.in28minutes.primitive.datatypes;

import java.math.BigDecimal;

public class SimpleInterestCalculator {

	BigDecimal principal;

	BigDecimal interest;

	public SimpleInterestCalculator(String principal, String interest) {
		this.principal = new BigDecimal(principal);
		this.interest = new BigDecimal(interest).divide(new BigDecimal(100));
	}

	public BigDecimal calculateTotalValue(int noOfYears) {
		// Total Value = principal + principal * interest * noOfYears;
		BigDecimal noOfYearsBigDecimal = new BigDecimal(noOfYears);
		BigDecimal totalValue = principal.add(principal.multiply(interest).multiply(noOfYearsBigDecimal));
		return totalValue;
	}

}
```


### /06-PrimitiveDataTypesAndAlternatives/src/com/in28minutes/primitive/datatypes/SimpleInterestCalculatorRunner.java

```java
package com.in28minutes.primitive.datatypes;

import java.math.BigDecimal;

public class SimpleInterestCalculatorRunner {

	public static void main(String[] args) {

		SimpleInterestCalculator calculator = 
		        new SimpleInterestCalculator("4500.00", "7.5");
		 BigDecimal totalValue = 
		        calculator.calculateTotalValue(5);// 5 years
		 //6187.50000
		 System.out.println(totalValue);
	}

}
```


# 07-Conditionals

## Steps
- Step 00 - Conditionals with Java - Section Overview
- Step 01 - Introduction to If Else Statement
- Step 02 - Introduction to Nested If Else
- Step 03 - If Else Statement - Puzzles
- Step 04 - If Else Problem - How to get User Input in Java?
- Step 05 - If Else Problem - How to get number 2 and choice from user?
- Step 06 - If Else Problem - Implementing with Nested If Else
- Step 07 - Java Switch Statement - An introduction
- Step 08 - Java Switch Statement - Puzzles - Default, Break and Fall Through
- Step 09 - Java Switch Statement - Exercises - isWeekDay, nameOfMonth, nameOfDay
- Step 10 - Java Ternary Operation - An Introduction
- Step 11 - Conditionals with Java - Conclusion

## Exercises

#### If and Nested If Else - Design a Menu
- Ask User for input
  - Enter two numbers 
  - Choose an Operation
      - add
      - multiply
      - divide 
      - subtract
      - ...
  - Publish Result

```
Enter Number1: 
2

Enter Number2: 
4

1 - Add
2 - Subtract
3 - Divide
4 - Multiply
Choose Operation: 4

Result is - 8
```

#### Switch 
- ```public static boolean isWeekDay(int dayNumber) {``` 
  - input - number of day 0 (Sunday) to 6(Saturday)
  - return if the day is a Week Day.   
- ```public static String determineNameOfMonth(int monthNumber) {```
  - input - number of month 1(January) to 12(December)
  - output - Name of month
- ```public static String determineNameOfDay(int dayNumber) {```
  - input - number of day 0 (Sunday) to 6(Saturday)
  - Return the day of week in text


## Code Examples

### /07-Conditionals/commands.txt

```java
if(true) {
   System.out.println("True");
}
if(false) {
   System.out.println("True");
}
if(i==3) {
   System.out.println("True");
}
if(i<2) {
    System.out.println("True");
}
if(i<=3 || i>=35) {
    System.out.println("True");
}
if(i<=3 && i>=35) {
    System.out.println("True");
}
if (i==3) {
   System.out.println("True");
} else {
   System.out.println("i is not 3");
}
i = 5
if (i==3) {
   System.out.println("True");
} else {
   System.out.println("i is not 3");
}
if(i==1) {
   System.out.println("i");
}
switch (i) {
   case 1 : System.out.println("1");
   case 5 : System.out.println("5");
   default : System.out.println("default");
}
i = 1
switch (i) {
   case 1 : System.out.println("1");
   case 5 : System.out.println("5");
   default : System.out.println("default");
}
switch (i) {
   case 1 : System.out.println("1"); break;
   case 5 : System.out.println("5"); break;
   default : System.out.println("default"); break;
}
boolean isEven;
int i =5;
if(i%2==0) {
  isEven = true;
} else {
  isEven = false;
}
isEven
i = 6
if(i%2==0) {
  isEven = false;
}
if(i%2==0) {
  isEven = true;
} else {
  isEven = false;
}
isEven
isEven = ( i%2==0 ? true : false  )
i = 6
isEven = ( i%2==0 ? true : false  )
i = 7
isEven = ( i%2==0 ? true : false  )
i = 6
String even = ( i%2 ==0 ? "YES" : "NO" );
```


### /07-Conditionals/src/com/in28minutes/ifstatement/examples/IfStatementRunner.java

```java
package com.in28minutes.ifstatement.examples;

public class IfStatementRunner {

	public static void main(String[] args) {
		puzzle5();
	}

	private static void puzzle1() {
		int k = 15;
		if (k > 20) {
			System.out.println(1);
		} else if (k > 10) {
			System.out.println(2);
		} else if (k < 20) {
			System.out.println(3);
		} else {
			System.out.println(4);
		}
		
	}

	private static void puzzle2() {
		int l = 15;

		if (l < 20)
			System.out.println("l<20");//
		if (l > 20)
			System.out.println("l>20");
		else
			System.out.println("Who am I?");//
	}

	
	
	private static void puzzle3() {
		int m = 15;

		if(m>20) 
		    if(m<20)
		System.out.println("m>20");
		    else
		System.out.println("Who am I?");
	}


	private static void puzzle5() {
		int number = 5;
		if(number < 0) 
		    number = number + 10; 
		number++; 
		System.out.println(number);
	}

	private static void basicNestedIfElse() {
		int i = 24;
		// i is 25
		// i is 24
		// i is neither 25 or 24
		if (i == 25) {
			System.out.println("i = 25");
		} else if (i == 24) {
			System.out.println("i = 24");
		} else if (i == 23) {
			System.out.println("i = 23");
		} else {
			System.out.println("i != 24 and i !=25 and i !=23");
		}
	}

}
```


### /07-Conditionals/src/com/in28minutes/ifstatement/examples/MenuRunner.java

```java
package com.in28minutes.ifstatement.examples;

import java.util.Scanner;

public class MenuRunner {
	public static void main(String[] args) {
		// Type obj = new Type(argument);
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter Number1: ");
		int number1 = scanner.nextInt();

		System.out.print("Enter Number2: ");
		int number2 = scanner.nextInt();

		System.out.println("Choices Available are ");
		System.out.println("1 - Add");
		System.out.println("2 - Subtract");
		System.out.println("3 - Divide");
		System.out.println("4 - Multiply");

		System.out.print("Enter Choice: ");
		int choice = scanner.nextInt();

		System.out.println("Your Choices are");
		System.out.println("Number1 " + number1);
		System.out.println("Number2 " + number2);
		System.out.println("Choice " + choice);

		performOperationUsingSwitch(number1, number2, choice);
	}

	private static void performOperationUsingNestedIfElse(int number1, int number2, int choice) {
		if (choice == 1) {
			System.out.println("Result " + (number1 + number2));
		} else if (choice == 2) {
			System.out.println("Result " + (number1 - number2));
		} else if (choice == 3) {
			System.out.println("Result " + (number1 / number2));
		} else if (choice == 4) {
			System.out.println("Result " + (number1 * number2));
		} else {
			System.out.println("Invalid Operation");
		}
	}

	private static void performOperationUsingSwitch(int number1, int number2, int choice) {
		switch (choice) {
		case 1:
			System.out.println("Result " + (number1 + number2));
			break;
		case 2:
			System.out.println("Result " + (number1 - number2));
			break;
		case 3:
			System.out.println("Result " + (number1 / number2));
			break;
		case 4:
			System.out.println("Result " + (number1 * number2));
			break;
		default:
			System.out.println("Invalid Operation");
			break;
		}

	}

}
```


### /07-Conditionals/src/com/in28minutes/ifstatement/examples/SwitchExercisesRunner.java

```java
package com.in28minutes.ifstatement.examples;

public class SwitchExercisesRunner {

	public static void main(String[] args) {
		System.out.println(isWeekDay(5));
	}

	public static boolean isWeekDay(int dayNumber) {
		switch(dayNumber) {
		//case 0 :
		//case 6 : return false;
		case 1 : 
		case 2 :
		case 3 :
		case 4 :
		case 5 : return true;
		}

		return false;
	}
	
	public static String determineNameOfDay(int dayNumber) {
		switch (dayNumber) {
		case 0:
			return "Sunday";
		case 1:
			return "Monday";
		case 2:
			return "Tuesday";
		case 3:
			return "Wednesday";
		case 4:
			return "Thursday";
		case 5:
			return "Friday";
		case 6:
			return "Saturday";
		}

		return "Invalid_day";
	}
}
```


### /07-Conditionals/src/com/in28minutes/ifstatement/examples/SwitchStatementRunner.java

```java
package com.in28minutes.ifstatement.examples;

public class SwitchStatementRunner {
	public static void main(String[] args) {
		puzzle4();
	}

	private static void puzzle1() {
		int number = 2;
		switch (number) {
		case 1:
			System.out.println(1);
		case 2:
			System.out.println(2);
		case 3:
			System.out.println(3);
		default:
			System.out.println("Default");
		}
	}

	private static void puzzle2() {
		int number = 2;
		switch (number) {
		case 1:
			System.out.println(1);
			break;
		case 2:
		case 3:
			System.out.println("Number is 2 or 3");
			break;
		default:
			System.out.println("Default");
			break;
		}
	}

	private static void puzzle3() {
		int number = 10;
		switch (number) {
		case 1:
			System.out.println(1);
			break;
		case 2:
			System.out.println(2);
			break;
		case 3:
			System.out.println(3);
			break;
		default:
			System.out.println("Default");
			break;
		}
	}

	private static void puzzle4() {
		int number = 10;
		switch (number) {
		default:
			System.out.println("Default");
			break;
		case 1:
			System.out.println(1);
			break;
		case 2:
			System.out.println(2);
			break;
		case 3:
			System.out.println(3);
			break;
		}
	}

	private static void puzzle5() {
		long l = 15;
		/*switch(l){
		
		}*/
	}

	private static void puzzle6() {
		int number = 10;
		int i = number * 2;
		switch (number) {
		 //case number>5: System.out.println("number>5");
		}
	}

}
```

# 08-Loops

## Steps
- Step 00 - Java Loops - Section Introduction
- Step 01 - Java For Loop - Syntax and Puzzles
- Step 02 - Java For Loop - Exercises Overview and First Exercise Prime Numbers
- Step 03 - Java For Loop - Exercise - Sum Upto N Numbers and Sum of Divisors
- Step 04 - Java For Loop - Exercise - Print a Number Triangle
- Step 05 - While Loop in Java - An Introduction
- Step 06 - While Loop - Exericises - Cubes and Squares upto limit
- Step 07 - Do While Loop in Java - An Introduction
- Step 08 - Do While Loop in Java - An Example - Cube while user enters positive numbers
- Step 09 - Introduction to Break and Continue
- Step 10 - Selecting Loop in Java - For vs While vs Do While

## Exercises

#### For Loop

Implement MyNumber class with behavior shown in the example below:

```java
MyNumber number = new MyNumber(9);

number.isPrime(); //Is a number Prime? 
//Hint : 5 => true, 7 => true, 11 => true, 6 => false

int sum = number.sumUptoN();//Sum of numbers upto n?
//1 + 2 + 3 + 4 + 5 + 6

int sumOfDivisors = number.sumOfDivisors();

number.printANumberTriangle();
//1
//1 2
//1 2 3
//1 2 3 4 
//1 2 3 4 5
```

#### While
Implement WhileNumberPlayer class with behavior shown in the example below:

```java

WhileNumberPlayer player = new WhileNumberPlayer(30);//limit

player.printSquaresUptoLimit();
//For limit = 30, output would be 1 4 9 16 25

player.printCubesUptoLimit();
//For limit = 30, output would be 1 8 27

```

#### Choosing Loops

Thinking Exercise 
- What would we use for the Menu 
- If we would want to run the Menu again and again?
```
Enter Number1: 
2

Enter Number2: 
4

1 - Add
2 - Subtract
3 - Divide
4 - Multiply
5 - Exit

Choose Operation: 4
Result is 8

Choose Operation: 1
Result is 6

Choose Operation: 5

Thank You!

```

## Code Examples

### /08-Loops/commands.txt

```java
for (int i = 0; i<= 10; i++) {
   System.out.print (i + " ");
}
for (int i = 0; i<= 10; i = i + 2) {
   System.out.print (i + " ");
}
for (int i = 1; i<= 10; i = i + 2) {
   System.out.print (i + " ");
}
for (int i = 11; i<= 10; i = i + 2) {
   System.out.print (i + " ");
}
for (int i = 11; i<= 20;) {
   System.out.print (i + " ");
   i++;
}
for (; i<= 30;i++) {
   System.out.print (i + " ");
}
9 % 2
9 % 3
if (i>2) {
   System.out.println("i>2");
}
int i = 3;
if (i>2) {
   System.out.println("i>2");
}
i = 0
while (i <5) {
   System.out.println(i);
   i++;
}
i
i = 6
while (i < 5) {
   System.out.println(i);
   i++;
}
i = -2
while (i < 5) {
   System.out.println(i);
}
while (i < 5) {
   System.out.println(i);
   i++;
}
i
while (i < 5) {
   System.out.print(i + " ");
   i++;
}
i
i = 1
do {
   System.out.print(i + " ");
   i++;
} while (i<5);
i = 10
while (i < 5) {
   System.out.print(i + " ");
   i++;
}
do {
   System.out.print(i + " ");
   i++;
} while (i<5);
for(i=1;i<=10;i++) {
   if(i==5)
      break;
   System.out.print(i + " ");
}
for(i=1;i<=10;i++) {
   if(i%2==0)
      break;
   System.out.print(i + " ");
}
for(i=1;i<=10;i++) {
   if(i%2==0)
     continue;
   System.out.print(i + " ");
}
for(i=1;i<=10;i++) {
   if(i%2!=0)
     continue;
   System.out.print(i + " ");
}
```


### /08-Loops/src/com/in28minutes/loops/DoWhileRepeatedQuestionRunner.java

```java
package com.in28minutes.loops;

import java.util.Scanner;

public class DoWhileRepeatedQuestionRunner {

	public static void main(String[] args) {

		Scanner scanner = new Scanner(System.in);
		int number = -1;

		do {
			if (number != -1) {
				System.out.println("Cube is " + (number * number * number));
			}
			System.out.print("Enter a number: ");
			number = scanner.nextInt();
		} while (number >= 0);
		System.out.print("Thank You! Have Fun!");
	}

}
```


### /08-Loops/src/com/in28minutes/loops/MyNumber.java

```java
package com.in28minutes.loops;

public class MyNumber {

	private int number;

	public MyNumber(int number) {
		this.number = number;
	}

	public boolean isPrime() {
		// 2 to number-1
		// How can check if a number is divisible by 2?

		if (number < 2) {
			return false;
		}

		for (int i = 2; i <= number - 1; i++) {
			if (number % i == 0) {
				return false;
			}
		}

		return true;
	}

	public int sumUptoN() {
		int sum = 0;

		for (int i = 1; i <= number; i++) {
			sum = sum + i;
		}

		return sum;
	}

	public int sumOfDivisors() {
		// 6 except 1 , 6 => 2,3
		// 2 + 3 + 4 + 5

		int sum = 0;

		for (int i = 2; i <= number - 1; i++) {
			if (number % i == 0) {
				sum = sum + i;
			}
		}

		return sum;
	}

	public void printNumberTriangle() {
		// 1
		// 1 2
		// 1 2 3
		// 1 2 3 4
		// 1 2 3 4 5

		for (int i = 1; i <= number; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print(j + " ");
			}
			System.out.println();
		}

	}

}
```


### /08-Loops/src/com/in28minutes/loops/MyNumberRunner.java

```java
package com.in28minutes.loops;

import com.in28minutes.loops.MyNumber;

public class MyNumberRunner {

	public static void main(String[] args) {
		MyNumber number = new MyNumber(5);
		
		boolean isPrime = number.isPrime();
		System.out.println("isPrime " + isPrime);
		
		int sum = number.sumUptoN();
		System.out.println("sumUptoN " + sum);
		
		int sumOfDivisors = number.sumOfDivisors();
		System.out.println("sumOfDivisors " + sumOfDivisors);
		
		number.printNumberTriangle();
	}

}
```


### /08-Loops/src/com/in28minutes/loops/WhileNumberPlayer.java

```java
package com.in28minutes.loops;

public class WhileNumberPlayer {

	private int limit;

	public WhileNumberPlayer(int limit) {
		this.limit = limit;
	}

	// For limit = 30, output would be 1 4 9 16 25
	public void printSquaresUptoLimit() {
		int i = 1;
		while (i * i < limit) {
			System.out.print(i * i + " ");
			i++;
		}
		System.out.println();
	}

	// For limit = 27, output would be 1 8 27
	public void printCubesUptoLimit() {
		int i = 1;
		while (i * i * i <= limit) {
			System.out.print(i * i * i + " ");
			i++;
		}
		System.out.println();
	}

}
```


### /08-Loops/src/com/in28minutes/loops/WhileNumberPlayerRunner.java

```java
package com.in28minutes.loops;

public class WhileNumberPlayerRunner {
	public static void main(String[] args) {
		WhileNumberPlayer player = new WhileNumberPlayer(27);
		player.printSquaresUptoLimit();
		player.printCubesUptoLimit();
	}
}
```


# 09-ReferenceTypes

## Steps
- Step 00 - Java Reference Types - Section Introduction
- Step 01 - Reference Types - How are they stored in Memory?
- Step 02 - Java Reference Types - Puzzles
- Step 03 - String class - Introduction and Exercise - Print each word and char on a new line
- Step 04 - String class - Exercise Solution and Some More Important Methods
- Step 05 - Understanding String is Immutable and String Concat, Upper Case, Lower Case, Trim methods
- Step 06 - String Concatenation and Join, Replace Methods
- Step 07 - Java String Alternatives - StringBuffer and StringBuilder
- Step 08 - Java Wrapper Classes - An Introduction - Why and What?
- Step 09 - Java Wrapper Classes - Creation - Constructor and valueOf 
- Step 10 - Java Wrapper Classes - Auto Boxing and a Few Wrapper Constants - SIZE, BYTES, MAX_VALUE and MIN_VALUE
- Step 11 - Java Dates - Introduction to LocalDate, LocalTime and LocalDateTime
- Step 12 - Java Dates - Exploring LocalDate - Creation and Methods to play with Date
- Step 13 - Java Dates - Exploring LocalDate - Comparing Dates and Creating Specific Dates
- Step 14 - Java Reference Types - Conclusion

## Exercises

#### String
- Take a piece of Text into a String. 
   - Print each character in the text on a seperate line
   - Print each word in the text on a seperate line


## Code Examples

### /09-ReferenceTypes/commands.txt

```java
class Planet {
}
Planet jupiter = new Planet();
int i = 5;
class Animal {
    int id;
    Animal(int id) {
       this.id = id;
    }
}
Animal nothing;
nothing = cat
nothing.id = 10
cat.id
nothing = dog
nothing.id
int j = i;
j = 6
i
i == j
j = 5
i == j
Animal dog = new Animal(12);
Animal cat = new Animal(10);
Animal ref = cat;
Animal dog2 = new Animal(12);
cat == dog
cat == ref
dog == dog2
1
2
12.34
"Test".length()
BigDecimal bd = new BigDecimal("1.0");
str.charAt(0)
str.charAt(2)
str.charAt(3)
String biggerString = "This is a lot of text";
str.substring(5)
biggerString.substring(5)
biggerString.substring(5,13)
str.charAt(13)
biggerString.charAt(13)
biggerString.charAt(456)
someString.length()
someString.charAt(5)
for(int i= 0; i<someString.length(); i++) {
    System.out.println(someString.charAt(i));
}
someString.indexOf("lot")
someString.charAt(10)
someString.charAt('i')
someString.indexOf('i')
someString.lastIndexOf('i')
someString.contains("text")
String someString = "This is a lot of text again";
someString.startsWith("This")
someString.startsWith("jfsdklfj")
someString.endsWith("jfsdklfj")
someString.endsWith("in")
someString.endsWith("ain")
someString.endsWith("again")
someString.endsWith("againfsda")
someString.isEmpty()
"fjsadlkfj".isEmpty()
"".isEmpty()
"true".equals("true")
"value".equals("value")
str.equals("value")
str.equals("VAlue")
str.equalsIgnoreCase("VAlue")
str.concat("is awesome");
str
String anotherString = str.concat(" is awesome");
str
anotherString
String string2 = anotherString.concat(".");
str
anotherString
string2
str.toUpperCase()
str.toLowerCase()
str2.trim()
String str2 = "  in28Minutes is awesome.   ";
str2.trim()
1 + 2
"1" + "2"
"1" + 2
"1" + 23
1 + 23
1 + 2 + "3"
"1" + 2 + 3
System.out.println("Value is " + 20)
System.out.println("Value is " + 20 + 20)
System.out.println("Value is " + (20 + 20))
String.join(",", "2", "3", "4")
String.join(",", "A", "B","C")
String.join(",", "A")
String.join(",", "A", "B")
"abcd".replace('a', 'z');
"abcd".replace("ab", "xyz");
String str = "jdsfja ";
"123" + "123" + "1234" + "123456"
sb.append(" 123")
sb
sb
sb.setCharAt(1,'e')
sb
StringBuilder sb = new StringBuilder("test");
Integer integer1 = new Integer("5234");
Integer integer2 = new Integer("5234");
Integer i1 = new Integer(5);
Integer i2 = new Integer(5);
Integer i3 = Integer.valueOf(5);
Integer i4 = Integer.valueOf(5);
i1 == i2
i3 == i4
Integer integer = Integer.valueOf("4567");
int i = integer.intValue();
Float f = Float.valueOf("12.45");
f.floatValue()
f.intValue()
Integer eight = Integer.valueOf(8);
Integer.toBinaryString(eight);
Integer.toHexString(eight);
Integer eightyEight = Integer.valueOf(88);
Integer.toHexString(eightyEight);
seven++
seven
seven == sevenAgain
Integer seven = 7;
Integer sevenAgain = 7;
seven == sevenAgain
Integer.MAX_VALUE
Integer.MIN_VALUE
Integer.SIZE
Integer.BYTES
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.*;
today.getYear()
today.getDayOfWeek()
today.getDayOfMonth()
today.getDayOfYear()
today.getMonth()
today.getMonthValue()
today.isLeapYear()
today.lengthOfYear()
today.lengthOfMonth()
today.plusDays(100)
today.plusMonths(100)
today.plusYears(100)
today.minusYears(100)
LocalDate hundredYearsBefore = today.minusYears(100);
today
LocalDateTime now = LocalDateTime.now();
LocalDate today = LocalDate.now();
LocalDate yesterady = LocalDate.of(2018, 01, 31);
LocalDate yesterday = LocalDate.of(2018, 01, 31);
today
yesterday
today.withYear(2016)
today.withDayOfMonth(20)
today.withMonth(3)
today.withDayOfYear(120)
today.isBefore(yesterday)
today.isAfter(yesterday)
```


# 10-ArraysAndArrayList


## Exercises

#### Student Class

```java
Student student = new Student (name, list of marks);
int number = student.getNumberOfMarks();
int sum = student.getTotalSumOfMarks();
int maximumMark = student.getMaximumMark();
int minimumMark = student.getMinimumMark();
BigDecimal average = student.getAverageMarks();
student.addNewMark(35);
student.removeMarkAtIndex(5);
```

#### String Arrays
- Create a string array with days of the week
   - "Sunday", "Monday", "Tuesday", "Wednesday"
   - "Thursday", "Friday", "Saturday"
- Find the day with most number of letters in it 
   - Longest String
- Print days of the week backwards


## Code Examples

### /10-ArraysAndArrayList/src/com/in28minutes/arrays/StringRunner.java

```java
package com.in28minutes.arrays;

public class StringRunner {

	public static void main(String[] args) {

		String[] daysOfWeek = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };

		String dayWithMostCharacters = "";

		for (String day : daysOfWeek) {
			if (day.length() > dayWithMostCharacters.length()) {
				dayWithMostCharacters = day;
			}
		}

		System.out.println("Day with Most number of characters " + dayWithMostCharacters);

		for (int i = daysOfWeek.length - 1; i >= 0; i--) {
			System.out.println(daysOfWeek[i]);
		}

	}

}
```


### /10-ArraysAndArrayList/src/com/in28minutes/arrays/Student.java

```java
package com.in28minutes.arrays;

import java.math.BigDecimal;
import java.math.RoundingMode;
import java.util.ArrayList;
import java.util.Collections;

public class Student {

	private String name;
	private ArrayList<Integer> marks = new ArrayList<Integer>();

	public Student(String name, int... marks) {
		this.name = name;

		for (int mark : marks) {
			this.marks.add(mark);
		}
	}

	public int getNumberOfMarks() {
		return marks.size();
	}

	public int getTotalSumOfMarks() {
		int sum = 0;
		for (int mark : marks) {
			sum += mark;
		}
		return sum;
	}

	public int getMaximumMark() {
		return Collections.max(marks);
	}

	public int getMinimumMark() {
		return Collections.min(marks);
	}

	public BigDecimal getAverageMarks() {
		int sum = getTotalSumOfMarks();
		int number = getNumberOfMarks();

		return new BigDecimal(sum).divide(new BigDecimal(number), 3, RoundingMode.UP);
	}

	public String toString() {
		return name + marks;
	}

	public void addNewMark(int mark) {
		marks.add(mark);
	}

	public void removeMarkAtIndex(int index) {
		marks.remove(index);
		
	}
}
```


### /10-ArraysAndArrayList/src/com/in28minutes/arrays/StudentRunner.java

```java
package com.in28minutes.arrays;

import java.math.BigDecimal;

public class StudentRunner {

	public static void main(String[] args) {
				
		Student student = new Student("Ranga", 97, 98, 100);
				
		int number = student.getNumberOfMarks();
		System.out.println("number of marks : " + number);
		
		int sum = student.getTotalSumOfMarks();
		System.out.println("sum of marks : " + sum);
		
		int maximumMark = student.getMaximumMark();
		System.out.println("maximum of marks : " + maximumMark);
		
		int minimumMark = student.getMinimumMark();
		System.out.println("minimum of marks : " + minimumMark);
		
		BigDecimal average = student.getAverageMarks();
		System.out.println("average : " + average);
		
		System.out.println(student);
		
		student.addNewMark(35);
		
		System.out.println(student);

		student.removeMarkAtIndex(1);
		
		System.out.println(student);
		
	}

}
```


# 11-ObjectOrientedProgrammingAgain

## Steps

- Step 00 - Object Oriented Programming - Level 2 - Section Introduction
- Step 01 - Basics of Designing a Class - Class, Object, State and Behavior
- Step 02 - OOPS Example - Fan Class - Deciding State and Constructors
- Step 03 - OOPS Example - Fan Class - Deciding Behavior with Methods
- Step 04 - OOPS Exercise - Rectangle Class
- Step 05 - Understanding Object Composition with Customer Address Example
- Step 06 - Understanding Object Composition - An Exercise - Books and Reviews
- Step 07 - Understanding Inheritance - Why do we need it?
- Step 08 - Object is at top of Inheritance Hierarchy
- Step 09 - Inheritance and Overriding - with toString() method
- Step 10 - Java Inheritance - Exercise - Student and Employee Classes
- Step 11 - Java Inheritance - Default Constructors and super() method call
- Step 12 - Java Inheritance - Puzzles - Multiple Inheritance, Reference Variables and instanceof

- Step 13 - Java Abstract Class - Introductio
- Step 14 - Java Abstract Class - First Example - Creating Recipes with Template Method
- Step 15 - Java Abstract Class - Puzzles
- Step 16 - Java Interface - Example 1 - Gaming Console - How to think about Intefaces? 
- Step 17 - Java Interface - Example 2 - Complex Algorithm - API defined by external team
- Step 18 - Java Interface - Puzzles - Unimplemented methods, Abstract Classes, Variables, Default Methods and more
- Step 19 - Java Interface vs Abstract Class - A Comparison
- Step 20 - Java Interface Flyable and Abstract Class Animal - An Exercise
- Step 21 - Polymorphism - An introduction

## Exercises

#### Creating a simple class
- public class Rectangle
  - length, width;
  - What constructors?
  - What Operations?

#### Object Composition - Book and Reviews

Object Composition
- Book - id, name, author
  - Reviews - id, description, rating

```java 
 Book book = 
    new Book(123, "Object Oriented Programming with Java", 
          "Ranga");
 book.addReview(
    new Review(10, "Great Book", 5));
 book.addReview(
    new Review(101, "Awesome", 5);

 System.out.println(book);
 ```

#### Inheritance

Setup an Inheritance Hierarchy and implement toString in Employee class
- Person
   - name,phone,email;
- Student 
  - college, class
- Employee 
  - title, employer, employeeGrade, salary
  - toString (print all values including those of Person)

#### Interface and Abstract Class

interface Flyable 
- void fly();
- Bird "with wings"
- Aeroplane "with fuel"
- Flyable flyingObjects = {new Bird(), new Aeroplane()};
- Loop and invoke fly method

abstract class Animal
- void bark()
- Dog "Bow Bow"
- Cat "Meow Meow"
- Animal[] animals = {new Cat(), new Dog()};
- Loop and invoke bark method

## Code Examples

### /commands.txt

```java
class Pet extends Animal {
     public void groom() {
        System.out.println("Groom");
     }
}
dog.toString()
dog.groom()
Pet pet = new Dog();
pet.groom()
pet instanceof Pet
pet instanceof Dog
pet instanceof Animal
pet instanceof Object
animal instanceof Pet
animal instanceof Dog
animal instanceof Object
class Animal {
   public void bark() {
       System.out.println("TEst");
   }
}
animal.bark()
abstract class AbstractAnimal {
    abstract public void bark();
}
class Dog extends AbstractAnimal {
    public void bark() {
       System.out.println("Bow Bow");
    }
}
Dog dog = new Dog();
dog.bark()
abstract class AbstractTest {
}
abstract class Algorithm1 extends AbstractAlgorithm {
}
abstract class AbstractAlgorithm {
     private int stepCount;
     public int getStepCount() {
          return stepCount();
     }
}
class Implementation implements Interface2 {
   public void method2() { }
   public void method1() { }
}
abstract class ImplementationAbstract implements Interface2 {
   public void method1() { }
}
interface Interface3 {
  int test = 5;
}
interface Interface4 {
    default void print() {
       System.out.println("default");
    }
}
class Test implements Interface4 {
}
test.print()
class Test1 implements Interface4 {
   public void print() {
      System.out.println("override");
   }
}
Test1 test = new Test1();
test.print()
interface Interface1 {
 void method1();
}
interface Interface2 {
 void method2();
}
```


### /src/com/in28minutes/oops/level2/AbstractRecipe.java

```java
package com.in28minutes.oops.level2;

public abstract class AbstractRecipe {
	
	public void execute() {
		getReady();
		doTheDish();
		cleanup();
	}
	
	abstract void getReady();
	abstract void doTheDish();
	abstract void cleanup();
}
```


### /src/com/in28minutes/oops/level2/Address.java

```java
package com.in28minutes.oops.level2;

public class Address {
	private String line1;
	private String city;
	private String zip;
	
	//creation
	public Address(String line1, String city, String zip) {
		super();
		this.line1 = line1;
		this.city = city;
		this.zip = zip;
	}
	
	public String toString() {
		return line1 + " " + city + " " + zip;
				 
	}
	
}
```


### /src/com/in28minutes/oops/level2/Book.java

```java
package com.in28minutes.oops.level2;

import java.util.ArrayList;

public class Book {

	private int id;
	private String name;
	private String author;
	private ArrayList<Review> reviews = new ArrayList<>();

	public Book(int id, String name, String author) {
		this.id = id;
		this.name = name;
		this.author = author;
	}

	public void addReview(Review review) {
		this.reviews.add(review);
	}
	
	public String toString() {
		return String.format("id =%d name = %s author = %s Reviews = [%s]",
				id, name, author, reviews);
	}

}
```


### /src/com/in28minutes/oops/level2/BookRunner.java

```java
package com.in28minutes.oops.level2;

public class BookRunner {

	public static void main(String[] args) {
		Book book = new Book(123, "Object Oriented Programming with Java",
				"Ranga");
		book.addReview(new Review(10, "Great Book", 5));
		book.addReview(new Review(101, "Awesome", 5));

		System.out.println(book);

	}

}
```


### /src/com/in28minutes/oops/level2/Customer.java

```java
package com.in28minutes.oops.level2;

public class Customer {

	//state
	private String name;
	private Address homeAddress;
	private Address workAddress;
	
	//creating
	public Customer(String name, Address homeAddress) {
		this.name = name;
		this.homeAddress = homeAddress;
	}

	//operations
	public Address getHomeAddress() {
		return homeAddress;
	}

	public void setHomeAddress(Address homeAddress) {
		this.homeAddress = homeAddress;
	}

	public Address getWorkAddress() {
		return workAddress;
	}

	public void setWorkAddress(Address workAddress) {
		this.workAddress = workAddress;
	}
		
	public String toString() {
		return String.format("name - [%s] home address - [%s] work address - [%s])"
				, name, homeAddress, workAddress);
	}
	
}
```


### /src/com/in28minutes/oops/level2/CustomerRunner.java

```java
package com.in28minutes.oops.level2;

public class CustomerRunner {

	public static void main(String[] args) {
		Address homeAddress = new Address("line 1", "Hyderabad", "500035");
		Customer customer = new Customer("Ranga", homeAddress);
		System.out.println(customer);
		
		Address workAddress = new Address("line 1 for work", "Hyderabad", "500078");
		customer.setWorkAddress(workAddress);
		
		System.out.println(customer);
	}	
}
```


### /src/com/in28minutes/oops/level2/Fan.java

```java
package com.in28minutes.oops.level2;

public class Fan {
	
	//state
	private String make;
	private double radius;
	private String color;

	private boolean isOn;
	private byte speed; //0 to 5
	
	//creation
	public Fan(String make, double radius, String color) {
		this.make = make;
		this.radius = radius;
		this.color = color;
	}
	
	public void switchOn() {
		this.isOn = true;
		setSpeed((byte)5);
	}

	public void switchOff() {
		this.isOn = false;
		setSpeed((byte)0);
	}

	public void setSpeed(byte speed) {
		this.speed = speed;
	}
	
	//print the state
	public String toString() {
		return String.format("make - %s, radius - %f , color - %s , isOn - %b , speed - %d", 
				make, radius, color, isOn, speed);
	}
	
}
```


### /src/com/in28minutes/oops/level2/FanRunner.java

```java
package com.in28minutes.oops.level2;

public class FanRunner {
	public static void main(String[] args) {
		Fan fan = new Fan("Manufacturer 1", 0.34567, "GREEN");
		fan.switchOn();
		System.out.println(fan);
		fan.setSpeed((byte)3);
		System.out.println(fan);
		fan.switchOff();
		System.out.println(fan);
	}
}
```


### /src/com/in28minutes/oops/level2/inheritance/AnimalRunner.java

```java
package com.in28minutes.oops.level2.inheritance;

abstract class Animal {
	abstract void bark();
}

class Dog extends Animal {
	public void bark() {
		System.out.println("Bow Bow");
	}
}

class Cat extends Animal {
	public void bark() {
		System.out.println("Meow Meow");
	}
}

public class AnimalRunner {
	public static void main(String[] args) {
		Animal[] animals = {new Cat(), new Dog()};
		for(Animal animal:animals) {
			animal.bark();
		}

	}

}
```


### /src/com/in28minutes/oops/level2/inheritance/Employee.java

```java
package com.in28minutes.oops.level2.inheritance;

import java.math.BigDecimal;

public class Employee extends Person {
	private String title;
	private String employerName;
	private char employeeGrade;
	private BigDecimal salary;
	
	public Employee(String name, String title) {
		super(name);
		this.title = title;
		System.out.println("Employee Constructor");
	}

	public String getTitle() {
		return title;
	}

	public void setTitle(String title) {
		this.title = title;
	}

	public String getEmployerName() {
		return employerName;
	}

	public void setEmployerName(String employerName) {
		this.employerName = employerName;
	}

	public char getEmployeeGrade() {
		return employeeGrade;
	}

	public void setEmployeeGrade(char employeeGrade) {
		this.employeeGrade = employeeGrade;
	}

	public BigDecimal getSalary() {
		return salary;
	}

	public void setSalary(BigDecimal salary) {
		this.salary = salary;
	}

	public String toString() {
        return super.toString() + "#" + title + "#" + employerName + "#" + employeeGrade;
    }

}
```


### /src/com/in28minutes/oops/level2/inheritance/Person.java

```java
package com.in28minutes.oops.level2.inheritance;

public class Person extends Object{
	private String name;
	private String email;
	private String phoneNumber;
		
	public Person(String name) {
		System.out.println("Person Constructor");
		this.name = name;
	}
	
	public String getName() {
		return name;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}

	public String getPhoneNumber() {
		return phoneNumber;
	}

	public void setPhoneNumber(String phoneNumber) {
		this.phoneNumber = phoneNumber;
	}
	
	public String toString() {
        return name + "#" + email + "#" + phoneNumber;
    }
}
```


### /src/com/in28minutes/oops/level2/inheritance/Student.java

```java
package com.in28minutes.oops.level2.inheritance;

public class Student extends Person {
	private String collegeName;
	private int year;

	public Student(String name, String collegeName) {
		super(name);
		this.collegeName = collegeName;
	}
	
	public String getCollegeName() {
		return collegeName;
	}

	public void setCollegeName(String collegeName) {
		this.collegeName = collegeName;
	}

	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

}
```


### /src/com/in28minutes/oops/level2/inheritance/StudentRunner.java

```java
package com.in28minutes.oops.level2.inheritance;

public class StudentRunner {

	public static void main(String[] args) {
		
		//Student student = new Student();
		//student.setName("Ranga");
		//student.setEmail("in28minutes@gmail.com");
		
		/*
		Person person = new Person();
		person.setName("Ranga");
		person.setEmail("ranga@in28minutes.com");
		person.setPhoneNumber("123-456-7890");
		String value = person.toString();
		System.out.println(value);
		System.out.println(person);
		*/
		
		Employee employee = new Employee("Ranga", "Programmer Analyst");
		//employee.setName("Ranga");
		employee.setEmail("ranga@in28minutes.com");
		employee.setPhoneNumber("123-456-7890");
		employee.setEmployeeGrade('A');
		employee.setTitle("Programmer Analyst");
		
		System.out.print(employee);
		
	}
}
```


### /src/com/in28minutes/oops/level2/inheritance/StudentWithoutInheritance.java

```java
package com.in28minutes.oops.level2.inheritance;

public class StudentWithoutInheritance {
	private String name;
	private String email;
	private String phoneNumber;
	
	private String college;
	private int year;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}

	public String getPhoneNumber() {
		return phoneNumber;
	}

	public void setPhoneNumber(String phoneNumber) {
		this.phoneNumber = phoneNumber;
	}

	public String getCollege() {
		return college;
	}

	public void setCollege(String college) {
		this.college = college;
	}

	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

	
	
}
```


### /src/com/in28minutes/oops/level2/interfaces/ChessGame.java

```java
package com.in28minutes.oops.level2.interfaces;

public class ChessGame implements GamingConsole{

	@Override
	public void up() {
		System.out.println("Move piece up");
	}

	@Override
	public void down() {
		System.out.println("Move piece down");
	}

	@Override
	public void left() {
		System.out.println("Move piece left");
	}

	@Override
	public void right() {
		System.out.println("Move piece right");
	}
	
}
```


### /src/com/in28minutes/oops/level2/interfaces/ComplexAlgorithm.java

```java
package com.in28minutes.oops.level2.interfaces;

public interface ComplexAlgorithm {
	int complexAlgorithm(int number1, int number2);
}
```


### /src/com/in28minutes/oops/level2/interfaces/DummyAlgorithm.java

```java
package com.in28minutes.oops.level2.interfaces;

public class DummyAlgorithm implements ComplexAlgorithm{

	@Override
	public int complexAlgorithm(int number1, int number2) {
		return number1 + number2;
	}

}
```


### /src/com/in28minutes/oops/level2/interfaces/FlyableRunner.java

```java
package com.in28minutes.oops.level2.interfaces;

interface Flyable{
	void fly();
}

class Bird implements Flyable{

	@Override
	public void fly() {
		System.out.println("with wings");
	}
	
}

class Aeroplane implements Flyable{

	@Override
	public void fly() {
		System.out.println("with fuel");
	}
	
}

public class FlyableRunner {

	public static void main(String[] args) {
		Flyable[] flyingObjects = { new Bird(), new Aeroplane()};
		for(Flyable object : flyingObjects) {
			object.fly();
		}
	}

}
```


### /src/com/in28minutes/oops/level2/interfaces/GameRunner.java

```java
package com.in28minutes.oops.level2.interfaces;

public class GameRunner {

	public static void main(String[] args) {
		GamingConsole[] games = {new MarioGame(), new ChessGame()};
		
		for(GamingConsole game:games) {
			game.up();
			game.down();
			game.left();
			game.right();
		}

	}

}
```


### /src/com/in28minutes/oops/level2/interfaces/GamingConsole.java

```java
package com.in28minutes.oops.level2.interfaces;

public interface GamingConsole {
	public void up();
	public void down();
	public void left();
	public void right();
}
```


### /src/com/in28minutes/oops/level2/interfaces/MarioGame.java

```java
package com.in28minutes.oops.level2.interfaces;

public class MarioGame implements GamingConsole{

	@Override
	public void up() {
		System.out.println("Jump");
	}

	@Override
	public void down() {
		System.out.println("Goes into a hole");
	}

	@Override
	public void left() {
	}

	@Override
	public void right() {
		System.out.println("Go Forward");
	}
	
}
```


### /src/com/in28minutes/oops/level2/interfaces/Project.java

```java
package com.in28minutes.oops.level2.interfaces;

public class Project {

	interface Test {
		void nothing();

		default void nothing1() {

		}

	}

	class Class1 implements Test {

		@Override
		public void nothing() {
			// TODO Auto-generated method stub

		}

	}

	class Class2 implements Test {

		@Override
		public void nothing() {
			// TODO Auto-generated method stub

		}

	}

	public static void main(String[] args) {
		ComplexAlgorithm algorithm = new RealAlgorithm();
		System.out.println(algorithm.complexAlgorithm(10, 20));
	}

}
```


### /src/com/in28minutes/oops/level2/interfaces/RealAlgorithm.java

```java
package com.in28minutes.oops.level2.interfaces;

public class RealAlgorithm implements ComplexAlgorithm{

	@Override
	public int complexAlgorithm(int number1, int number2) {
		return number1 * number2;
	}

}
```


### /src/com/in28minutes/oops/level2/Recipe1.java

```java
package com.in28minutes.oops.level2;

public class Recipe1 extends AbstractRecipe{

	@Override
	void getReady() {
		System.out.println("Get the raw materials");
		System.out.println("Get the utensils");
	}

	@Override
	void doTheDish() {
		System.out.println("do the dish");
	}

	@Override
	void cleanup() {
		System.out.println("Cleanup the utensils");		
	}

}
```


### /src/com/in28minutes/oops/level2/RecipeRunner.java

```java
package com.in28minutes.oops.level2;

public class RecipeRunner {

	public static void main(String[] args) {
		Recipe1 recipe = new Recipe1();
		recipe.execute();

		RecipeWithMicrowave recipeWithMicrowave = new RecipeWithMicrowave();
		recipeWithMicrowave.execute();

	}

}
```


### /src/com/in28minutes/oops/level2/RecipeWithMicrowave.java

```java
package com.in28minutes.oops.level2;

public class RecipeWithMicrowave extends AbstractRecipe{

	@Override
	void getReady() {
		System.out.println("Get the raw materials");
		System.out.println("Switch on the microwave");
	}

	@Override
	void doTheDish() {
		System.out.println("get stuff ready");
		System.out.println("Put it in the microwave");
	}

	@Override
	void cleanup() {
		System.out.println("Cleanup the utensils");
		System.out.println("Switch off the microwave");
	}

}
```


### /src/com/in28minutes/oops/level2/Rectangle.java

```java
package com.in28minutes.oops.level2;

public class Rectangle {

	//state
	private int length;
	private int width;
	
	//creation
	public Rectangle(int length, int width) {
		this.length = length;
		this.width = width;
	}


	//operations
	public int getLength() {
		return length;
	}

	public void setLength(int length) {
		this.length = length;
	}

	public int getWidth() {
		return width;
	}

	public void setWidth(int width) {
		this.width = width;
	}
		
	public int area() {
		return length * width;
	}
	
	public int perimeter() {
		return 2 * (length + width);
	}
	
	public String toString() {
		return String.format("length - %d width - %d area - %d perimeter - %d", 
				length, width, area(), perimeter());
	}
}
```


### /src/com/in28minutes/oops/level2/RectangleRunner.java

```java
package com.in28minutes.oops.level2;

public class RectangleRunner {

	public static void main(String[] args) {
		Rectangle rectangle = new Rectangle(12, 23);
		System.out.println(rectangle);
		rectangle.setWidth(25);
		System.out.println(rectangle);
	}

}
```


### /src/com/in28minutes/oops/level2/Review.java

```java
package com.in28minutes.oops.level2;

public class Review {

	private int id;
	private String description;
	private int rating;

	public Review(int id, String description, int rating) {
		this.id = id;
		this.description = description;
		this.rating = rating;
	}
	
	public String toString() {
		return id + " " + description + " " + rating;
	}

}
```


# 12-Collections

## Steps
- Step 01 - Java Collections - Section Overview with Need For Collections
- Step 02 - List Interface - Introduction - Position is King
- Step 03 - List Inteface - Immutability and Introduction of Implementations - ArrayList, LinkedList and Vector
- Step 04 - List Inteface Implementations - ArrayList vs LinkedList
- Step 05 - List Inteface Implementations - ArrayList vs Vector
- Step 06 - List Inteface - Methods to add, remove and change elements and lists 
- Step 07 - List and ArrayList - Iterating around elements
- Step 08 - List and ArrayList - Choosing iteration approach for printing and deleting elements
- Step 09 - List and ArrayList - Puzzles - Type Safety and Removing Integers
- Step 10 - List and ArrayList - Sorting - Introduction to Collections sort static method
- Step 11 - List and ArrayList - Sorting - Implementing Comparable Inteface in Student Class
- Step 12 - List and ArrayList - Sorting - Providing Flexibility by implementing Comparator interface
- Step 13 - List and ArrayList - A Summary
- Step 14 - Set Interface - Introduction - No Duplication 
- Step 15 - Understanding Data Structures - Array, LinkedList and Hashing
- Step 16 - Understanding Data Structures - Tree - Sorted Order
- Step 17 - Set Interface - Hands on - HashSet, LinkedHashSet and TreeSet
- Step 18 - Set Interface - Exercise - Find Unique Characters in a List
- Step 19 - TreeSet - Methods from NavigableSet - floor,lower,upper, subSet, head and tailSet
- Step 20 - Queue Interface - Process Elements in Order
- Step 21 - Introduction to PriorityQueue - Basic Methods and Customized Priority
- Step 22 - Map Interface - An Introduction - Key and Value
- Step 23 - Map Interface - Implementations - HashMap, HashTable, LinkedHashMap and TreeMap
- Step 24 - Map Interface - Basic Operations
- Step 25 - Map Interface - Comparison - HashMap vs LinkedHashMap vs TreeMap
- Step 26 - Map Interface - Exercise - Count occurances of characters and words in a piece of text
- Step 27 - TreeMap - Methods from NavigableMap - floorKey, higherKey, firstEntry, subMap and more
- Step 28 - Java Collections - Conclusion with Three Tips

## Exercises

#### Set Interface
- Find unique characters in a list of characters
   - In Insertion Order
   - In Sort Order

#### Map Interface
- Find number of occurances of each character and word in a piece of text.  

## Code Examples

### /12-Collections/commands.txt

```java
words.size()
words.isEmpty()
words.get(0)
words.contains("Dog");
words.contains("Cat");
words.indexOf("Cat")
words
words.indexOf("Dog")
words.add("Dog")
List<String> wordsLinkedList = new LinkedList<String>(words);
List<String> wordsVector = new Vector<String>(words);
wordsArrayList.add("Dog")
wordsArrayList
wordsArrayList.add("Elephant")
wordsArrayList.add(2, "Ball")
wordsArrayList
wordsArrayList.add("Ball")
wordsArrayList
List<String> newList = List.of("Yak","Zebra");
wordsArrayList.addAll(newList)
wordsArrayList
wordsArrayList.set(6, "Fish")
wordsArrayList
wordsArrayList.remove(2)
wordsArrayList
wordsArrayList.remove("Dog")
wordsArrayList
wordsArrayList.remove("Dog")
for(int i=0; i < words.size(); i++) {
     System.out.println(words.get(i));
}
for(String word:words) {
     System.out.println(word);
}
Iterator wordsIterator = words.iterator();
while(wordsIterator.hasNext()) {
      System.out.println(wordsIterator.next());
}
List<String> wordsArrayList = new ArrayList<String>(words);
for(String word:words) {
   if(word.endsWith("at")) {
        words.remove(word);
   }
}
for(String word:wordsArrayList) {
   if(word.endsWith("at")) {
        wordsArrayList.remove(word);
   }
}
wordsArrayList
for(String word:words) {
   if(word.endsWith("at"))
      System.out.println(word);
}
for(String word:wordsAl) {
   if(word.endsWith("at")) {
        words.remove(word);
   }
}
for(String word:wordsAl) {
   if(word.endsWith("at")) {
        wordsAl.remove(word);
   }
}
wordsAl
List<String> words = List.of("Apple", "Bat" , "Cat");
List<String> wordsAl = new ArrayList<>(words);
Iterator<String> iterator = wordsAl.iterator();
while(iterator.hasNext()) {
     if(iterator.next().endsWith("at")) {
          iterator.remove();
     }
}
wordsAl
List value = List.of("A", 'A' , 1, 1.0);
value.get(2)
value.get(2) instanceof Integer
value.get(1) instanceof Character
value.get(3) instanceof Double
numbers.indexOf(101);
numbersAl.indexOf(101)
numbersAl.remove(101);
numbersAl.remove(101)
numbersAl.remove(Integer.valueOf(101))
numbersAl
List<Integer> numbersAl = new ArrayList<>(numbers);
Collections.sort(numbersAl);
numbersAl
set.add("Apple");
Set<String> hashset = new HashSet<>(set);
hashset.add("Apple")
hashset
Set<String> set = Set.of("A", "Z","D", "C", "B");
hashSet.add("A")
hashSet.add("B")
hashSet
hashSet.add("C")
hashSet
hashSet.add("CA")
hashSet
hashSet.add("CAfsadfa")
hashSet
treeSet.add("Cat")
treeSet.add("Bat")
treeSet.add("Apple")
treeSet
hashSet.add("Cat");
hashSet.add("Bat");
hashSet.add("Apple");
hashSet
hashSet.add("Dog");
hashSet
hashSet.add("Elephant");
hashSet.add(5);
hashSet.add(4);
hashSet.add(3);
hashSet.add(2);
hashSet.add(1);
hashSet
Set<Integer> hashSet = new HashSet<>();
hashSet.add(589789);
hashSet.add(58978);
hashSet.add(5897);
hashSet.add(589);
hashSet.add(58);
hashSet.add(5);
hashSet
Set<Integer> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add(589789);
linkedHashSet.add(58978);
linkedHashSet.add(5897);
linkedHashSet.add(589);
linkedHashSet.add(58);
linkedHashSet.add(5);
linkedHashSet
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(584567);
treeSet.add(58456);
treeSet.add(5845);
treeSet.add(584);
treeSet.add(58);
treeSet.add(5);
treeSet
numbers.add(765432);
numbers.add(76543);
numbers.add(7654);
numbers.add(765);
numbers.add(76);
numbers
numbers.add(765432);
numbers.add(76543);
numbers.add(7654);
numbers.add(765);
numbers.add(76);
numbers
numbers.add(765789);
numbers
numbers.add(76)
numbers
numbers.add(765432);
numbers.add(76543);
numbers.add(7654);
numbers.add(765);
numbers.add(76);
numbers
numbers.add(76)
List<Character> characters = List.of('A','Z','A', 'B', 'Z','F');
TreeSet<Integer> numbers = new TreeSet<>(Set.of(65,54,34,12,99));
numbers.floor(40)
numbers.floor(34)
numbers.lower(34)
numbers.ceiling(34)
numbers.ceiling(36)
numbers.higher(34)
numbers
numbers.subSet(20,80)
numbers.subSet(34,54)
numbers.subSet(34,65)
numbers.subSet(34,true,65,true)
numbers.subSet(34,false,65,false)
numbers.headSet(50)
numbers.tailSet(50)
Queue<String> queue = new PriorityQueue<>();
queue.poll()
queue.offer("Apple")
queue.addAll(List.of("Zebra", "Monkey", "Cat"))
queue
queue.poll()
queue
queue.poll()
queue.poll()
queue.poll()
queue.poll()
map.put("R",1);
map
map.get("Z")
map.get("A")
map.get("C")
map.size()
map.isEmpty()
map.containsKey("A")
map.containsKey("F")
map.containsValue(3)
map
map.containsValue(4)
map.keySet()
map.values()
map
hashmap.put("F",5)
hashmap
hashmap.put("Z",11)
hashmap
Map<String, Integer> map = Map.of("A",3,"Z",5,"B",10);
Map<String, Integer> linkedHashmap = new LinkedHashMap<>(map);
HashMap<String, Integer> hashmap = new HashMap<>();
hashmap.put("Z",5)
hashmap.put("A",15)
hashmap.put("F",25)
hashmap.put("L",250)
hashmap
LinkedHashMap<String, Integer> linkedHashMap = new LinkedHashMap<>();
hashmap
linkedHashMap.put("F",25)
linkedHashMap.put("A",15)
linkedHashMap.put("Z",5)
linkedHashMap.put("L",250)
linkedHashMap
treemap.put("F",25)
treemap.put("A",15)
treemap.put("Z",5)
treemap.put("L",250)
treemap
TreeMap<String, Integer> treemap = new TreeMap<>();
treemap.put("F",25)
treemap.put("Z",5)
treemap.put("L",250)
treemap.put("A",15)
treemap.put("B",25)
treemap.put("G",25)
treemap
treemap.higherKey("C")
treemap.lowerKey("C")
treemap.lowerKey("B")
treemap.floorKey("B")
treemap.higherKey("B")
treemap.higherKey("C")
treemap.ceilingKey("B")
treemap.lowerKey("B")
treemap.floorKey("B")
treemap.firstEntry()
treemap.lastEntry()
treemap
treemap.subMap("C", "Y")
treemap.subMap("B", "Z")
treemap.subMap("B",true, "Z",true)
```


### /12-Collections/src/collections/MapRunner.java

```java
package collections;

import java.util.HashMap;
import java.util.Map;


public class MapRunner {

	public static void main(String[] args) {
		String str = "This is an awesome occasion. "
				+ "This has never happened before.";
		
		Map<Character, Integer> occurances = new HashMap<>();
		
		char[] characters = str.toCharArray();
		
		for(char character:characters) {
			//Get the character
			Integer integer = occurances.get(character);
			if(integer==null) {
				occurances.put(character, 1);
			} else {
				occurances.put(character, integer + 1);
			}
		}
		
		System.out.println(occurances);
		
		Map<String, Integer> stringOccurances = new HashMap<>();
		String[] words = str.split(" ");
		
		
		for(String word:words) {
			//Get the character
			Integer integer = stringOccurances.get(word);
			if(integer==null) {
				stringOccurances.put(word, 1);
			} else {
				stringOccurances.put(word, integer + 1);
			}
		}
		
		System.out.println(stringOccurances);
		
		
	}

}
```


### /12-Collections/src/collections/QueueRunner.java

```java
package collections;

import java.util.Comparator;
import java.util.List;
import java.util.PriorityQueue;
import java.util.Queue;

class StringLengthComparator implements Comparator<String> {
	@Override
	public int compare(String value1, String value2) {
		return Integer.compare(value2.length(),
				value1.length());
	}

}

public class QueueRunner {

	public static void main(String[] args) {
		Queue<String> queue = new PriorityQueue<>(10,
				new StringLengthComparator());
		queue.addAll(List.of("Zebra", "Monkey", "Cat", "A",
				"B", "C", "D", "E", "F", "G"));
		queue.offer("Z");
		while (queue.peek() != null)
			System.out.println(queue.poll());
	}

}
```


### /12-Collections/src/collections/SetRunner.java

```java
package collections;

import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.List;
import java.util.Set;
import java.util.TreeSet;

public class SetRunner {

	public static void main(String[] args) {
		List<Character> characters = List.of('A','Z','A', 'B', 'Z','F');
		//unique - Set
		// Tree
		// Hash
		// LinkedHash
		
		Set<Character> treeSet = new TreeSet<>(characters);
		System.out.println("treeSet "+ treeSet);

		Set<Character> linkedHashSet = new LinkedHashSet<>(characters);
		System.out.println("linkedHashSet "+ linkedHashSet);
		
		Set<Character> hashSet = new HashSet<>(characters);
		System.out.println("hashSet "+ hashSet);

		

	}

}
```


### /12-Collections/src/collections/Student.java

```java
package collections;

public class Student implements Comparable<Student>{
	private int id;
	private String name;

	public Student(int id, String name) {
		super();
		this.id = id;
		this.name = name;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String toString() {
		return id + " " + name;
	}

	@Override
	public int compareTo(Student that) {
		return Integer.compare(that.id, this.id);
	}
}
```


### /12-Collections/src/collections/StudentsCollectionRunner.java

```java
package collections;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class AscendingStudentComparator implements Comparator<Student> {
	@Override
	public int compare(Student student1, Student student2) {
		return Integer.compare(student1.getId(), student2.getId());
	}
}

public class StudentsCollectionRunner {

	public static void main(String[] args) {
		List<Student> students = List.of(new Student(1, "Ranga"),
				new Student(100, "Adam"),
				new Student(2,"Eve"));
		
		ArrayList<Student> studentsAl = new ArrayList<>(students);
		
		System.out.println(studentsAl);
		
		Collections.sort(studentsAl);
		System.out.println("Desc " + studentsAl);
		
		//Collections.sort(studentsAl, new AscendingStudentComparator());
		
		studentsAl.sort(new AscendingStudentComparator());
		System.out.println("AscendingStudentComparator " + studentsAl);	
	}

}
```


# 13-Generics

## Steps
- Step 01 - Introduction to Generics - Why do we need Generics?
- Step 02 - Implementing Generics for the Custom List
- Step 03 - Extending Custom List with a Generic Return Method
- Step 04 - Generics Puzzles - Restrictions with extends and Generic Methods
- Step 05 - Generics and WildCards - Upper Bound and Lower Bound

## Code Examples

### /13-Generics/src/com/in28minutes/generics/GenericsRunner.java

```java
package com.in28minutes.generics;

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class GenericsRunner {

	static <X> X doubleValue(X value) {
		return value;
	}

	static <X extends List> void duplicate(X list) {
		list.addAll(list);
	}

	static double sumOfNumberList(
			List<? extends Number> numbers) {
		double sum = 0.0;
		for (Number number : numbers) {
			sum += number.doubleValue();
		}
		return sum;
	}

	static void addACoupleOfValues(
			List<? super Number> numbers) {
		numbers.add(1);
		numbers.add(1.0);
		numbers.add(1.0f);
		numbers.add(1l);
	}

	public static void main(String[] args) {
		List emptyList = new ArrayList<Number>();
		addACoupleOfValues(emptyList);
		System.out.println(emptyList);

		System.out.println(
				sumOfNumberList(List.of(1, 2, 3, 4, 5)));
		System.out.println(sumOfNumberList(
				List.of(1.1, 2.1, 3.1, 4.1, 5.1)));
		System.out.println(sumOfNumberList(
				List.of(1l, 2l, 3l, 4l, 5l)));

		String value1 = doubleValue(new String());
		Integer number1 = doubleValue(Integer.valueOf(5));
		ArrayList list1 = doubleValue(new ArrayList());

		LinkedList<Integer> numbers = new LinkedList<>(
				List.of(1, 2, 3));
		duplicate(numbers);
		System.out.println(numbers);

		MyCustomList<String> list = new MyCustomList<>();
		list.addElement("Element 1");
		list.addElement("Element 2");
		String value = list.get(0);

		System.out.println(value);

		MyCustomList<Integer> list2 = new MyCustomList<>();
		list2.addElement(Integer.valueOf(5));
		list2.addElement(Integer.valueOf(7));
		Integer number = list2.get(0);
		System.out.println(number);

	}

}
```


### /13-Generics/src/com/in28minutes/generics/MyCustomList.java

```java
package com.in28minutes.generics;

import java.util.ArrayList;

public class MyCustomList<T>{
	
	ArrayList<T> list = new ArrayList<>();
	
	public void addElement(T element) {
		list.add(element);
	}
	
	public void removeElement(T element) {
		list.remove(element);
	}
	
	public String toString() {
		return list.toString();
	}

	public T get(int index) {
		return list.get(index);
	}
}
```


# 14-FunctionalProgramming

## Steps
- Step 01 - Introduction to Functional Programming - Functions are First Class Citizens
- Step 02 - Functional Programming - First Example with Function as Parameter
- Step 03 - Functional Programming - Exercise - Loop a List of Numbers
- Step 04 - Functional Programming - Filtering - Exercises to print odd and even numbers from List
- Step 05 - Functional Programming - Collect - Sum of Numbers in a List
- Step 06 - Functional Programming vs Structural Programming - A Quick Comparison
- Step 07 - Functional Programming Terminology - Lambda Expression, Stream and Operations on a Stream
- Step 08 - Stream Intermediate Operations - Sort, Distinct, Filter and Map
- Step 09 - Stream Intermediate Operations - Exercises - Squares of First 10, Map String List to LowerCase and Length of String
- Step 10 - Stream Terminal Operations - 1 - max operation with Comparator 
- Step 11 - Stream Terminal Operations - 2 - min, collect to List, 
- Step 12 - Optional class in Java - An Introduction
- Step 13 - Behind the Screens with Functional Interfaces - Implement Predicate Interface
- Step 14 - Behind the Screens with Functional Interfaces - Implement Consumer Interface
- Step 15 - Behind the Screens with Functional Interfaces - Implement Function Inteface for Mapping
- Step 16 - Simplify Functional Programming code with Method References - static and instance methods
- Step 17 - Functions are First Class Citizens
- Step 18 - Introduction to Functional Programming - Conclusion

## Exercises
- Create a list of numbers
   - Print each element using forEach
   - Filter Odd and Even numbers
- Print squares of first 10 Numbers using ```IntStream.range(1,11)```
- ```List.of("Apple","Ant","Bat").stream()``` 
   - Map each to lowercase and print
   - Print length (no of characters) of each word using map

## Code Examples

### /14-FunctionalProgramming/commands.txt

```java
List<Integer> list = List.of(1,4,7,9);
list.stream().forEach(
      element -> System.out.println(element)
)
list.stream().filter(
               element -> element%2 == 1)
list.stream().filter(
               element -> element%2 == 1).
             forEach(
               element -> System.out.println(element))
list.stream().filter(element -> element%2==1).forEach(element->System.out.println(element))
list.stream().filter(element -> element%2==0).forEach(element->System.out.println(element))
numbers.stream().sorted().forEach(e->System.out.println(e));
List<Integer> numbers = List.of(3,5,3,213,45,5,7);
numbers.stream().distinct().forEach(e->System.out.println(e));
numbers.stream().distinct().sorted().forEach(e->System.out.println(e));
numbers.stream().distinct().map(e -> e * e).forEach(e->System.out.println(e));
IntStream.range(1,10).forEach(p->System.out.println(p))
IntStream.range(1,11).forEach(p->System.out.println(p))
IntStream.range(1,11).map(e -> e * e).forEach(p->System.out.println(p))
List.of("Apple", "Ant", "Bat").stream().map(s->s.toLowerCase()).forEach(p -> System.out.println(p))
List.of("Apple", "Ant", "Bat").stream().map(s->s.length()).forEach(p -> System.out.println(p))
IntStream.range(1,11).reduce( 0 , (n1,n2) -> n1+n2)
List.of(23,12,34,53).stream().max((n1,n2) -> Integer.compare(n1,n2))
$24.isPresent()
List.of(23,12,34,53).stream().max((n1,n2) -> Integer.compare(n1,n2)).get()
List.of(23,12,34,53).stream().max((n1,n2) -> Integer.compare(n1,n2)).get()
List.of(23,12,34,53).stream().max((n1,n2) -> Integer.compare(n1,n2)).get()
List.of(23,12,34,53).stream().min((n1,n2) -> Integer.compare(n1,n2)).get()
List.of(23,12,34,53).stream().filter(e -> e%2==1).forEach(e -> System.out.println(e))
List.of(23,12,34,53).stream().filter(e -> e%2==1).collect(Collectors.toList())
List.of(23,12,34,53).stream().filter(e -> e%2==0).collect(Collectors.toList())
IntStream.range(1,11).map(e -> e * e)
List.of(23,12,34,53).stream().filter(e -> e%2==0).collect(Collectors.toList())
IntStream.range(1,10).map(e -> e * e)
IntStream.range(1,10).map(e -> e * e).boxed().collect(Collectors.toList())
IntStream.range(1,11).map(e -> e * e).boxed().collect(Collectors.toList())
List.of(23,45,67,12).stream().filter(n -> n%2==0).max( (n1,n2) -> Integer.compare(n1,n2) )
$39.get()
$39.isPresent()
List.of(23,45,67).stream().filter(n -> n%2==0).max( (n1,n2) -> Integer.compare(n1,n2) )
$42.isPresent()
$42.orElse(0)
$42.orElse(0)
List.of(23,45,67).stream().filter(n -> n%2==0).max( (n1,n2) -> Integer.compare(n1,n2) ).orElse(0)
List.of(23,45,67,34).stream().filter(n -> n%2==0).max( (n1,n2) -> Integer.compare(n1,n2) ).orElse(0)
```


### /14-FunctionalProgramming/src/com/in28minutes/functionalprogramming/FPNumberRunner.java

```java
package com.in28minutes.functionalprogramming;

import java.util.List;

public class FPNumberRunner {

	public static void main(String[] args) {
		List<Integer> numbers = List.of(4,6,8,13,3,15);
		
		//Exercise - Print squares of first 10 numbers!
		//Clue - IntStream.range(1,10)
		
		//List.of("Apple", "Ant", "Bat").stream()
		//Map all of these to lowercase and print them

		//List.of("Apple", "Ant", "Bat").stream()
		//Print the length of each element

		/*
		numbers.stream()
				.forEach( element ->System.out.println(element));*/
		
		int sum = fpSum(numbers);
			
		System.out.println(sum);

	}

	private static int fpSum(List<Integer> numbers) {
		return numbers.stream()
				.reduce(0, 
					(number1, number2) ->  number1 + number2);
	}

	private static int normalSum(List<Integer> numbers) {
		int sum = 0;
		for(int number:numbers) {
			sum += number; 
		}
		return sum;
	}

}
```


### /14-FunctionalProgramming/src/com/in28minutes/functionalprogramming/FunctionalProgrammingRunner.java

```java
package com.in28minutes.functionalprogramming;

import java.util.List;

public class FunctionalProgrammingRunner {

	public static void main(String[] args) {
		List<String> list = List.of("Apple", "Bat", "Cat",
				"Dog");
		printWithFPWithFiltering(list);

	}

	private static void printBasic(List<String> list) {
		for (String string : list) {
			System.out.println(string);
		}
	}

	private static void printBasicWithFiltering(
			List<String> list) {
		for (String string : list) {
			if (string.endsWith("at")) {
				System.out.println(string);
			}
		}
	}

	private static void printWithFP(List<String> list) {
		list.stream().forEach(element -> System.out
				.println("element - " + element));
	}
	
	private static void printWithFPWithFiltering(List<String> list) {
		list.stream()
				.filter(element -> element.endsWith("at"))
			.forEach(element -> System.out.println("element - " + element));
	}

}
```


### /14-FunctionalProgramming/src/com/in28minutes/functionalprogramming/LambdaBehindTheScreensRunner.java

```java
package com.in28minutes.functionalprogramming;

import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;

class EvenNumberPredicate implements Predicate<Integer> {

	@Override
	public boolean test(Integer number) {
		return number%2 == 0;
	}
	
}

class SystemOutConsumer implements Consumer<Integer> {

	@Override
	public void accept(Integer number) {
		System.out.println(number);
	}
	
}

class NumberSquareMapper implements Function<Integer, Integer> {

	@Override
	public Integer apply(Integer number) {
		return number * number;
	}
	
}

public class LambdaBehindTheScreensRunner {
	
	

	public static void main(String[] args) {

		List.of(23,43,34,45,36,48).stream()
		.filter(n -> n%2 ==0)
		.map(n -> n * n)
		.forEach(e -> System.out.println(e));

		List.of(23,43,34,45,36,48).stream()
		.filter(new EvenNumberPredicate())
		.map(new NumberSquareMapper())
		.forEach(new SystemOutConsumer());

		//.map(n -> n * n)
		//<R> Stream<R> map(Function<? super T, ? extends R> mapper);
		// R apply(T t);
		
		//.filter(new EvenNumberPredicate())
		//Stream<T> filter(Predicate<? super T> predicate);
		//boolean test(T t);
		
		//.forEach(e -> System.out.println(e));
		//Consumer<? super T> action
		//void accept(T t);
		
		//1.Storing functions in variables
		//2.Passing functions to methods <=
		//3.Returning functions from methods
		
		Predicate<? super Integer> evenPredicate = createEvenPredicate();
		Predicate<? super Integer> oddPredicate = n -> n%2 ==1;
		
		List.of(23,43,34,45,36,48).stream()
				.filter(evenPredicate)
				.map(n -> n * n)
				.forEach(e -> System.out.println(e));
	}

	private static Predicate<? super Integer> createEvenPredicate() {
		return n -> n%2 ==0;
	}

}
```


### /14-FunctionalProgramming/src/com/in28minutes/functionalprogramming/MethodReferencesRunner.java

```java
package com.in28minutes.functionalprogramming;

import java.util.List;

public class MethodReferencesRunner {

	public static void print(Integer number) {
		System.out.println(number);
	}

	public static void main(String[] args) {
		List.of("Ant", "Bat", "Cat", "Dog", "Elephant")
				.stream().map(s -> s.length())
				.forEach(s -> MethodReferencesRunner
						.print(s));

		List.of("Ant", "Bat", "Cat", "Dog", "Elephant")
				.stream().map(String::length)
				.forEach(MethodReferencesRunner::print);

		List.of(23,45,67,34).stream()
				.filter(n -> n%2==0)
				.max( (n1,n2) -> Integer.compare(n1,n2) )
				.orElse(0);
		
		Integer max = List.of(23, 45, 67, 34).stream()
				.filter(MethodReferencesRunner::isEven)
				.max(Integer::compare)
				.orElse(0);
		
		System.out.println(max);
	}

	public static boolean isEven(Integer number) {
		return number % 2 == 0;
	}

}
```




# /15-
ThreadsAndConcurrency

## Steps
- Step 01 - Introduction to Threads and MultiThreading - Need for Threads
- Step 02 - Creating a Thread for Task1 - Extending Thread Class
- Step 03 - Creating a Thread for Task2 - Implement Runnable Interface
- Step 04 - Theory - States of a Thread
- Step 05 - Placing Priority Requests for Threads
- Step 06 - Communication between Threads - join method
- Step 07 - Thread utility methods and synchronized keyword - sleep, yield
- Step 08 - Need for Controlling the Execution of Threads
- Step 09 - Introduction to Executor Service 
- Step 10 - Executor Service - Customizing number of Threads
- Step 11 - Executor Service - Returning a Future from Thread using Callable
- Step 12 - Executor Service - Waiting for completion of multiple tasks using invokeAll
- Step 13 - Executor Service - Wait for only the fastest task using invokeAny
- Step 14 - Threads and MultiThreading - Conclusion

## Code Examples

### /15-
ThreadsAndConcurrency/src/CallableRunner.java

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

class CallableTask implements Callable<String> {
   
   private String name;

   public CallableTask(String name) {
      this.name = name;
   }
   
   @Override
   public String call() throws Exception {
      Thread.sleep(1000);
      return "Hello " + name;
   }
   
}

public class CallableRunner {

   public static void main(String[] args) throws InterruptedException, ExecutionException {
      ExecutorService executorService = Executors.newFixedThreadPool(1);
      
      Future<String> welcomeFuture = 
            executorService.submit(new CallableTask("in28Minutes"));
      
      System.out.print("\n new CallableTask(\"in28Minutes\") executed");
      
      String welcomeMessage = welcomeFuture.get();
      
      System.out.println(welcomeMessage);
      
      System.out.print("\n Main completed");

   }

}
```

### /15-
ThreadsAndConcurrency/src/ExecutorServiceRunner.java

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class Task extends Thread {
	
	private int number;

	public Task(int number) {
		this.number = number;
	}
	
	public void run() { //SIGNATURE
		System.out.print("\nTask " + number + " Started");
		
		for(int i=number*100;i<=number*100 + 99; i++) 
			System.out.print(i + " ");
		
		System.out.print("\nTask" + number +  "Done");
	}
}


public class ExecutorServiceRunner {

	public static void main(String[] args) {
		//ExecutorService executorService = Executors.newSingleThreadExecutor();
		ExecutorService executorService = Executors.newFixedThreadPool(5);
		
		executorService.execute(new Task(1));
		executorService.execute(new Task(2));
		executorService.execute(new Task(3));
		executorService.execute(new Task(4));
		executorService.execute(new Task(5));
		executorService.execute(new Task(6));
		executorService.execute(new Task(7));
				
		executorService.shutdown();

	}

}
```


### /15-
ThreadsAndConcurrency/src/MultipleAnyCallableRunner.java

```java
import java.util.List;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class MultipleAnyCallableRunner {

	public static void main(String[] args) throws InterruptedException, ExecutionException {
		ExecutorService executorService = Executors.newFixedThreadPool(3);
		
		List<CallableTask> tasks = List.of(
				new CallableTask("in28Minutes"),
				new CallableTask("Ranga"),
				new CallableTask("Adam"));
		
		String result = executorService.invokeAny(tasks);
		
		System.out.println(result);

		executorService.shutdown();
	}

}
```


### /15-
ThreadsAndConcurrency/src/MultipleCallableRunner.java

```java
import java.util.List;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class MultipleCallableRunner {

	public static void main(String[] args) throws InterruptedException, ExecutionException {
		ExecutorService executorService = Executors.newFixedThreadPool(3);
		
		List<CallableTask> tasks = List.of(new CallableTask("in28Minutes"), 
				new CallableTask("Ranga"),  new CallableTask("Adam"));
		
		List<Future<String>> results = executorService.invokeAll(tasks);
		
		for(Future<String> result:results) {
			System.out.println(result.get());
		}

		executorService.shutdown();
	}

}
```


### /15-
ThreadsAndConcurrency/src/ThreadBasicsRunner.java

```java
//extends Thread
//implements Runnable

class Task1 extends Thread {
	
	public void run() { //SIGNATURE
		System.out.print("\nTask1 Started");
		
		for(int i=101;i<=199; i++) 
			System.out.print(i + " ");
		
		System.out.print("\nTask1 Done");
	}
}

class Task2 implements Runnable {

	@Override
	public void run() {
		System.out.print("\nTask2 Started");
		
		for(int i=201;i<=299; i++) 
			System.out.print(i + " ");
		
		System.out.print("\nTask2 Done");
		
		
	}
	
}


public class ThreadBasicsRunner {

	public static void main(String[] args) throws InterruptedException {

		//• NEW;
		//• RUNNABLE;
		//• RUNNING;
		//• BLOCKED/WAITING;
		//• TERMINATED/DEAD;
		
		//Task1 - 101 to 199
		System.out.print("\nTask1 Kicked Off");
		Task1 task1 = new Task1();
		task1.setPriority(1);
		task1.start(); //task1.run();
		
		System.out.print("\nTask2 Kicked Off");
		
		Task2 task2 = new Task2();
		Thread task2Thread = new Thread(task2);
		task2Thread.setPriority(10);
		task2Thread.start();	
	
		task1.join();
		task2Thread.join();
		
		System.out.print("\nTask3 Kicked Off");
		
		//Task3
		for(int i=301;i<=399; i++) 
			System.out.print(i + " ");
		
		System.out.print("\nTask3 Done");
		
		System.out.print("\nMain Done");
	}
}
```


# 16-ExceptionHandling

## Steps
- Step 01 - Introduction to Exception Handling - Your Thought Process during Exception Handling
- Step 02 - Basics of Exceptions - NullPointerException and StackTrace
- Step 03 - Basics of Handling Exceptions - try and catch
- Step 04 - Basics of Handling Exceptions - Exception Hierarchy, Matching and Catching Multiple Exceptions
- Step 05 - Basics of Handling Exceptions - Need for finally
- Step 06 - Basics of Handling Exceptions - Puzzles
- Step 07 - Checked Exceptions vs Unchecked Exceptions - An Example
- Step 08 - Hierarchy of Errors and Exceptions - Checked and Runtime
- Step 09 - Throwing an Exception - Currencies Do Not Match Runtime Exception
- Step 10 - Throwing a Checked Exception - Throws in method signature and handling
- Step 11 - Throwing a Custom Exception - CurrenciesDoNotMatchException
- Step 12 - Write less code with Try with Resources - New Feature in Java 7
- Step 13 - Basics of Handling Exceptions - Puzzles 2
- Step 14 - Exception Handling - Conclusion with Best Practices
## Code Examples

### /16-ExceptionHandling/src/com/in28minutes/exceptionhandling/CheckedExceptionRunner.java

```java
package com.in28minutes.exceptionhandling;

public class CheckedExceptionRunner {
	
	public static void main(String[] args) {
	/*	try {
			someOtherMethod();
			Thread.sleep(2000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}*/
		//someOtherMethod1();
		someOtherMethod2();

	}
	
	private static void someOtherMethod2() throws RuntimeException{
		
	}
	
	private static void someOtherMethod() throws InterruptedException{
		Thread.sleep(2000);
	}

}
```


### /16-ExceptionHandling/src/com/in28minutes/exceptionhandling/ExceptionHandlingRunner.java

```java
package com.in28minutes.exceptionhandling;

public class ExceptionHandlingRunner {

	public static void main(String[] args) {
		method1();
		System.out.println("Main Ended");
	}

	private static void method1() {
		method2();
		System.out.println("Method1 Ended");
	}

	private static void method2() {
		String str = null;
		str.length();
		System.out.println("Method2 Ended");
	}
}
```


### /16-ExceptionHandling/src/com/in28minutes/exceptionhandling/ExceptionHandlingRunner2.java

```java
package com.in28minutes.exceptionhandling;

public class ExceptionHandlingRunner2 {

	public static void main(String[] args) {
		method1();
		System.out.println("Main Ended");
	}

	private static void method1() {
		method2();
		System.out.println("Method1 Ended");
	}

	private static void method2() {
		try {
			//String str = null;
			//str.length();
			int[] i = {1,2};
			int number = i[3];
			System.out.println("Method2 Ended");
		} catch (NullPointerException ex) {
			System.out.println("Matched NullPointerException");
			ex.printStackTrace();
		} catch (ArrayIndexOutOfBoundsException ex) {
			System.out.println("Matched ArrayIndexOutOfBoundsException");
			ex.printStackTrace();
		} catch (Exception ex) {
			System.out.println("Matched Exception");
			ex.printStackTrace();
		}
	}
}
```


### /16-ExceptionHandling/src/com/in28minutes/exceptionhandling/FinallyRunner.java

```java
package com.in28minutes.exceptionhandling;

import java.util.Scanner;

public class FinallyRunner {

	public static void main(String[] args) {
		
		Scanner scanner = null;

		try {
			scanner = new Scanner(System.in);
			int[] numbers = { 12, 3, 4, 5 };

			int number = numbers[21];

		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			System.out.println("Before Scanner Close");
			if(scanner!=null) {
				scanner.close();
			}
		}
		
		System.out.println("Just before closing out main");
	}

}
```


### /16-ExceptionHandling/src/com/in28minutes/exceptionhandling/ThrowingExceptionRunner.java

```java
package com.in28minutes.exceptionhandling;

class Amount {
	private String currency;
	private int amount;
	
	public Amount(String currency, int amount) {
		super();
		this.currency = currency;
		this.amount = amount;
	}
	
	public void add(Amount that) throws CurrenciesDoNotMatchException {
		
		if(!this.currency.equals(that.currency)) {
			//throw new Exception("Currencies Don't Match " + this.currency + " & " +that.currency );
			throw new CurrenciesDoNotMatchException("Currencies Don't Match " + this.currency + " & " +that.currency );
		}
		
		this.amount = this.amount + that.amount;
	}
	
	public String toString() {
		return amount + " " + currency; 
	}
}

class CurrenciesDoNotMatchException extends Exception {
	public CurrenciesDoNotMatchException(String msg) {
		super(msg);
	}
}

public class ThrowingExceptionRunner {

	public static void main(String[] args) throws CurrenciesDoNotMatchException {
		Amount amount1 = new Amount("USD", 10);
		Amount amount2 = new Amount("EUR", 20);
		amount1.add(amount2);
		System.out.println(amount1);	
	}

}
```


### /16-ExceptionHandling/src/com/in28minutes/exceptionhandling/TryWithResourcesRunner.java

```java
package com.in28minutes.exceptionhandling;

import java.util.Scanner;

public class TryWithResourcesRunner {

	public static void main(String[] args) {
		try (Scanner scanner = new Scanner(System.in)) {
			int[] numbers = { 12, 3, 4, 5 };
			int number = numbers[21];
		} 
	}

}
```

# 17-Files

## Steps
- Step 01 - List files and folders in Directory with Files list method
- Step 02 - Recursively List and Filter all files and folders in Directory with Step Files walk method and Search with find method
- Step 03 - Read content from a File - Files readAllLines and lines methods
- Step 04 - Writing Content to a File - Files write method
- Step 05 - Files - Conclusion

## Code Examples

### /17-Files/src/files/DirectoryScanRunner.java

```java
package files;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.attribute.BasicFileAttributes;
import java.util.function.BiPredicate;
import java.util.function.Predicate;

public class DirectoryScanRunner {

	public static void main(String[] args) throws IOException {
		
		Path currentDirectory = Paths.get(".");
		//Files.list(currentDirectory).forEach(System.out::println);
		
		Predicate<? super Path> predicate 
				= path -> String.valueOf(path).contains(".java");
		
		//Files.walk(currentDirectory, 4).filter(predicate).forEach(System.out::println);
		
		BiPredicate<Path, BasicFileAttributes> javaMatcher 
		= (path,attributes) -> String.valueOf(path).contains(".java");

		BiPredicate<Path, BasicFileAttributes> directoryMatcher 
		= (path,attributes) -> attributes.isDirectory();

		
		Files.find(currentDirectory, 4, directoryMatcher )
							.forEach(System.out::println);
		     
	}

}
```


### /17-Files/src/files/FileReadRunner.java

```java
package files;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

public class FileReadRunner {

	public static void main(String[] args) throws IOException {
		Path pathFileToRead = Paths.get("./resources/data.txt");
		
		//List<String> lines = Files.readAllLines(pathFileToRead);
		//System.out.println(lines);
		
		Files.lines(pathFileToRead)
			.map(String::toLowerCase)
			.filter(str -> str.contains("a"))
			.forEach(System.out::println);
		
	}

}
```


### /17-Files/src/files/FileWriteRunner.java

```java
package files;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

public class FileWriteRunner {

	public static void main(String[] args) throws IOException {
		Path pathFileToWrite = Paths.get("./resources/file-write.txt");
		
		List<String> list = 
					List.of("Apple", "Boy", "Cat", "Dog", "Elephant");
		
		Files.write(pathFileToWrite, list);
	
		
	}

}
```

### /17-Files/resources/data.txt

```
123,122
jljlfsadf
Apple
Bat
Cat

```


### /17-Files/resources/file-write.txt

```
Apple
Boy
Cat
Dog
Elephant

```

# 18-ConcurrencyLocksAtomicityAndCollections

## Steps
- Step 01 - Getting started with Synchronized
- Step 02 - Problem with Synchronized - Less Concurrency
- Step 03 - Enter Locks with ReEntrantLock
- Step 04 - Introduction to Atomic Classes - AtomicInteger
- Step 05 - Need for ConcurrentMap
- Step 06 - Implementing an example with ConcurrentHashMap
- Step 07 - ConcurrentHashMap uses different locks for diferrent regions
- Step 08 - CopyOnWrite Concurrent Collections - When reads are more than writes
- Step 09 - Conclusion

## Code Examples

### /src/com/in28minutes/concurrency/BiCounter.java

```java
package com.in28minutes.concurrency;

public class BiCounter {
  private int i = 0;
  private int j = 0;
  
  synchronized public void incrementI() {
    i++; 
    //get i
    //increment  
    //set i
  }

  public int getI() {
    return i;
  }
  
  synchronized public void incrementJ() {
    j++; 
    //get j
    //increment  
    //set j
  }

  public int getJ() {
    return j;
  }

}
```
### /src/com/in28minutes/concurrency/BiCounterWithAtomicInteger.java

```java
package com.in28minutes.concurrency;

import java.util.concurrent.atomic.AtomicInteger;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class BiCounterWithAtomicInteger {
  private AtomicInteger i = new AtomicInteger();
  private AtomicInteger j = new AtomicInteger();
    
  public void incrementI() {    
    i.incrementAndGet();
  }

  public int getI() {
    return i.get();
  }
  
  public void incrementJ() {
    j.incrementAndGet(); 
  }

  public int getJ() {
    return j.get();
  }

}
```
### /src/com/in28minutes/concurrency/BiCounterWithLock.java

```java
package com.in28minutes.concurrency;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class BiCounterWithLock {
  private int i = 0;
  private int j = 0;
  
  Lock lockForI = new ReentrantLock();
  Lock lockForJ = new ReentrantLock();
  
  public void incrementI() {    
    lockForI.lock();//Get Lock For I 
    i++;
    lockForI.unlock();
    //Release Lock For I
  }

  public int getI() {
    return i;
  }
  
  public void incrementJ() {
    lockForJ.lock();//Get Lock For J
    j++; 
    lockForJ.unlock();//Release Lock For J
  }

  public int getJ() {
    return j;
  }

}
```
### /src/com/in28minutes/concurrency/ConcurrencyRunner.java

```java
package com.in28minutes.concurrency;

public class ConcurrencyRunner {

  public static void main(String[] args) {
    Counter counter = new Counter();
    counter.increment();
    counter.increment();
    counter.increment();
    System.out.println(counter.getI());

  }

}
```
### /src/com/in28minutes/concurrency/ConcurrentMapRunner.java

```java
package com.in28minutes.concurrency;

import java.util.Hashtable;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ConcurrentMap;
import java.util.concurrent.atomic.LongAdder;

public class ConcurrentMapRunner {

  public static void main(String[] args) {
    ConcurrentMap<Character, LongAdder> occurances = new ConcurrentHashMap<>();
    
    String str = "ABCD ABCD ABCD";

    for(char character:str.toCharArray()) {
      occurances.computeIfAbsent(character, ch -> new LongAdder()).increment();
    }
    
    System.out.println(occurances);
        

  }

  /*
      Map<Character, LongAdder> occurances = new Hashtable<>();
    
    String str = "ABCD ABCD ABCD";
    for(char character:str.toCharArray()) {
      LongAdder longAdder = occurances.get(character);
      if(longAdder == null) {
        longAdder = new LongAdder();
      }
      longAdder.increment();
      occurances.put(character, longAdder);
    }
    
    System.out.println(occurances);

   */
}
```
### /src/com/in28minutes/concurrency/CopyOnWriteArrayListRunner.java

```java
package com.in28minutes.concurrency;

import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class CopyOnWriteArrayListRunner {
  
  //add - copy
  //get

  public static void main(String[] args) {
    List<String> list = new CopyOnWriteArrayList<>();
    
    //Threads - 3
    list.add("Ant");
    list.add("Bat");
    list.add("Cat");
    
    //Threads - 10000
    for(String element:list) {
      System.out.println(element);
    }
    
    // TODO Auto-generated method stub

  }

}
```
### /src/com/in28minutes/concurrency/Counter.java

```java
package com.in28minutes.concurrency;

public class Counter {
  private int i = 0;
  
  synchronized public void increment() {
    i++; 
    //get i
    //increment  
    //set i
  }

  public int getI() {
    return i;
  }
}
```

# 99-TipsAndTricks

## Steps
- Java Tip 01 - Imports and Static Imports
- Java Tip 02 - Blocks
- Java Tip 03 - equals method
- Java Tip 04 - hashcode method
- Java Tip 05 - Class Access Modifiers - public and default
- Java Tip 06 - Method Access Modifiers - public, protected, private and default
- Java Tip 07 - Final classes and Final methods
- Java Tip 08 - Final Variables and Final Arguments
- Java Tip 09 - Why do we need static variables?
- Java Tip 09 - Why do we need static methods?
- Java Tip 10 - Static methods cannot use instance methods or variables
- Java Tip 11 - public static final - Constants
- Java Tip 12 - Nested Classes - Inner Class vs Static Nested Class
- Java Tip 13 - Anonymous Classes
- Java Tip 14 - Why Enum and Enum Basics - ordinal and values
- Java Tip 15 - Enum - Constructor, variables and methods
- Java Tip 16 - Quick look at inbuild Enums - Month, DayOfWeek

## Code Examples

### /src/com/in28minutes/tips/access/package1/ClassAccessModifiers.java

```java
package com.in28minutes.tips.access.package1;


//public, protected, (default), private
public class ClassAccessModifiers {

  public static void main(String[] args) {
    // TODO Auto-generated method stub
    ClassAccessModifiers c = new ClassAccessModifiers();

  }

}
```
### /src/com/in28minutes/tips/access/package1/ExampleClass.java

```java
package com.in28minutes.tips.access.package1;

public class ExampleClass {
  public void publicMethod() {}
  protected void protectedMethod() {}
  private void privateMethod() {}
  void defaultMethod() {}
  
  public static void main(String[] args) {
    ExampleClass exampleClass = new ExampleClass();
    exampleClass.privateMethod();
    exampleClass.protectedMethod();
    exampleClass.publicMethod();
    exampleClass.defaultMethod();
  }
}
```
### /src/com/in28minutes/tips/access/package1/MethodAccessRunnerInsideSamePackage.java

```java
package com.in28minutes.tips.access.package1;

public class MethodAccessRunnerInsideSamePackage {

  public static void main(String[] args) {
    // TODO Auto-generated method stub
    ExampleClass exampleClass = new ExampleClass();
    //exampleClass.privateMethod();
    exampleClass.protectedMethod();
    exampleClass.publicMethod();
    exampleClass.defaultMethod();

  }

}
```
### /src/com/in28minutes/tips/access/package2/ClassAccessModifiersRunnerInOtherPackage.java

```java
package com.in28minutes.tips.access.package2;

import com.in28minutes.tips.access.package1.ClassAccessModifiers;

//public, protected, (default), private
public class ClassAccessModifiersRunnerInOtherPackage {

  public static void main(String[] args) {
    ClassAccessModifiers c = new ClassAccessModifiers();
  }

}
```
### /src/com/in28minutes/tips/access/package2/MethodAccessRunnerInDifferentPackage.java

```java
package com.in28minutes.tips.access.package2;

import com.in28minutes.tips.access.package1.ExampleClass;

public class MethodAccessRunnerInDifferentPackage {

  public static void main(String[] args) {
    // TODO Auto-generated method stub
    ExampleClass exampleClass = new ExampleClass();

    //exampleClass.privateMethod();
    //exampleClass.protectedMethod();
    exampleClass.publicMethod();
    //exampleClass.defaultMethod();

  }

}
```
### /src/com/in28minutes/tips/anonymous/AnonymousClassRunner.java

```java
package com.in28minutes.tips.anonymous;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class AnonymousClassRunner {
  
  public static void main(String[] args) {
    List<String> animals = new ArrayList<String>(
        List.of("Ant", "Cat", "Ball", "Elephant"));
    
    Comparator<String> lengthComparator = new Comparator<String>() {
      @Override
      public int compare(String str1, String str2) {
        return Integer.compare(str1.length(), str2.length());
      }
    };
    
    Collections.sort(animals, 
        lengthComparator
    );
    System.out.println(animals);

  }

}
```
### /src/com/in28minutes/tips/blocks/BlocksRunner.java

```java
package com.in28minutes.tips.blocks;

public class BlocksRunner {
  public static final int SECONDS_IN_MINUTE = 60;
  public static final int MINUTES_IN_HOUR = 60;
  public static final int HOURS_IN_DAY = 24;
  public static final int SECONDS_IN_DAY 
    = SECONDS_IN_MINUTE * MINUTES_IN_HOUR * HOURS_IN_DAY;
  
  public static void main(String[] args) {
    //System.out.print(Integer.MIN_VALUE);
    System.out.print(SECONDS_IN_DAY);
    
    //System.out.print("main");
    
    {
      int i;
      //System.out.print("3>2");
        //System.out.print("3>2");
    }
    
    //System.out.print(i); 

  }

}
```
### /src/com/in28minutes/tips/eclipse/DummyForTest.java

```java
package com.in28minutes.tips.eclipse;

import java.util.ArrayList;
import java.util.List;

public class DummyForTest {

  public void doSomething() {
    List list = new ArrayList();
  }

}
```
### /src/com/in28minutes/tips/eclipse/EclipseTipsAndTricks.java

```java
package com.in28minutes.tips.eclipse;

import java.math.BigDecimal;

//PAIR PROGRAMMING

class TestBean {
  private int i; //i is awesome
  private String str;
  
  
  
  public TestBean() {
    /*
     fsadjflkas
     fskljdfalsk
     */
    super();  
  }
  
  public TestBean(int i, String str) {
    super();
    this.i = i;
    this.str = str;
  }
  /* (non-Javadoc)
   * @see java.lang.Object#hashCode()
   */
  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + i;
    return result;
  }
  /* (non-Javadoc)
   * @see java.lang.Object#equals(java.lang.Object)
   */
  @Override
  public boolean equals(Object obj) {
    if (this == obj) {
      return true;
    }
    if (obj == null) {
      return false;
    }
    if (getClass() != obj.getClass()) {
      return false;
    }
    TestBean other = (TestBean) obj;
    if (i != other.i) {
      return false;
    }
    return true;
  }
  /**
   * @return the i
   */
  public int getI() {
    return i;
  }
  /**
   * @param i the i to set
   */
  public void setI(int i) {
    this.i = i;
  }
  /**
   * @return the str
   */
  public String getStr() {
    return str;
  }
  /**
   * @param str the str to set
   */
  public void setStr(String str) {
    this.str = str;
  }
  
  
  
}

class Test implements Comparable<String> {

  @Override
  public int compareTo(String arg0) {
    return 0;
  }
  
}

public class EclipseTipsAndTricks {
  
  public static void main(String[] args) throws InterruptedException {
    
    DummyForTest dt = new DummyForTest();
    dt.doSomething();
    BigDecimal bd = new BigDecimal(25);
    Thread.sleep(returnSomething());
  }

  private static int returnSomething() {
    return 1000 * 45 * 456;
  }

}
```
### /src/com/in28minutes/tips/enums/EnumRunner.java

```java
package com.in28minutes.tips.enums;

import java.util.Arrays;

public class EnumRunner {

  public static void main(String[] args) {
    Season season = Season.FALL;

    Season season1 = Season.valueOf("WINTER");
    System.out.println(season1);
    System.out.println(Season.SPRING.ordinal());
    System.out.println(Season.SPRING.getValue());

    System.out
        .println(Arrays.toString(Season.values()));

  }

}
```
### /src/com/in28minutes/tips/enums/Season.java

```java
package com.in28minutes.tips.enums;
public enum Season {
  SPRING(4), SUMMER(1), WINTER(2), FALL(3) ;
  
  private int value;
  
  private Season(int value) {
    this.value = value;
  }

  public int getValue() {
    return value;
  }
  
  
  //0,1,2,3
}
```
### /src/com/in28minutes/tips/equals/EqualsRunner.java

```java
package com.in28minutes.tips.equals;

class Client {
  private int id;

  public Client(int id) {
    super();
    this.id = id;
  }

  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + id;
    return result;
  }

  @Override
  public boolean equals(Object that) {
    if (this == that)
      return true;
    
    if (that == null)
      return false;
    if (getClass() != that.getClass())
      return false;
    Client other = (Client) that;
    if (id != other.id)
      return false;
    return true;
  }
  
  //equals
  //hashcode
  
  
  
}

public class EqualsRunner {

  public static void main(String[] args) {
    Client c1 = new Client(1);
    Client c2 = new Client(1);
    Client c3 = new Client(2);
    System.out.println(c1.equals(c2));
    System.out.println(c1.equals(c3));
    
    
  }

}
```
### /src/com/in28minutes/tips/imports/ImportsRunner.java

```java
package com.in28minutes.tips.imports;

//import java.lang.*; //DEFAULT
import java.math.BigDecimal;
import java.util.ArrayList;
//import java.util.Collections;

import static java.lang.System.out;
import static java.util.Collections.*;

public class ImportsRunner {

  public static void main(String[] args) {
    
    out.println("IMports");
    out.println("Static Imports");
    
    sort(new ArrayList<String>());
    
    BigDecimal db = null;

  }

}
```
### /src/com/in28minutes/tips/nonaccess/package1/FinalNonAccessModifierRunner.java

```java
package com.in28minutes.tips.nonaccess.package1;

final class FinalClass {
  
}

//class SomeClass extends FinalClass{
//}

class SomeClass {
  final public void doSomething() {}
  public void doSomethingElse(final int arg) {
    //arg = 6;
    
  }
}

class ExtendingClass extends SomeClass {
  //public void doSomething() {}
}

public class FinalNonAccessModifierRunner {
  
  public static void main(String[] args) {
    final int i;
    i=5;
    
    //i = 7;

  }

}
```
### /src/com/in28minutes/tips/nonaccess/package1/StaticModifierRunner.java

```java
package com.in28minutes.tips.nonaccess.package1;

class Player{
  private String name;
  
  private static int count = 0;
  
  public Player(String name) {
    super();
    this.name = name;
    count++;
  }

  static public int getCount() {
    return count;
  }

  public String getName() {
    System.out.println(count);
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }
  
  
}

public class StaticModifierRunner {
  
  public static void main(String[] args) {
    Player player1 = new Player("Ronaldo");
    
    System.out.println(Player.getCount());
    
    Player player2 = new Player("Federer");
    
    System.out.println(Player.getCount());
  }

}
```
---

# Java to Python in 100 Easy Steps

## Fastest way to Learn Python for Experienced Java Programmers

## Complete Code Example


### /oops/abstract_class_example.py

```py
from abc import ABC, abstractmethod

class AbstractRecipe(ABC):

    def execute(self):
        self.get_ready()
        self.do_the_dish()
        self.cleanup()

    @abstractmethod
    def get_ready(self):
        pass

    @abstractmethod
    def do_the_dish(self):
        pass

    @abstractmethod
    def cleanup(self):
        pass


class Recipe1(AbstractRecipe):

    def get_ready(self):
        print('Get raw materials')
        print('Get utensils')

    def do_the_dish(self):
        print('do the dish')

    def cleanup(self):
        print('clean utensils')


# TypeError: Can't instantiate abstract class AbstractRecipe
# with abstract methods cleanup, do_the_dish, get_ready
# recipe = AbstractRecipe()

recipe = Recipe1()

recipe.execute()
```
---

### /oops/abstract_class_to_implement_interface_example.py

```py
from abc import ABC,abstractmethod


# class GamingConsole(ABC):
#     @abstractmethod
#     def up(self): pass
#
#     @abstractmethod
#     def down(self): pass
#
#     @abstractmethod
#     def left(self): pass
#
#     @abstractmethod
#     def right(self): pass


class MarioGame:
    def up(self): print('jump')

    def down(self): print('goes into a hole')

    def left(self): pass

    def right(self): print('Go Forward')


class ChessGame:
    def up(self): print('Move piece up')

    def down(self): print('Move piece down')

    def left(self): print('Move piece left')

    def right(self): print('Move piece right')


# games = [ChessGame(), MarioGame()]
#
# for game in games:
#     game.up()
#     game.down()
#     game.left()
#     game.right()

class Test1:
    def method(self): print("Test1")

class Test2:
    def method(self): print("Test2")

tests = [Test1(),Test2()]

for test in tests:
    test.method()

```
---

### /oops/book_example.py

```py
# MotorBike
 # gear, speed

class Book:

    def __init__(self, name, copies):
        self.name = name
        self.copies = copies

    def __repr__(self):
        return repr((self.name, self.copies))

    def increase_copies(self, how_much):
        self.copies += how_much

    def decrease_copies(self, how_much):
        self.copies -= how_much

    #set
    #get

book1 = Book('Mastering Spring 5.0', 200)
book1.increase_copies(50)

book2 = Book('Mastering Python 3', 15)
book2.decrease_copies(5)

print(book1)
print(book2)
```
---

### /oops/encapsulation_examples.py

```py
class BookEnhanced:
    def __init__(self, name, copies):
        self.name = name
        self._copies = copies

    @property
    def copies(self):
        print('getter called')
        return self._copies

    @copies.setter
    def copies(self, copies):
        print('setter called')
        if(copies>=0):
            self._copies = copies

microservices = BookEnhanced('Microservices',5)

print(microservices.copies)

microservices.copies = 10

print(microservices.copies)
```
---

### /oops/exception_handling_examples.py

```py
# try:
#     i = 0
#     number = 10/i
# except ZeroDivisionError as error:
#     print(error)
#     number = 0
# else: # else is execute when exception is not thrown
#     print('else')
# finally:
#     print('finally')
#
# print(number)
#

class Amount:
    def __init__(self, currency, amount):
        self.currency = currency
        self.amount = amount

    def add(self, that):
        if(self.currency==that.currency):
            self.amount += that.amount
        else:
            raise CurrencyDoNotMatchException(self.currency + " " + that.currency)

    def __repr__(self):
        return repr((self.currency,self.amount))

class CurrencyDoNotMatchException(Exception):
    def __init__(self, message):
        super().__init__(message)


amount1 = Amount('EUR',35)
amount2 = Amount('INR',70)

amount2.add(amount1)
print(amount2)
```
---

### /oops/inheritance_examples.py

```py
# Student(college,year,degree)
# IS A Person(name, address)


class Person:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return repr((self.name))


class Student(Person):

    def __init__(self, name, college_name):
        super().__init__(name)
        self.college_name = college_name

    def __repr__(self):
        return repr((super().__repr__(),self.college_name))


person = Person('Ranga')

student = Student('Ranga', 'Pondicherry Engg College')

print(person)

print(student)

class Planet:
    pass

earth = Planet()
earth.__repr__()
```
---

### /oops/motor_bike_example.py

```py
class MotorBike:

    def __init__(self, gear, speed):
        self.gear = gear
        self.speed = speed

    def __repr__(self):
        return repr((self.gear, self.speed))


# instance 1 or object 1
honda = MotorBike(3, 50)

# instance 2 or object 2
ducati = MotorBike(1, 10)

print(honda)
print(ducati)
```
---

### /oops/multiple_inheritance_examples.py

```py
class LandAnimal:
    def walk(self):
        print('walk')

class WaterAnimal:
    def swim(self):
        print('swim')

class Amphibian(LandAnimal, WaterAnimal):
    pass

frog = Amphibian()

frog.swim()
frog.walk()

```
---

### /oops/oops_in_depth.py

```py
class Planet:
    def __init__(self, name, distance_from_sun):
        self.name = name
        self.distance_from_sun = distance_from_sun

earth = Planet('Earth', 200)
mars = Planet('Mars', 500)

earth.speed = 10000
print(earth.speed)

# mars.name = 'Mars'
print(mars.name)
```
---

### /oops/oops_puzzles.py

```py
class Country:
    # def __init__(self):
      #  print('constuctor 1')

    def __init__(self, name="Default"):
        self.name = name
        print('constuctor 2')

    def instance_method(self):
        print('instance method')


default_country = Country()
india = Country('India')

print(default_country.name)
print(india.name)
#TypeError: __init__() missing 1 required positional argument: 'name'
```
---

### /oops/operator_overloading_examples.py

```py
from functools import total_ordering

@total_ordering
class Money:
    def __init__(self, currency, amount):
        self.currency = currency
        self.amount = amount

    def __add__(self, other):
        return Money(self.currency, self.amount + other.amount)

    def __sub__(self, other):
        return Money(self.currency, self.amount - other.amount)

    def __repr__(self):
        return repr((self.currency, self.amount))

    def __eq__(self, other):
        return (self.currency, self.amount) == (other.currency,other.amount)

    def __le__(self, other):
        return (self.amount) <= (other.amount)

amount1 = Money('EUR', 10)
amount2 = Money('EUR', 20)
amount3 = Money('EUR', 10)

print(amount1 < amount2)
print(amount2 < amount3)
print(amount3 < amount1)

print(amount3 <= amount1)
print(amount3 >= amount1)

# print(amount1 == amount2)
# print(amount1 != amount2)
# print(amount1 == amount3)
# print(amount1 != amount3)

# print(amount1 + amount2)
# print(amount2 - amount1)



# object.__add__(self, other)
# object.__sub__(self, other)
# object.__mul__(self, other) *
# object.__matmul__(self, other)
# object.__truediv__(self, other) \
# object.__floordiv__(self, other) \\
# object.__mod__(self, other) %
# object.__pow__(self, other[, modulo]) **
# object.__and__(self, other) and
# object.__xor__(self, other) ^
# object.__or__(self, other) or
#
# i methods
```
---

### /oops/static_examples.py

```py
class Player:
    count = 0

    def __init__(self, name):
        self.name = name
        Player.count += 1

    @staticmethod
    def get_count():
        return Player.count

messi = Player('Messi')
ronaldo = Player('Ronaldo')

print(messi.get_count())
print(ronaldo.get_count())
print(Player.get_count())

# print(Player.count)
#
# print(messi.count)
# print(ronaldo.count)
#
# Player.count = 100
#
# print(Player.count)
#
# print(messi.count)
# print(ronaldo.count)

# messi.count = 100
#
# print(Player.count)//2
#
# print(messi.count)//100
# print(ronaldo.count)//2
```
---

### /python-hello-world/first_method.py

```py
# print("Hello World")


def print_hello_world_twice():
    print("Hello World 1")
    print("Hello World 2")


def print_hello_world_multiple_times(times):
    for i in range(1, times+1):
        print("Hello World")


# print("Hello World 3")

# print_hello_world_twice()

print_hello_world_multiple_times(4)
```
---

### /python-hello-world/for_loop_examples.py

```py
for i in range(1,10):
    print(i)
    print("Done")

for i in range(1,10):
    print(i*i)

print("Test")
```
---

### /python-hello-world/for_loop_exercises.py

```py

def is_prime(number):

    if number < 2:
        return False

    for divisor in range(2,number):
        if number % divisor == 0:
            return False

    return True

# print(is_prime(15));


def sum_upto_n(number):

    sum = 0

    for i in range(1, number+1):
        sum = sum + i

    return sum


# print(sum_upto_n(6))
# print(sum_upto_n(10))


def calculate_sum_of_divisors(number):
    sum_of_divisors = 0

    for divisor in range(1,number+1):
        if number % divisor == 0:
            sum_of_divisors = sum_of_divisors + divisor

    return sum_of_divisors

# print(calculate_sum_of_divisors(6))
# print(calculate_sum_of_divisors(15))


def print_a_number_triangle(number):
    for j in range(1, number + 1):
        for i in range(1, j + 1):
            print(i, end=' ')
        print()


print_a_number_triangle(6)
```
---

### /python-hello-world/hello_world.py

```py
print('Hello World')
print("Hello World2")
print("Hello World3")
```
---

### /python-hello-world/if_examples.py

```py
x_string = input("Enter a Number")
x = int(x_string)

if x == 1:
    print(f"{x} is 1")
    print("this is part of if")
elif x == 2:
    print(f"{x} is 2")
    print("this is part of elif")
else:
    print(f"{x} is NOT 1 or 2")
    print("this is part of else")
```
---

### /python-hello-world/math_basic.py

```py
def print_squares_of_numbers_upto(n):
    for i in range(1,n+1):
        print(i*i)


def print_squares_of_even_numbers_upto(n):
    for i in range(2,n+1,2):
        print(i*i)


def sum_of_two_numbers(number1,number2):
    sum = number1 + number2
    return sum


def print_numbers_in_reverse(n):
    for i in range(n,0,-1):
        print(i)


print(sum_of_two_numbers(5,6))
# print_squares_of_even_numbers_upto(10)
# print_numbers_in_reverse(10)
```
---

### /python-hello-world/menu_with_if.py

```py
number1 = int(input("Enter Number1:"))
number2 = int(input("Enter Number2:"))

print("Choices Available are ")
print("1 - Add")
print("2 - Subtract")
print("3 - Divide")
print("4 - Multiply")

choice = int(input("Enter Choice: "))

print("Your Choices are")

if choice == 1:
    print(f"Result = {number1 + number2}")
elif choice == 2:
    print(f"Result = {number1 - number2}")
elif choice == 3:
    print(f"Result = {number1 / number2}")
elif choice == 4:
    print(f"Result = {number1 * number2}")
else:
    print("Invalid Operation")
```
---

### /python-hello-world/multiplication_table.py

```py
def print_multiplication_table(table=5, start=1, end=10):
    for i in range(start, end+1):
        print(f"{table} X {i} = {table*i}")


print_multiplication_table()

# print_multiplication_table(6)

# print_multiplication_table(7, 31, 40)
```
---

### /python-hello-world/oops_trials.py

```py
class Book:

    count = 0

    def __init__(self, name):
        self._name = name
        Book.count = Book.count + 1

    @property
    def name(self):
        print("Getter For Name Called")
        return self._name

    @name.setter
    def name(self, name):
        print("Setter For Name Called")
        self._name = name

    @staticmethod
    def static_method():
        print("I'm static")

    def __setattr__(self, key, value):
        print(f'{key} - {value}')
        self.__dict__[key] = value


# book1 = Book('Microservices')
# print(book1.name)
# book1.name = 'ABC'
# print(book1.name)
# book2 = Book('Web Services')

# print(Book.count)
# print(book1.count)
# print(book2.count)
# Book.static_method()
# book1.static_method()

# print(book1.name)

def do_this_and_print(func,data):
    print(func(data))


def double(data):
    return data * 2

def triple(data):
    return data * 3


do_this_and_print(double,5)

do_this_and_print(triple,5)

do_this_and_print(lambda x : x*2, 5)

do_this_and_print(lambda x : x*5, 5)
```
---

### /python-hello-world/repeated_question.py

```py
number = int(input('Enter a number:'))

while number >= 0:
   print(f'cube is {number ** 3}')
   number = int(input('Enter a number:'))
```
---

### /python-hello-world/while_loop_examples.py

```py
i = 0

while i<11:
    print(i)
    i += 1


# print all the squares of numbers < 100
# 1 4 9 .. 81
def print_squares_of_numbers_below(limit):
    i = 1
    while i*i < limit :
        print(i*i, end=' ')
        i += 1
    print()

print_squares_of_numbers_below(100)
```
---


### /tips/all_about_methods.py

```py
def example_method(mandatory_parameter, default_parameter="Default"
                   , *args, **kwargs):
    print(f"""
        mandatory_parameter = {mandatory_parameter} {type(mandatory_parameter)}
        default_parameter = {default_parameter} {type(default_parameter)}
        args = {args} {type(args)}
        kwargs = {kwargs} {type(kwargs)}
        """)

# example_method() #example_method() missing 1 required positional argument
# example_method(mandatory_parameter=15)  #example_method(15)
# example_method(25,"Some String")
# example_method(25,"String 1","String 2","String 3")
# example_method(25,"String 1","String 2","String 3","String 4","String 5")
# example_method(25,"String 1","String 2","String 3",key1='a', key2='b')
#example_method(25,"String 1",key1='a', key2='b')
# example_method(key1='a', key2='b',mandatory_parameter=25,default_parameter="String 1")
# example_method(25,"String 1",key1='a', key2='b')
example_list = [1,2,3,4,5,6]
# example_method(*example_list)
example_dict = {'a':'1', 'b':'2'}
example_method(*example_list, **example_dict)
```
---

### /tips/enum_examples.py

```py
# Currency - USD EUR INR
from enum import Enum


class Currency(Enum):
    USD = 1
    EUR = 2
    INR = 3

# for currency in Currency:
#     print(currency)

print(Currency(1))

print(Currency(1).name)
print(Currency(1).value)


# print(Currency.USD)
# print(Currency.INR)
```
---

### /tips/module_1.py

```py
def method_1():
    print("method 1")

class ClassA:
    def class_method_1(self):
        print("class_method_1 method 1")

# print(__name__)

if __name__ == '__main__':
    method_1()
    ClassA().class_method_1()
```
---

### /tips/module_2.py

```py
import module_1

module_1.method_1()
module_1.ClassA().class_method_1()
```
---

### /tips/switch_alternatives.py

```py
week_days = {
    0 : 'Sunday',
    1 : 'Monday',
    2 : 'Tuesday'
    # You can fill rest of the stuff
}

print(week_days.get(7,'Invalid_day'))
```
---

# Learn Programming with Python

# Course Guide

## Introduction To Python Programming With Multiplication Table

### Step By Step Details
- Step 00 - Getting Started with Programming
- Step 01 - Introduction to Multiplication Table challenge
- Step 02 - Launch Python Shell - TODO
- Step 03 - Break Down Multiplication Table Challenge
- Step 04 - Python Expression - An Introduction
- Step 05 - Python Expression - Exercises
- Step 06 - Java Expression - Puzzles
- Step 07 - Printing output to console with Python
- Step 08 - Calling Functions in Python - Puzzles
- Step 09 - Advanced Printing output to console with Python
- Step 10 - Advanced Printing output to console with Python - Exercises and Puzzles
- Step 11 - Introduction to Variables in Python
- Step 12 - Introduction to Variables in Python - Puzzles
- Step 13 - Assignment Statement
- Step 14 - Tip - Using formatted strings in print method
- Step 15 - Using For Loop to Print Multiplication Table
- Step 16 - Using For Loop in Python - Puzzles
- Step 17 - Using For Loop in Python - Exercises
- Step 18 - Getting Started with Programming - Revise all Terminology


#### /01-first-python-project/input.py

```py
value = input("Enter a Value: ")
integer_value = int(value)
print("you entered ", integer_value)
print(type(integer_value))
```
---

#### /01-first-python-project/number_menu.py

```py
number1 = int(input("Enter Number1: "))
number2 = int(input("Enter Number2: "))

print("\n\n1 - Add")
print("2 - Subtract")
print("3 - Divide")
print("4 - Multiply")

choice = int(input("Choose Operation: "))

# print(number1 + number2)
# print(choice)
if choice==1:
    result = number1 + number2
elif choice==2:
    result = number1 - number2
elif choice==3:
    result = number1 / number2
elif choice==4:
    result = number1 * number2
else:
    result = "Invalid Choice"

print(result)
```
---



### Python Shell Code

```py
Last login: Wed May 16 14:30:51 on ttys001
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> number = 5
>>> value = 2.5
>>> type(number)
<class 'int'>
>>> type(5)
<class 'int'>
>>> type(2.5)
<class 'float'>
>>> type(2.55)
<class 'float'>
>>> type(5/2)
<class 'float'>
>>> type(4/2)
<class 'float'>
>>> 4/2
2.0
>>> 1 + 2
3
>>> i = 10
>>> j = 2
>>> i + j
12
>>> i - j
8
>>> i / j
5.0
>>> i * j
20
>>> i % 2
0
>>> value1 = 4.5
>>> value2 = 3.2
>>> value1 + value2
7.7
>>> value1 - value2
1.2999999999999998
>>> value1 / value2
1.40625
>>> value1 % value2
1.2999999999999998
>>> i + value1
14.5
>>> i - value1
5.5
>>> i / value1
2.2222222222222223
>>> 
>>> import os
>>> os.system('clear')

0
>>> i = 1
>>> i = i + 1
>>> i
2
>>> i += 1
>>> i
3
>>> i++
  File "<stdin>", line 1
    i++
      ^
SyntaxError: invalid syntax
>>> ++i
3
>>> i += 1
>>> i
4
>>> i -= 1
>>> i
3
>>> i /= 1
>>> i *= 2
>>> i
6.0
>>> type(i)
<class 'float'>
>>> number1 = 5
>>> number2 = 2
>>> number1/number2
2.5
>>> number1//number2
2
>>> number1 //= 2
>>> number1
2
>>> 5 ** 3
125
>>> pow(5,3)
125
>>> 5.6
5.6
>>> int(5.6)
5
>>> round(5.6)
6
>>> round(5.4)
5
>>> round(5.5)
6
>>> round(5.67, 1)
5.7
>>> round(5.678, 2)
5.68
>>> float(5)
5.0
>>> os.clear('system')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'os' has no attribute 'clear'
>>> os.system('clear')

0
>>> True
True
>>> False
False
>>> true
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'true' is not defined
>>> false
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'false' is not defined
>>> is_even = True
>>> is_odd = False
>>> i = 10
>>> i > 15
False
>>> i < 15
True
>>> i >= 15
False
>>> i >= 10
True
>>> i > 10
False
>>> i <= 10
True
>>> i < 10
False
>>> i == 10
True
>>> i == 11
False
>>> os.system('clear')

0
>>> i = 5
>>> if i>3:
...     print(f"{i} is greater than 3")
... 
5 is greater than 3
>>> i = 2
>>> if i>3:
...     print(f"{i} is greater than 3")
... 
>>> if i<10:
...   print(f"{i} is less than 10")
... 
2 is less than 10
>>> i = 15
>>> if i<10:
...   print(f"{i} is less than 10")
... 
>>> if(False):
...   print("False")
... 
>>> if(True):
...   print("True")
... 
True
>>> a = 5
>>> b = 7
>>> if(a>b):
...   print("a is greater than b")
... 
>>> a = 9
>>> if(a>b):
...   print("a is greater than b")
... 
a is greater than b
>>> os.system('clear')

0
>>> a = 1
>>> b = 2
>>> c = 3
>>> d = 5
>>> if a+b > c+d :
...    print("a+b > c +d")
... 
>>> a = 9
>>> if a+b > c+d :
...    print("a+b > c +d")
... 
a+b > c +d
>>> angle1 = 30
>>> angle2 = 20
>>> angle3 = 60
>>> if(angle1 + angle2 + angle3 = 180):
  File "<stdin>", line 1
    if(angle1 + angle2 + angle3 = 180):
                                ^
SyntaxError: invalid syntax
>>> if(angle1 + angle2 + angle3 == 180):
...      print("Valid Triangle")
... 
>>> angle2 = 90
>>> if(angle1 + angle2 + angle3 == 180):
...      print("Valid Triangle")
... 
Valid Triangle
>>> i = 2
>>> if(i%2==0): 
...   print("i is even")
... 
i is even
>>> i = 3
>>> if(i%2==0): 
...   print("i is even")
... 
>>> os.system('clear')

0
>>> True and False
False
>>> True and True
True
>>> True and False
False
>>> False and True
False
>>> False and False
False
>>> True or False
True
>>> False or True
True
>>> True or True
True
>>> False or False
False
>>> not True
False
>>> not(True)
False
>>> not False
True
>>> not(False)
True
>>> True ^ True
False
>>> True ^ False
True
>>> False ^ True
True
>>> False ^ False
False
>>> os.system('clear')

0
>>> i = 10
>>> j = 15
>>> if i%2==0 and j%2==0:
...   print("i and j are even")
... 
>>> j = 14
>>> if i%2==0 and j%2==0:
...   print("i and j are even")
... 
i and j are even
>>> if i%2==0 or j%2==0:
... 
  File "<stdin>", line 2
    
    ^
IndentationError: expected an indented block
>>> if i%2==0 or j%2==0:
...   print("atleast one of i and j are even")
... 
atleast one of i and j are even
>>> i = 15
>>> j
14
>>> if i%2==0 or j%2==0:
...   print("atleast one of i and j are even")
... 
atleast one of i and j are even
>>> j = 23
>>> if i%2==0 or j%2==0:
...   print("atleast one of i and j are even")
... 
>>> i
15
>>> if(True ^ False)
  File "<stdin>", line 1
    if(True ^ False)
                   ^
SyntaxError: invalid syntax
>>> if(True ^ False):
...     print("This will Print")
... 
This will Print
>>> if(False ^ True):
...     print("This will Print")
... 
This will Print
>>> if(True ^ True):
...     print("This will Print")
... 
>>> x = 5
>>> if not x == 6:
...   print("This")
... 
This
>>> x = 6
>>> if not x == 6:
...   print("This")
... 
>>> if x!=6:
...   print("This")
... 
>>> x=5
>>> if x!=6:
...   print("This")
... 
This
>>> if x=6:
  File "<stdin>", line 1
    if x=6:
        ^
SyntaxError: invalid syntax
>>> int(True)
1
>>> int(False)
0
>>> x = -6
>>> if x:
...   print("something")
... 
something
>>> bool(6)
True
>>> bool(-6)
True
>>> bool(0)
False
>>> os.system('clear')

0
>>> i = 2
>>> if i%2 == 0:
...   print("i is even");
... else:
...   print("i is odd");
... 
i is even
>>> i = 3
>>> if i%2 == 0:
...   print("i is even");
... else:
...   print("i is odd");
... 
i is odd
>>> if i==1:
...   print("i is 1")
... elif i==2:
...   print("i is 2")
... else:
...   print("i is not 1 or 2")
... 
i is not 1 or 2
>>> 

```


## Text in Python

### Step By Step Details
- Step 01 - Text in Python - Methods in str class ##EDIT
- Step 02 - Data Type Conversion - Puzzles
- Step 03 - Strings are immutable
- Step 04 - There is no seperate Character data type
- Step 05 - String module ##EDIT
- Step 06 - Exercise - is_vowel, print lower case and upper case characters
- Step 07 - String - Exercises and Puzzles
- Step 08 - String - Conclusion

### Python Shell Code

```py
Last login: Thu May 17 09:41:15 on ttys002
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> message = "Hello World"
>>> message = 'Hello World'
>>> message = 'Hello World"
  File "<stdin>", line 1
    message = 'Hello World"
                          ^
SyntaxError: EOL while scanning string literal
>>> message = "Hello World"
>>> type(message)
<class 'str'>
>>> message.upper()
'HELLO WORLD'
>>> message.lower()
'hello world'
>>> message = "hello"
>>> message.capitalize()
'Hello'
>>> "hello".capitalize()
'Hello'
>>> 'hello'.capitalize()
'Hello'
>>> 'hello'.islower()
True
>>> 'Hello'.islower()
False
>>> 'Hello'.istitle()
True
>>> 'hello'.istitle()
False
>>> 'hello'.isupper()
False
>>> 'Hello'.isupper()
False
>>> 'HELLO'.isupper()
True
>>> '123'.isdigit()
True
>>> 'A23'.isdigit()
False
>>> '2 3'.isdigit()
False
>>> '23'.isdigit()
True
>>> '23'.isalpha()
False
>>> '2A'.isalpha()
False
>>> 'ABC'.isalpha()
True
>>> 'ABC123'.isalnum()
True
>>> 'ABC 123'.isalnum()
False
>>> 'Hello World'.endswith('World')
True
>>> 'Hello World'.endswith('ld')
True
>>> 'Hello World'.endswith('old')
False
>>> 'Hello World'.endswith('Wo')
False
>>> 'Hello World'.startswith('Wo')
False
>>> 'Hello World'.startswith('He')
True
>>> 'Hello World'.startswith('Hell0')
False
>>> 'Hello World'.startswith('Hello')
True
>>> 'Hello World'.find('Hello')
0
>>> 'Hello World'.find('ello')
1
>>> 'Hello World'.find('Ello')
-1
>>> 'Hello World'.find('bello')
-1
>>> 'Hello World'.find('Ello')
-1
>>> os.system('clear')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'os' is not defined
>>> import os
>>> os.system('clear')

0
>>> str(True)
'True'
>>> bool('True')
True
>>> bool('true')
True
>>> bool('tru')
True
>>> bool('false')
True
>>> bool('False')
True
>>> bool('')
False
>>> str(123)
'123'
>>> str(12345)
'12345'
>>> str(12345.45678)
'12345.45678'
>>> int('45')
45
>>> int('45.56')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: '45.56'
>>> int('45dfsafk')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: '45dfsafk'
>>> int('45abc',16)
285372
>>> int('a',16)
10
>>> int('b',16)
11
>>> int('c',16)
12
>>> int('f',16)
15
>>> int('g',16)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 16: 'g'
>>> float("34.43")
34.43
>>> float("34.43rer")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: could not convert string to float: '34.43rer'
>>> os.system('clear')

0
>>> message = "Hello"
>>> message.upper()
'HELLO'
>>> message
'Hello'
>>> message = message.upper()
>>> message
'HELLO'
>>> message = "Hello"
>>> message.upper()
'HELLO'
>>> message_upper = message.upper()
>>> message = "ABC"
>>> message = message.lowercase()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'str' object has no attribute 'lowercase'
>>> message = message.lower()
>>> os.system('clear')
0
>>> message = "Hello World"
>>> message[0]
'H'
>>> type(message[0])
<class 'str'>
>>> type(message)
<class 'str'>
>>> message[0]
'H'
>>> message[1]
'e'
>>> message[2]
'l'
>>> message[3]
'l'
>>> message[100]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
>>> for ch in message:
...    print(ch)
... 
H
e
l
l
o
 
W
o
r
l
d
>>> os.system('clear')

0
>>> import string
>>> string.
string.Formatter(       string.ascii_uppercase  string.octdigits
string.Template(        string.capwords(        string.printable
string.ascii_letters    string.digits           string.punctuation
string.ascii_lowercase  string.hexdigits        string.whitespace
>>> string.ascii_letters
'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
>>> string.ascii_lowercase
'abcdefghijklmnopqrstuvwxyz'
>>> string.ascii_uppercase
'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
>>> string.digits
'0123456789'
>>> string.hexdigits
'0123456789abcdefABCDEF'
>>> string.punctuation
'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
>>> 'a' in string.ascii_letters
True
>>> string.ascii_letters
'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
>>> 'ab' in string.ascii_letters
True
>>> 'abc' in string.ascii_letters
True
>>> 'a' in string.ascii_letters
True
>>> '1' in '13579'
True
>>> '2' in '13579'
False
>>> '4' in '13579'
False
>>> char = 'a'
>>> vowel_string = 'aeiouAEIOU'
>>> char in vowel_string
True
>>> char = 'b'
>>> char in vowel_string
False
>>> vowel_string = 'AEIOU'
>>> char.upper() in vowel_string
False
>>> char = 'a'
>>> char.upper() in vowel_string
True
>>> vowel_string = 'aeiou'
>>> char.lower() in vowel_string
True
>>> char = 'A'
>>> char.lower() in vowel_string
True
>>> import string
>>> string.
string.Formatter(       string.ascii_uppercase  string.octdigits
string.Template(        string.capwords(        string.printable
string.ascii_letters    string.digits           string.punctuation
string.ascii_lowercase  string.hexdigits        string.whitespace
>>> string.ascii_uppercase
'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
>>> for char in string.ascii_uppercase:
...   print(char)
... 
A
B
C
D
E
F
G
H
I
J
K
L
M
N
O
P
Q
R
S
T
U
V
W
X
Y
Z
>>> for char in string.ascii_lowercase:
...   print(char)
... 
a
b
c
d
e
f
g
h
i
j
k
l
m
n
o
p
q
r
s
t
u
v
w
x
y
z
>>> for char in string.
string.Formatter(       string.ascii_uppercase  string.octdigits
string.Template(        string.capwords(        string.printable
string.ascii_letters    string.digits           string.punctuation
string.ascii_lowercase  string.hexdigits        string.whitespace
>>> for char in string.digits:
...   print(char)
... 
0
1
2
3
4
5
6
7
8
9
>>> vowel_string = 'aeiou'
>>> char.lower() in vowel_string
False
>>> 'b'.lower() not in vowel_string
True
>>> 'a'.lower() not in vowel_string
False
>>> '1'.lower() not in vowel_string
True
>>> '1'.isalpha() and '1'.lower() not in vowel_string
False
>>> char.isalpha() and char.lower() not in vowel_string
True
>>> char
'b'
>>> char = '1'
>>> char.isalpha() and char.lower() not in vowel_string
False
>>> os.system('clear')

0
>>> string_example = "This is a great thing"
>>> string_example.
string_example.capitalize(    string_example.join(
string_example.casefold(      string_example.ljust(
string_example.center(        string_example.lower(
string_example.count(         string_example.lstrip(
string_example.encode(        string_example.maketrans(
string_example.endswith(      string_example.partition(
string_example.expandtabs(    string_example.replace(
string_example.find(          string_example.rfind(
string_example.format(        string_example.rindex(
string_example.format_map(    string_example.rjust(
string_example.index(         string_example.rpartition(
string_example.isalnum(       string_example.rsplit(
string_example.isalpha(       string_example.rstrip(
string_example.isdecimal(     string_example.split(
string_example.isdigit(       string_example.splitlines(
string_example.isidentifier(  string_example.startswith(
string_example.islower(       string_example.strip(
string_example.isnumeric(     string_example.swapcase(
string_example.isprintable(   string_example.title(
string_example.isspace(       string_example.translate(
string_example.istitle(       string_example.upper(
string_example.isupper(       string_example.zfill(
>>> string_example.split()
['This', 'is', 'a', 'great', 'thing']
>>> for word in string_example.split():
...    print(word)
... 
This
is
a
great
thing
>>> string_example = "This\nis\n\ngreat\nthing"
>>> print(string_example)
This
is

great
thing
>>> string_example = "This\nis\na\ngreat\nthing"
>>> print(string_example)
This
is
a
great
thing
>>> string_example.split
string_example.split(       string_example.splitlines(  
>>> string_example.splitlines()
['This', 'is', 'a', 'great', 'thing']
>>> 1 + 2
3
>>> "1" + "2"
'12'
>>> "1" + 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: must be str, not int
>>> "ABC" + "DEF"
'ABCDEF'
>>> 1 * 20
20
>>> '1' * 20
'11111111111111111111'
>>> 'A' * 10
'AAAAAAAAAA'
>>> str = "test"
>>> str2 = "test1"
>>> str == str2
False
>>> str2 = "test"
>>> str == str2
True
>>> 
```


## Python Loops

### Step By Step Details
- Step 01 - For loop basics
- Step 02 - For loop exercise 1 - is_prime
- Step 03 - For loop exercise 2 - sum_upto_n
- Step 04 - For loop exercise 3 - sum of divisors 
- Step 05 - For loop exercise 4 - print a number triangle
- Step 06 - Introduction to while loop in Python
- Step 07 - While loop - Exercises
- Step 08 - Choosing a Loop - Menu Exercise
- Step 09 - Loops - Puzzles - break and continue

### PyCharm Code


#### /01-first-python-project/while_exercises.py

```py
# print_squares_upto_limit(30)
# //For limit = 30, output would be 1 4 9 16 25
#
# print_cubes_upto_limit(30)
# //For limit = 30, output would be 1 8 27

def print_squares_upto_limit(limit):
    i = 1
    while i * i < limit:
        print(i*i, end = " ")
        i = i + 1

def print_cubes_upto_limit(limit):
    i = 1
    while i * i * i < limit:
        print(i*i*i, end = " ")
        i = i + 1

print_cubes_upto_limit(80)
```
---

#### /01-first-python-project/number_menu_loop.py

```py
number1 = int(input("Enter Number1: "))
number2 = int(input("Enter Number2: "))

print("\n\n1 - Add")
print("2 - Subtract")
print("3 - Divide")
print("4 - Multiply")
print("5 - Exit")

choice = int(input("Choose Operation: "))

while(choice != 5):

    # print(number1 + number2)
    # print(choice)
    if choice==1:
        result = number1 + number2
    elif choice==2:
        result = number1 - number2
    elif choice==3:
        result = number1 / number2
    elif choice==4:
        result = number1 * number2
    else:
        result = "Invalid Choice"

    print(result)

    choice = int(input("Choose Operation: "))

print("Thank You")
```
---

#### /01-first-python-project/loop_puzzles.py

```py
# for i in range(1,11,2):
#    print(i, end=' ')

# for i in range(11,0,-1):
#     print(i,  end=' ')

#
# i = 5
# while i*i < 10:
#     print(i)
# print("done")
#
#
# i = 2
# while i*i < 10:
#     print(i,  end=' ')
#     i = i + 1
# print("done")

# for i in range(1,11):
#    if i==5:
#       break
#    print(i,  end=' ')
# print("done")
# for i in range(2,11):
#    if i%2:
#       break
#    print(i ,  end=' ')
#
# print("done")
# for i in range(1,11):
#    if i%2:
#      continue
#    print(i ,  end=' ')
#
# print("done")

for i in range(1,11):
   if i%2!=0:
     continue
   print(i ,  end=' ')
print("done")
```
---

#### /01-first-python-project/for_exercises.py

```py
# is_prime(9); //Is a number Prime?
# //H: 5 => True, 7 => True, 11 => True, 6 => False
def is_prime(number):

    if(number < 2):
        return False

    # check if number is divisible by 2 to number - 1
    for divisor in range(2,number):
        if number % divisor == 0:
            return False

    return True

# print(is_prime(15));

# sum_upto_n(6)
# Sum of numbers upto n?
# 1 + 2 + 3 + 4 + 5 + 6

def sum_upto_n(number):

    sum = 0

    for i in range(1, number+1):
        sum = sum + i

    return sum

# print(sum_upto_n(6))
# print(sum_upto_n(10))

def calculate_sum_of_divisors(number):
    sum = 0

    if(number < 2):
        return sum
    for divisor in range(1,number+1):
        if number % divisor == 0:
            sum = sum + divisor

    return sum

# print(calculate_sum_of_divisors(6))
# print(calculate_sum_of_divisors(15))

def print_a_number_triangle(number):
    for j in range(1, number + 1):
        for i in range(1, j + 1):
            print(i, end=' ')
        print()
print_a_number_triangle(6)
```


### Python Shell Code

```py
Last login: Thu May 17 09:53:08 on ttys002
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> for i in range(1,11):
...   print(i)
... 
1
2
3
4
5
6
7
8
9
10
>>> for ch in "Hello World":
...   print(ch)
... 
H
e
l
l
o
 
W
o
r
l
d
>>> for word in "Hello World".split():
...   print(word)
... 
Hello
World
>>> for item in (3, 6, 9):
...   print(item)
... 
3
6
9
>>> os.system('clear')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'os' is not defined
>>> import os
>>> os.system('clear')

0
>>> i = 5
>>> if i == 5:
...   print("i is 5")
... 
i is 5
>>> i = 0
>>> while i < 5:
...   print(i)
... 
0
0
0
0
0
0
0
0
^CTraceback (most recent call last):
  File "<stdin>", line 2, in <module>
KeyboardInterrupt
>>> 
KeyboardInterrupt
>>> while i < 5:
...   print(i)
...   i = i + 1
... 
0
1
2
3
4
>>> i = 0
>>> while i < 5:
...   print(i, end=" ")
...   i = i + 1
... 
0 1 2 3 4 >>> for i in range(0,5): print(i)
... 
0
1
2
3
4
>>> os.system('clear')

0
>>> 
```


# Tips For Beginners
- Tip 1 - Using Predefined Python Modules
- Tip 2 - Loop - Getting Index Element
- Tip 3 - Python is Strongly Typed and Dynamic Language
- Tip 4 - Beginners Mistakes - Shadowing
- Tip 9 - Defining Equality for Classes
- Tip 5 - Beginners Mistakes - Indentation
- Tip 6 - PEP8 - Python Style Guide
- Tip 7 - PEP20 - Zen of Python

## Introduction To Object Oriented Programming

### Step By Step Details
- Step 00 - Introduction to Object Oriented Programming - Section Overview
- Step 01 - Introduction to Object Oriented Programming - Basics
- Step 02 - Introduction to Object Oriented Programming - Terminology - Class, Object, State and Behavior
- Step 03 - Introduction to Object Oriented Programming - Exercise - Online Shopping System and Person
- Step 04 - First Class and Object - Country class
- Step 05 - Create Motor Bike Python Class and a couple of objects
- Step 06 - Class and Objects - a few Puzzles
- Step 07 - Constructor for MotorBike class
- Step 08 - Constructor for Book class - Exercise
- Step 09 - Constructors - Puzzles
- Step 10 - Class and Objects - Methods and Behavior
- Step 11 - Exercise - Enhance Book class with copies
- Step 12 - Class and Objects - Methods and Behavior - Puzzles on self
- Step 13 - Advantages of Encapsulation
- Step 14 - Everything is Object in Python

### PyCharm Code

#### /02-oops/book.py

```py
class Book:
    def __init__(self, name, copies=0):
        self.name = name
        self.copies = copies

    def increase_copies(self, how_much):
        self.copies += how_much

    def decrease_copies(self, how_much):
        self.copies -= how_much
# copies
# increase_copies
# decrease_copies

the_art_of_computer_programming = Book('The Art of Computer Programming')
learning_python = Book('Learning Python in 100 Steps', 100)
learning_restful_services = Book('Learning RestFul Service in 50 Steps')

# print(the_art_of_computer_programming.name)
# print(learning_python.name)
# print(learning_restful_services.name)

learning_python.increase_copies(25)
learning_python.decrease_copies(10)
learning_python.copies = 50

print(learning_python.copies)
```
---

#### /02-oops/country.py

```py
from operator import attrgetter

class Country:

    def __init__(self, name, population, area):
        self.name = name
        self.population = population
        self.area = area

    def __repr__(self):
        return repr((self.name,self.population,self.area))
countries = [Country('India',1200,100),
             Country('China', 1400, 200),
             Country('USA', 120, 300)]

countries.append(Country('Russia',80,900))

countries.sort(key=attrgetter('population'), reverse=True)
print(max(countries, key=attrgetter('population')))
print(min(countries, key=attrgetter('population')))
print(min(countries, key=attrgetter('area')))
print(max(countries, key=attrgetter('area')))

print(countries)
```
---

#### /02-oops/motor_bike.py

```py
# Class
class MotorBike:
    def __init__(self, speed):
        self.speed = speed #State

    # Behavior
    def increase_speed(self, how_much):
        self.speed += how_much

    # Behavior
    def decrease_speed(self, how_much):
        if(self.speed-how_much>0):
            self.speed -= how_much
        else:
            print("Get a life")
# instance 1 or object 1
honda = MotorBike(50)

# instance 2 or object 2
ducati = MotorBike(250)

# print(honda)
# print(ducati)
#

# State changes through behavior of the object
honda.increase_speed(150)
ducati.increase_speed(25)

# State changes through behavior of the object
honda.decrease_speed(50)
ducati.decrease_speed(25)

honda.decrease_speed(350)

print(honda.speed)
print(ducati.speed)

#
# honda.speed = 150
# print(honda.speed)
# print(ducati.speed)
```
---

#### /02-oops/planet.py

```py
class Planet(object):
    def rotate(self):
        print("rotate")

    def revolve(self):
        print("revolve")

    def rotate_and_revolve(self):
        self.rotate()
        self.revolve()
earth = Planet()
earth.rotate_and_revolve()
```
---


### Python Shell Code

```py
>>> class Country: 
...     pass
... 
>>> india = Country()
>>> usa = Country()
>>> netherlands = Country()
>>> india.name = 'India'
>>> india.capital = 'New Delhi'
>>> usa.name = 'USA'
>>> usa.capital = 'Washington'
>>> netherlands.name = 'Netherlands'
>>> netherlands.capital = 'Amsterdam'
>>> india.name
'India'
>>> class Planet: pass
... 
>>> earth = Planet()
>>> earth = new Planet()
  File "<stdin>", line 1
    earth = new Planet()
                     ^
SyntaxError: invalid syntax
>>> earth = Planet('Earth')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: object() takes no parameters
>>> earth.name
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Planet' object has no attribute 'name'
>>> earth.name = 'The Earth'
>>> earth.name
'The Earth'
>>> venus = Planet()
>>> venus.name
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Planet' object has no attribute 'name'
>>> venus.name = 'Venus'
>>> venus.name
'Venus'
>>> venus.do_something()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Planet' object has no attribute 'do_something'
>>> os.system('clear')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'os' is not defined
>>> import os
>>> os.system('clear')

0
>>> class Planet:
...    def __init__(): pass
... 
>>> Planet()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() takes 0 positional arguments but 1 was given
>>> class Planet:
...    def __init__(self): pass
... 
>>> Planet()
<__main__.Planet object at 0x10426bc88>
>>> class Planet:
...    def __init__(self): pass
...    def __init__(self, name): pass
... 
>>> Planet()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() missing 1 required positional argument: 'name'
>>> class Planet:
...    def __init__(self, name): pass
...    def __init__(self): pass
... 
>>> Planet()
<__main__.Planet object at 0x10426bdd8>
>>> Planet("Jupiter")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() takes 1 positional argument but 2 were given
>>> class Planet:
...    def __init__(self, name="Earth"): pass
... 
>>> Planet()
<__main__.Planet object at 0x10426beb8>
>>> Planet("Jupiter")
<__main__.Planet object at 0x10426bef0>
>>> class Planet:
...    def __init__(self, name="Earth"):
...        self.speed = 10
...        self.name = name
...        self.distance_from_sun = 10000
... 
>>> earth = Planet()
>>> earth.name
'Earth'
>>> earth.speed
10
>>> earth.distance_from_sun
10000
>>> os.system('clear')

0
>>> class Planet:
...    def revolve(): pass
... 
>>> earth = Planet()
>>> earth.revolve()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: revolve() takes 0 positional arguments but 1 was given
>>> class Planet:
...    def revolve(self): pass
... 
>>> earth = Planet()
>>> earth.revolve()
Revolve
>>> os.system('clear')

0
>>> 5
5
>>> type(5)
<class 'int'>
>>> type(True)
<class 'bool'>
>>> type('Hello')
<class 'str'>
>>> 'Hello'.upper()
'HELLO'
>>> type(5.5)
<class 'float'>
>>> def do_something(): pass
... 
>>> do_something
<function do_something at 0x104275488>
>>> def do_something():
...    print("something")
... 
>>> do_something
<function do_something at 0x104275510>
>>> do_something()
something
>>> test = do_something
>>> test
<function do_something at 0x104275510>
>>> test()
something
>>> 

```


## Python Data Structures

### Step By Step Details
- Step 01 - Python Data Structures - Why do we need them?
- Step 02 - Operations on List Data Structure ##EDIT
- Step 03 - Exercise with List - Student class
- Step 04 - Puzzles with Strings Lists  ##
- Step 05 - List Slicing
- Step 06 - List Sorting, Looping and Reversing ##
- Step 07 - List as a Stack and Queue ##
- Step 08 - List with a custom class - Country and representation
- Step 08 - List with a custom class - Part 2 - sorting, max and min
- Step 09 - List Comprehension ##
- Step 10 - Introduction to Set ##
- Step 11 - Introduction to Dictionary ##
- Step 12 - Exercise with Dictionary - Word and Character Occurances
- Step 13 - Puzzles with Data Structures ##

### PyCharm Code

#### /02-oops/Student.py

```py
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def get_number_of_marks(self):
        return len(self.marks)

    def get_total_sum_of_marks(self):
        return sum(self.marks)

    def determine_maximum_mark(self):
        return max(self.marks)

    def determine_minimum_mark(self):
        return min(self.marks)

    def determine_average(self):
        return self.get_total_sum_of_marks()/self.get_number_of_marks()

    def add_new_mark(self, new_mark):
        self.marks.append(new_mark)

    def remove_mark_at_index(self, index):
        del self.marks[index]
student = Student ("Ranga", [23, 45, 56, 75])
number = student.get_number_of_marks()

sum_of_marks = student.get_total_sum_of_marks()
maximum_mark = student.determine_maximum_mark()
minimum_mark = student.determine_minimum_mark()
average = student.determine_average()
student.add_new_mark(35)
student.remove_mark_at_index(2)
print(student.marks)
print(f"""Student[
    number_of_marks-{number} 
    sum_of_marks-{sum_of_marks}
    max-{maximum_mark} 
    min-{minimum_mark} 
    avg-{average} ] """)
```
---

#### /02-oops/word_count.py

```py
str = "This is an awesome occasion. This has never happened before."

# key:value

char_occurances = {} #[]

for char in str:
    char_occurances[char] = char_occurances.get(char, 0) + 1

print(char_occurances)

word_occurances = {} #[]

for word in str.split():
    word_occurances[word] = word_occurances.get(word, 0) + 1

print(word_occurances)
```
---



### Python Shell Code

```py
Last login: Fri May 18 14:08:00 on ttys004
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> mark1 = 45
>>> mark2 = 54
>>> mark3 = 80
>>> mark1 + mark2 + mark3
179
>>> (mark1 + mark2 + mark3)/3
59.666666666666664
>>> mark4 = 43
>>> (mark1 + mark2 + mark3 + mark4)/3
74.0
>>> (mark1 + mark2 + mark3 + mark4)/4
55.5
>>> marks = [45, 54, 80]
>>> sum(marks)
179
>>> sum(marks)/len(marks)
59.666666666666664
>>> marks.append(43)
>>> sum(marks)/len(marks)
55.5
>>> type(marks)
<class 'list'>
>>> import os
>>> os.system('clear')

0
>>> marks = [23,56,67]
>>> sum(marks)
146
>>> max(marks)
67
>>> min(marks)
23
>>> len(marks)
3
>>> marks.append(76)
>>> marks
[23, 56, 67, 76]
>>> marks.insert(2, 60)
>>> marks
[23, 56, 60, 67, 76]
>>> marks.remove(60)
>>> 55 in marks
False
>>> 56 in marks
True
>>> marks.index(67)
2
>>> marks
[23, 56, 67, 76]
>>> marks.index(69)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: 69 is not in list
>>> for mark in marks:
...   print(mark)
... 
23
56
67
76
>>> os.system('clear')

0
>>> animals = ['Cat', 'Dog','Elephant']
>>> len(animals)
3
>>> sum(animals)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>> animals.append('Fish')
>>> animals
['Cat', 'Dog', 'Elephant', 'Fish']
>>> animals.remove('Dog')
>>> animals
['Cat', 'Elephant', 'Fish']
>>> animals[2]
'Fish'
>>> animals[1]
'Elephant'
>>> animals[0]
'Cat'
>>> animals[4]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
>>> del animals[2]
>>> animals
['Cat', 'Elephant']
>>> animals.extend('Fish')
>>> animals
['Cat', 'Elephant', 'F', 'i', 's', 'h']
>>> animals.append('Fish')
>>> animals
['Cat', 'Elephant', 'F', 'i', 's', 'h', 'Fish']
>>> animals.extend(['Giraffe', 'Horse'])
>>> animals
['Cat', 'Elephant', 'F', 'i', 's', 'h', 'Fish', 'Giraffe', 'Horse']
>>> animals = animals + ['Jackal','Kangaroo']
>>> animals
['Cat', 'Elephant', 'F', 'i', 's', 'h', 'Fish', 'Giraffe', 'Horse', 'Jackal', 'Kangaroo']
>>> animals += ['Lion','Monkey']
>>> animals
['Cat', 'Elephant', 'F', 'i', 's', 'h', 'Fish', 'Giraffe', 'Horse', 'Jackal', 'Kangaroo', 'Lion', 'Monkey']
>>> animals.append(10)
>>> animals
['Cat', 'Elephant', 'F', 'i', 's', 'h', 'Fish', 'Giraffe', 'Horse', 'Jackal', 'Kangaroo', 'Lion', 'Monkey', 10]
>>> os.system('clear')

0
>>> numbers = ['Zero','One','Two','Three','Four','Five','Six','Seven','Eight','Nine']
>>> len(numbers)
10
>>> number[2]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'number' is not defined
>>> numbers[2]
'Two'
>>> numbers[2:6]
['Two', 'Three', 'Four', 'Five']
>>> numbers[:6]
['Zero', 'One', 'Two', 'Three', 'Four', 'Five']
>>> numbers[3:]
['Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine']
>>> numbers[1:8:2]
['One', 'Three', 'Five', 'Seven']
>>> numbers[1:8:3]
['One', 'Four', 'Seven']
>>> numbers[::3]
['Zero', 'Three', 'Six', 'Nine']
>>> numbers[::-1]
['Nine', 'Eight', 'Seven', 'Six', 'Five', 'Four', 'Three', 'Two', 'One', 'Zero']
>>> numbers[::-3]
['Nine', 'Six', 'Three', 'Zero']
>>> del numbers[3:]
>>> numbers
['Zero', 'One', 'Two']
>>> numbers = ['Zero','One','Two','Three','Four','Five','Six','Seven','Eight','Nine']
>>> del numbers[5:7]
>>> numbers = ['Zero','One','Two','Three','Four','Five','Six','Seven','Eight','Nine']
>>> numbers[3:7] = [3,4,5,6]
>>> numbers
['Zero', 'One', 'Two', 3, 4, 5, 6, 'Seven', 'Eight', 'Nine']
>>> os.system('clear')

0
>>> numbers = ['Zero','One','Two','Three','Four','Five','Six','Seven','Eight','Nine']
>>> numbers.reverse()
>>> numbers
['Nine', 'Eight', 'Seven', 'Six', 'Five', 'Four', 'Three', 'Two', 'One', 'Zero']
>>> numbers = ['Zero','One','Two','Three','Four','Five','Six','Seven','Eight','Nine']
>>> numbers
['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine']
>>> reversed(numbers)
<list_reverseiterator object at 0x109560ba8>
>>> for number in reversed(numbers):
...    print(number)
... 
Nine
Eight
Seven
Six
Five
Four
Three
Two
One
Zero
>>> numbers
['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine']
>>> numbers.sort()
>>> numbers
['Eight', 'Five', 'Four', 'Nine', 'One', 'Seven', 'Six', 'Three', 'Two', 'Zero']
>>> numbers = ['Zero','One','Two','Three','Four','Five','Six','Seven','Eight','Nine']
>>> for number in sorted(numbers):
...   print(number)
... 
Eight
Five
Four
Nine
One
Seven
Six
Three
Two
Zero
>>> numbers
['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine']
>>> for number in sorted(numbers, key=len):
...   print(number)
... 
One
Two
Six
Zero
Four
Five
Nine
Three
Seven
Eight
>>> for number in sorted(numbers, key=len, reverse=True):
...   print(number)
... 
Three
Seven
Eight
Zero
Four
Five
Nine
One
Two
Six
>>> numbers.sort(key=len)
>>> numbers
['One', 'Two', 'Six', 'Zero', 'Four', 'Five', 'Nine', 'Three', 'Seven', 'Eight']
>>> numbers.sort(key=len, reverse=True)
>>> numbers
['Three', 'Seven', 'Eight', 'Zero', 'Four', 'Five', 'Nine', 'One', 'Two', 'Six']
>>> os.system('clear')

0
>>> numbers = []
>>> numbers.append(1)
>>> numbers.append(2)
>>> numbers.append(3)
>>> numbers.append(4)
>>> numbers.pop()
4
>>> numbers
[1, 2, 3]
>>> numbers.pop()
3
>>> numbers
[1, 2]
>>> numbers.append(10)
>>> numbers.pop()
10
>>> numbers
[1, 2]
>>> numbers = []
>>> numbers.append(1)
>>> numbers.append(2)
>>> numbers.append(3)
>>> numbers.append(4)
>>> numbers.pop(0)
1
>>> numbers
[2, 3, 4]
>>> numbers.pop(0)
2
>>> numbers
[3, 4]
>>> numbers.append(10)
>>> numbers.pop(0)
3
>>> numbers.pop(0)
4
>>> numbers.pop(0)
10
>>> numbers
[]
>>> os.system('clear')

0
>>> numbers = ['Zero', 'One','Two','Three','Four','Five','Six','Seven', 'Eight','Nine']
>>> numbers_length_four=[]
>>> for number in numbers:
...    if len(number)== 4:
...      numbers_length_four.append(number)
... 
>>> numbers_length_four
['Zero', 'Four', 'Five', 'Nine']
>>> numbers_length_four = [ number for number in numbers  ]
>>> numbers_length_four
['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine']
>>> numbers_length_four = [ len(number) for number in numbers  ]
>>> numbers_length_four
[4, 3, 3, 5, 4, 4, 3, 5, 5, 4]
>>> numbers_length_four = [ number.upper() for number in numbers  ]
>>> numbers_length_four
['ZERO', 'ONE', 'TWO', 'THREE', 'FOUR', 'FIVE', 'SIX', 'SEVEN', 'EIGHT', 'NINE']
>>> numbers_length_four = [ number for number in numbers if len(number)==4 ]
>>> numbers_length_four
['Zero', 'Four', 'Five', 'Nine']
>>> values = [3, 6, 9, 1, 4, 15, 6, 3]
>>> values_even = [ value for value in values if value%2==0]
>>> values_even
[6, 4, 6]
>>> values_odd = [ value for value in values if value%2==1]
>>> values_odd
[3, 9, 1, 15, 3]
>>> os.system('clear')

0
>>> numbers = [1,2,3,2,1]
>>> numbers
[1, 2, 3, 2, 1]
>>> numbers_set = set(numbers)
>>> numbers_set
{1, 2, 3}
>>> numbers_set.add(3)
>>> numbers_set
{1, 2, 3}
>>> numbers_set.add(4)
>>> numbers_set
{1, 2, 3, 4}
>>> numbers_set.add(0)
>>> numbers_set
{0, 1, 2, 3, 4}
>>> numbers_set.remove(0)
>>> numbers_set
{1, 2, 3, 4}
>>> numbers_set[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support indexing
>>> 1 in numbers_set
True
>>> 5 in numbers_set
False
>>> min(numbers_set)
1
>>> max(numbers_set)
4
>>> sum(numbers_set)
10
>>> len(numbers_set)
4
>>> numbers_1_to_5_set = set(range(1,6))
>>> numbers_1_to_5_set
{1, 2, 3, 4, 5}
>>> numbers_4_to_10_set = set(range(4,11))
>>> numbers_4_to_10_set
{4, 5, 6, 7, 8, 9, 10}
>>> numbers_1_to_5_set + numbers_4_to_10_set
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'set' and 'set'
>>> numbers_1_to_5_set | numbers_4_to_10_set
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
>>> numbers_1_to_5_set & numbers_4_to_10_set
{4, 5}
>>> numbers_1_to_5_set - numbers_4_to_10_set
{1, 2, 3}
>>> numbers_4_to_10_set - numbers_1_to_5_set
{6, 7, 8, 9, 10}
>>> os.system('clear')

0
>>> occurances = dict(a=5 b=6 c=8)
  File "<stdin>", line 1
    occurances = dict(a=5 b=6 c=8)
                          ^
SyntaxError: invalid syntax
>>> occurances = dict(a=5,b=6,c=8)
>>> occurances
{'a': 5, 'b': 6, 'c': 8}
>>> type(occurances)
<class 'dict'>
>>> occurances['d'] = 15
>>> occurances
{'a': 5, 'b': 6, 'c': 8, 'd': 15}
>>> occurances['d'] = 10
>>> occurances
{'a': 5, 'b': 6, 'c': 8, 'd': 10}
>>> occurances['d']
10
>>> occurances['e']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'e'
>>> occurances.get('d')
10
>>> occurances.get('e')
>>> occurances.get('e', 10)
10
>>> occurances
{'a': 5, 'b': 6, 'c': 8, 'd': 10}
>>> occurances.keys()
dict_keys(['a', 'b', 'c', 'd'])
>>> occurances.values()
dict_values([5, 6, 8, 10])
>>> occurances.items()
dict_items([('a', 5), ('b', 6), ('c', 8), ('d', 10)])
>>> for (key,value) in occurances.items():
...    print(f"{key} {value}")
... 
a 5
b 6
c 8
d 10
>>> occurances['a']=0
>>> occurances
{'a': 0, 'b': 6, 'c': 8, 'd': 10}
>>> del occurances['a']
>>> occurances
{'b': 6, 'c': 8, 'd': 10}
>>> os.system('clear'
... )

0
>>> str = "This is an awesome occasion. This has never happened before."
>>> squares_first_ten_numbers = [  i*i for i in range(1,11) ]
>>> type(squares_first_ten_numbers)
<class 'list'>
>>> squares_first_ten_numbers_set = set(squares_of_first_10_numbers)
>>> squares_first_ten_numbers_set = { i*i for i in range(1,11)}
>>> type(squares_first_ten_numbers_set)
<class 'set'>
>>> squares_first_ten_numbers_dict = { i:i*i for i in range(1,11)}
>>> type(squares_first_ten_numbers_dict)
<class 'dict'>
>>> squares_first_ten_numbers_dict
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81, 10: 100}
>>> type([])
<class 'list'>
>>> type({})
<class 'dict'>
>>> type(set())
<class 'set'>
>>> type({1})
<class 'set'>
>>> type({'A':5})
<class 'dict'>
>>> type(())
<class 'tuple'>
>>> type((1,2,3))
<class 'tuple'>
>>> 
```


## Object Oriented Programming Again

### Step By Step Details
- Step 01 - OOPS Basics Revised
- Step 02 - Designing a Fan Class
- Step 03 - Object Composition - Book and Reviews
- Step 04 - Why do we need Inheritance
- Step 05 - All classes in Python 3 inherit from object
- Step 06 - Multiple Inheritance ##
- Step 07 - Creating and Using an Abstract Class
- Step 08 - Template Method Pattern with Recipe Class
- Step 09 - A Quick Revision

### PyCharm Code

#### /06-oops-advanced/amphibian.py

```py
class LandAnimal:
    def __init__(self):
        super().__init__()
        self.walking_speed = 5

    def increase_walking_speed(self, how_much):
        self.walking_speed += how_much

class WaterAnimal:
    def __init__(self):
        super().__init__()
        self.swimming_speed = 10

    def increase_swimming_speed(self, how_much):
        self.swimming_speed += how_much

class Amphibian(WaterAnimal, LandAnimal):
    def __init__(self):
        super().__init__()
amphibian = Amphibian()
amphibian.increase_swimming_speed(25)
amphibian.increase_walking_speed(50)
print(amphibian.swimming_speed)
print(amphibian.walking_speed)
```
---

#### /06-oops-advanced/animal.py

```py
from abc import ABC, abstractmethod

class AbstractAnimal(ABC):
    @abstractmethod
    def bark(self): pass

class Dog(AbstractAnimal):
    def bark(self):
        print("Bow Bow")

print(Dog().bark())
```
---

#### /06-oops-advanced/book_reviews.py

```py
class Book(object):
    def __init__(self, id, name, author):
        self.id = id
        self.name = name
        self.author = author
        self.reviews = []

    def __repr__(self):
        return repr((self.id,self.name,self.author,self.reviews))

    def add_review(self, review):
        self.reviews.append(review)
class Review:
    def __init__(self, id, description, rating):
        self.id = id
        self.description = description
        self.rating = rating

    def __repr__(self):
        return repr((self.id,self.description,self.rating))
book = Book(123, 'Object Oriented Programming with Python', 'Ranga')

# book.add_review()
book.add_review(Review(10, "Great Book", 5))
book.add_review(Review(101, "Awesome", 5))

print(book)
```
---

#### /06-oops-advanced/fan.py

```py
# State

# make
# radius
# color
# speed
# is_on

# Behavior

# switch_on
# switch_off
# increase_speed
# decrease_speed

class Fan:
    def __init__(self, make, radius, color):
        self.make = make
        self.radius = radius
        self.color = color
        self.speed = 0
        self.is_on = False

    def __repr__(self):
        return repr((self.make,self.radius,self.color,self.speed,self.is_on))

    def switch_on(self):
        self.is_on = True
        self.speed = 3

    def switch_off(self):
        self.is_on = False
        self.speed = 0

# increase_speed
# decrease_speed
fan = Fan('Manufacturer 1', 5, 'Green')
fan.switch_on()
print(fan)
fan.switch_off()
print(fan)
```
---

#### /06-oops-advanced/person_inheritance.py

```py
class Person:
    def __init__(self,name, email):
        self.name = name
        self.email = email

    def __repr__(self):
        return repr((self.name,self.email))
class Student(Person):
    def __init__(self, name, email, college, cls):
        super().__init__(name,email)
        self.college = college
        self.cls = cls

    def __repr__(self):
        return repr((super().__repr__(), self.college,self.cls))

person = Person('Ranga','in28minutes@gmail.com')
print(person)

student = Student('Ranga','in28minutes@gmail.com', 'Stanford', 'Algorithms' )
print(student)
# Person
# name, email
# Student
# college, class
# Employee
# title, employer
```
---

#### /06-oops-advanced/recipe.py

```py
from abc import ABC, abstractmethod
class AbstractRecipe(ABC):

    def execute(self):
        self.prepare()
        self.recipe()
        self.cleanup()

    @abstractmethod
    def prepare(self): pass

    @abstractmethod
    def recipe(self): pass

    @abstractmethod
    def cleanup(self): pass

class Recipe1(AbstractRecipe):

    def prepare(self):
        print('do the dishes')
        print('get raw materials')

    def recipe(self):
        print('execute the steps')

    def cleanup(self): pass
class MicrowaveRecipe(AbstractRecipe):

    def prepare(self):
        print('do the dishes')
        print('get raw materials')
        print('switch on microwave')

    def recipe(self):
        print('execute the steps')

    def cleanup(self):
        print('switch off microwave')

MicrowaveRecipe().execute()
```
---


### Python Shell Code
```py
Last login: Fri May 18 15:27:46 on ttys003
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> class Animal:
...   def bark():
...     print("bark")
... 
>>> animal = Animal()
>>> animal.bark()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: bark() takes 0 positional arguments but 1 was given
>>> class Animal:
...   def bark(self):
...     print("bark")
... 
>>> animal = Animal()
>>> animal.bark()
bark
>>> class Pet:
...   def bark(self):
...     print("bark")
...   def groom(self):
...     print("groom")
... 
>>> pet = Pet()
>>> pet.bark()
bark
>>> pet.groom()
groom
>>> class Pet(Animal):
...   def groom(self):
...     print("groom")
... 
>>> dog = Pet()
>>> os.system('clear')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'os' is not defined
>>> import os
>>> os.system('clear')

0
>>> 
```


## Error Handling with Python

### Step By Step Details
- Step 01 - Introduction to Error Handling - Your Thought Process during Error Handling
- Step 02 - Basics of Exception Hierarchy
- Step 03 - Basics of Error Handling - try except
- Step 04 - Handling Multiple Errors with Multiple except blocks
- Step 05 - Error Handling - Puzzles - Exception Details and 
- Step 06 - Error Handling - finally and else
- Step 07 - Error Handling - Puzzles 2
- Step 08 - Raising Exceptions
- Step 09 - Raising Custom Exceptions
- Step 10 - Exception Handling Best Practices

### PyCharm Code

#### /04-exception-handling/currency.py

```py
#USD 20
#USD 30
#USD 50
#INR 500
class CurrenciesDoNotMatchError(Exception):
    def __init__(self,message):
        super().__init__(message)
class Currency:
    def __init__(self, currency, amount):
        self.currency = currency
        self.amount = amount

    def __repr__(self):
        return repr((self.currency,self.amount))

    def __add__(self, other):
        if self.currency != other.currency:
            #raise Exception("Currencies Do Not Match")
            raise CurrenciesDoNotMatchError(self.currency + " " + other.currency)
        total_amount = self.amount + other.amount
        return Currency(self.currency, total_amount)
value1 = Currency("USD", 20)
value2 = Currency("INR", 30)
print(value1 + value2)
```
---

#### /04-exception-handling/exception_handling_basics.py

```py
# Open File/Resource

try:
    # Business Logic to read
    i = 0 # Not hardcoded, getting a input from user
    j = 10/i
    values = [1,2]
    sum(values)
except TypeError:
    print("TypeError")
    j = 10
except ZeroDivisionError:
    print("ZeroDivisionError")
    j = 0
except:
    print("OtherError")
    j = 5
else:
    print("Else")
finally:
    # Close
    print("Finally")

print(j)
print("End")
```
---

#### /04-exception-handling/exception_handling_puzzles.py

```py
# try:
#     10/0
# except TypeError:
#     print("TypeError")
# except ZeroDivisionError:
#     print("ZeroDivisionError")
#
# print("End")

# try:
#     10/0
# except object:
#     print("ZeroDivisionError")
# # catching classes that do not inherit from BaseException is not allowed
# print("End")

# try:
#     10/0
# except BaseException:
#     print("BaseException")
#
# print("End")

# try:
#     10/0
# except Exception:
#     print("Exception")

# try:
#     sum([1, '1'])
# except (ZeroDivisionError, TypeError):
#     print("Exception")
#
# print("End")

# try:
#     sum([1,'1'])
# except (ZeroDivisionError, TypeError):
#     print("Exception")
#
# print("End")

try:
    sum([1,'1'])
except TypeError as error:
    print(error)
print("End")
```
---



### Python Shell Code

```py
Last login: Sat May 19 09:06:10 on ttys000
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 1/0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> i = 0
>>> j = 10/i
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> 2 + '2'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>> values = [1,'2']
>>> sum(values)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>> value
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'value' is not defined
>>> values.non_existing
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'list' object has no attribute 'non_existing'
>>> values.non_existing()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'list' object has no attribute 'non_existing'
>>> import builtins
>>> help(builtins)

>>> help(builtins)

>>> k = 10/non_existing_variable
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'non_existing_variable' is not defined
>>> 10/0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>>     values = [1,'1']
  File "<stdin>", line 1
    values = [1,'1']
    ^
IndentationError: unexpected indent
>>>     sum(values)
  File "<stdin>", line 1
    sum(values)
    ^
IndentationError: unexpected indent
>>> values = [1,'1']
>>> sum(values)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>> import builtins
>>> help(builtins)

>>> 
```


## Final Tips
- Tip 1 - Math Module and Decimal Class
- Tip 2 - Statistics Module - find mean and median
- Tip 3 - Collections Module - deque for Queue and Stack
- Tip 4 - Date Module
- Tip 5 - Methods and Arguments - Basics
- Tip 6 - Methods and Arguments - Keyword Arguments
- Tip 7 - Methods and Arguments - Unpacking Lists and Dictionaries
- Tip 8 - Creating Custom Modules and Using Them

### PyCharm Code
#### /05-tips/all_about_methods.py

```py
def example_method(mandatory_parameter, default_parameter="Default"
                   , *args, **kwargs):
    print(f"""
        mandatory_parameter = {mandatory_parameter} {type(mandatory_parameter)}
        default_parameter = {default_parameter} {type(default_parameter)}
        args = {args} {type(args)}
        kwargs = {kwargs} {type(kwargs)}
        """)

# example_method() #example_method() missing 1 required positional argument
# example_method(mandatory_parameter=15)  #example_method(15)
# example_method(25,"Some String")
# example_method(25,"String 1","String 2","String 3")
# example_method(25,"String 1","String 2","String 3","String 4","String 5")
# example_method(25,"String 1","String 2","String 3",key1='a', key2='b')
#example_method(25,"String 1",key1='a', key2='b')
# example_method(key1='a', key2='b',mandatory_parameter=25,default_parameter="String 1")
# example_method(25,"String 1",key1='a', key2='b')
example_list = [1,2,3,4,5,6]
# example_method(*example_list)
example_dict = {'a':'1', 'b':'2'}
example_method(*example_list, **example_dict)
```
---

#### /05-tips/module_1.py

```py
def method_1():
    print("method 1")

class ClassA:
    def class_method_1(self):
        print("class_method_1 method 1")

# print(__name__)

if __name__ == '__main__':
    method_1()
    ClassA().class_method_1()
```
---

#### /05-tips/module_2.py

```py
import module_1

module_1.method_1()
module_1.ClassA().class_method_1()
```
---



### Python Shell Code

```py
Last login: Sat May 19 09:06:12 on ttys001
Rangas-MacBook-Pro:~ rangaraokaranam$ python3
Python 3.6.5 (default, Mar 30 2018, 06:42:10) 
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print(4.5 - 3.2)
1.2999999999999998
>>> value1 = Decimal('4.5')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'Decimal' is not defined
>>> import decimal
>>> from decimal import Decimal
>>> value1 = Decimal('4.5')
>>> value2 = Decimal('3.2')
>>> value1 - value2
Decimal('1.3')
>>> import math
>>> math.
math.acos(       math.erf(        math.inf         math.pi
math.acosh(      math.erfc(       math.isclose(    math.pow(
math.asin(       math.exp(        math.isfinite(   math.radians(
math.asinh(      math.expm1(      math.isinf(      math.sin(
math.atan(       math.fabs(       math.isnan(      math.sinh(
math.atan2(      math.factorial(  math.ldexp(      math.sqrt(
math.atanh(      math.floor(      math.lgamma(     math.tan(
math.ceil(       math.fmod(       math.log(        math.tanh(
math.copysign(   math.frexp(      math.log10(      math.tau
math.cos(        math.fsum(       math.log1p(      math.trunc(
math.cosh(       math.gamma(      math.log2(       
math.degrees(    math.gcd(        math.modf(       
math.e           math.hypot(      math.nan         
>>> math.pi
3.141592653589793
>>> math.e
2.718281828459045
>>> help(math.factorial)

>>> help(math.ceil)

>>> math.ceil(5.5)
6
>>> math.ceil(-5.5)
-5
>>> import os
>>> os.system('clear')

0
>>> import statistics
>>> statistics.
statistics.Decimal(          statistics.mean(
statistics.Fraction(         statistics.median(
statistics.StatisticsError(  statistics.median_grouped(
statistics.bisect_left(      statistics.median_high(
statistics.bisect_right(     statistics.median_low(
statistics.chain(            statistics.mode(
statistics.collections       statistics.numbers
statistics.decimal           statistics.pstdev(
statistics.groupby(          statistics.pvariance(
statistics.harmonic_mean(    statistics.stdev(
statistics.math              statistics.variance(
>>> marks = [1, 6, 9, 23, 2]
>>> statistics.mean(marks)
8.2
>>> statistics.median(marks)
6
>>> marks = [1, 6, 9, 23, 2, 7]
>>> statistics.median(marks)
6.5
>>> statistics.median_high(marks)
7
>>> statistics.median_low(marks)
6
>>> statistics.variance(marks)
63.2
>>> os.system('clear')

0
>>> from collections import deque
>>> queue = deque(['Zero','One','Two'])
>>> queue.pop()
'Two'
>>> queue.append('Three')
>>> queue
deque(['Zero', 'One', 'Three'])
>>> queue.append('Four')
>>> queue.append('Five')
>>> queue.appendLeft('Minus One')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'collections.deque' object has no attribute 'appendLeft'
>>> queue.append
queue.append(      queue.appendleft(  
>>> queue.appendleft('Minus One')
>>> queue
deque(['Minus One', 'Zero', 'One', 'Three', 'Four', 'Five'])
>>> queue.pop()
'Five'
>>> queue.popleft()
'Minus One'
>>> os.system('clear')

0
>>> import datetime
>>> datetime.datetime.today()
datetime.datetime(2018, 5, 21, 9, 59, 57, 450683)
>>> today_date = datetime.datetime.today()
>>> today_date
datetime.datetime(2018, 5, 21, 10, 0, 39, 732463)
>>> today_date.year
2018
>>> today_date.month
5
>>> today_date.day
21
>>> today_date.hour
10
>>> today_date.minute
0
>>> today_date.second
39
>>> some_date = datetime.datetime(2019, 5, 27)
>>> some_date
datetime.datetime(2019, 5, 27, 0, 0)
>>> some_date = datetime.datetime(2019, 5, 27, 9, 5,25)
>>> some_date
datetime.datetime(2019, 5, 27, 9, 5, 25)
>>> some_date = datetime.datetime(2019, 5, 27, 9, 5,25, 234567)
>>> some_date
datetime.datetime(2019, 5, 27, 9, 5, 25, 234567)
>>> some_date.date()
datetime.date(2019, 5, 27)
>>> some_date.time()
datetime.time(9, 5, 25, 234567)
>>> some_date
datetime.datetime(2019, 5, 27, 9, 5, 25, 234567)
>>> day = some_date
>>> day
datetime.datetime(2019, 5, 27, 9, 5, 25, 234567)
>>> day + time.timedelta(day=90)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'time' is not defined
>>> day + datetime.timedelta(day=90)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'day' is an invalid keyword argument for this function
>>> day + datetime.timedelta(days=90)
datetime.datetime(2019, 8, 25, 9, 5, 25, 234567)
>>> day
datetime.datetime(2019, 5, 27, 9, 5, 25, 234567)
>>> day + datetime.timedelta(days=90)
datetime.datetime(2019, 8, 25, 9, 5, 25, 234567)
>>> day + datetime.timedelta(weeks=3)
datetime.datetime(2019, 6, 17, 9, 5, 25, 234567)
>>> day + datetime.timedelta(hours=48)
datetime.datetime(2019, 5, 29, 9, 5, 25, 234567)
>>> os.system('clear')

0
>>> import math
>>> math.
math.acos(       math.erf(        math.inf         math.pi
math.acosh(      math.erfc(       math.isclose(    math.pow(
math.asin(       math.exp(        math.isfinite(   math.radians(
math.asinh(      math.expm1(      math.isinf(      math.sin(
math.atan(       math.fabs(       math.isnan(      math.sinh(
math.atan2(      math.factorial(  math.ldexp(      math.sqrt(
math.atanh(      math.floor(      math.lgamma(     math.tan(
math.ceil(       math.fmod(       math.log(        math.tanh(
math.copysign(   math.frexp(      math.log10(      math.tau
math.cos(        math.fsum(       math.log1p(      math.trunc(
math.cosh(       math.gamma(      math.log2(       
math.degrees(    math.gcd(        math.modf(       
math.e           math.hypot(      math.nan         
>>> math.floor(4.5)
4
>>> help(math.floor)

>>> help(math)

>>> 
>>> from math import *
>>> floor(5)
5
>>> gcd(34,56)
2
>>> from math import gcd
>>> gcd(56,68)
4
>>> os.system('clear')

0
>>> numbers = [1,4,6,3,4]
>>> for number in numbers:
...   print(number)
... 
1
4
6
3
4
>>> for index,number in enumerate(numbers):
...    print(f'{index} - {number}')
... 
0 - 1
1 - 4
2 - 6
3 - 3
4 - 4
>>> values = list('aeiou')
>>> values
['a', 'e', 'i', 'o', 'u']
>>> for index, vowel in enumerate(values):
...     printf(f'{index} - {vowel}')
... 
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
NameError: name 'printf' is not defined
>>> for index, vowel in enumerate(values):
...     print(f'{index} - {vowel}')
... 
0 - a
1 - e
2 - i
3 - o
4 - u
>>> import os
>>> os.system('clear')

0
>>> number = 5
>>> if(number%2==0):
...   isEven = True
... else:
...   isEven = False
... 
>>> isEven = True if number%2==0 else False
>>> isEven
False
>>> number = 6
>>> isEven = True if number%2==0 else False
>>> isEven
True
>>> isEven = number%2==0
>>> isEven = "Yes" if number%2==0 else "No"
>>> isEven
'Yes'
>>> os.system('clear')

0
>>> a = 1
>>> len(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: object of type 'int' has no len()
>>> type(a)
<class 'int'>
>>> str = "Value"
>>> str.upper()
'VALUE'
>>> a.upper()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'int' object has no attribute 'upper'
>>> type(1)
<class 'int'>
>>> type(1.5)
<class 'float'>
>>> type("1.5")
<class 'str'>
>>> type(True)
<class 'bool'>
>>> type(str)
<class 'str'>
>>> str = 1
>>> type(str)
<class 'int'>
>>> str = True
>>> type(str)
<class 'bool'>
>>> str = [1,2]
>>> type(str)
<class 'list'>
>>> os.system('clear')

0
>>> def create_ranga():
...    return 'Ranga',1981,'India'
... 
>>> ranga = create_ranga()
>>> type(ranga)
<class 'tuple'>
>>> name, year, country = ranga
>>> ranga
('Ranga', 1981, 'India')
>>> name
'Ranga'
>>> year
1981
>>> country
'India'
>>> len(ranga)
3
>>> ranga[0]
'Ranga'
>>> ranga[1]
1981
>>> ranga[2]
'India'
>>> ranga[1] = 1991
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> person = ('Ranga', 5, 'India')
>>> person = 'Ranga', 5, 'India'
>>> type(person)
<class 'tuple'>
>>> name, age, country = person
>>> name, age = person
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: too many values to unpack (expected 2)
>>> x = 0
>>> y = 1
>>> x, y = 0, 1
>>> x, y = y, x
>>> x
1
>>> y
0
>>> x = (0)
>>> type(x)
<class 'int'>
>>> x = (0,)
>>> x = 1,
>>> type(x)
<class 'tuple'>
>>> os.system('clear')
0
>>> 
>>> sum
<built-in function sum>
>>> sum([12,34,56])
102
>>> number1 = 10
>>> number2 = 20
>>> sum = number1 + number2
>>> sum
30
>>> sum([12,34,56])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable
>>> sum_ = number1 + number2
>>> del sum
>>> sum
<built-in function sum>
>>> sum([12,34,56])
102
>>> os.system('clear')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'os' is not defined
>>> import os
>>> os.system('clear')

0
>>> None
>>> type(None)
<class 'NoneType'>
>>> def email(subject, content, to , cc , bcc): 
...    print(f" {subject}, {content}, {to}, {cc}, "
... )
... 
>>> email("subject", "great work", in28minutes@gmail.com)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'in28minutes' is not defined
>>> email("subject", "great work", "in28minutes@gmail.com")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: email() missing 2 required positional arguments: 'cc' and 'bcc'
>>> def email(subject, content, to , cc=None , bcc=None): 
...    print(f" {subject}, {content}, {to}, {cc}, {bcc}");
... 
>>> email("subject", "great work", "in28minutes@gmail.com")
 subject, great work, in28minutes@gmail.com, None, None
>>> email("subject", "great work", "in28minutes@gmail.com", None, None)
 subject, great work, in28minutes@gmail.com, None, None
>>> email(None, "great work", "in28minutes@gmail.com", None, None)
 None, great work, in28minutes@gmail.com, None, None
>>> var = "123"
>>> if var is None : print ("do something");
... 
>>> var = None
>>> if var is None : print ("do something");
... 
do something
>>> os.system('clear')

0
>>> class Student: pass
... 
>>> student1 = Student()
>>> student2 = Student()
>>> id(student1)
4554811768
>>> id(student2)
4554811992
>>> student1 is student2
False
>>> student3 = student1
>>> id(student3)
4554811768
>>> student1 is student3
True
>>> student1 == student2
False
>>> student1 == student3
True
>>> class Student:
...    def __init__(self, id): 
...        self.id = id
... 
>>> student1 = Student(1)
>>> student2 = Student(2)
>>> student3 = Student(1)
>>> student4 = student1
>>> id(student1)
4554812160
>>> id(student4)
4554812160
>>> student1 is student4
True
>>> student1 is student2
False
>>> student1 is student3
False
>>> student1 == student3
False
>>> class Student:
...    def __init__(self, id):
...       self.id = id
...    def __eq__(self, other):
...       return self.id == other.id
... 
>>> student1 = Student(1)
>>> student2 = Student(2)
>>> student3 = Student(1)
>>> student4 = student1
>>> student4 == student1
True
>>> student2 == student1
False
>>> student3 == student1
True
>>> os.system('clear')

0
>>>  i=1
  File "<stdin>", line 1
    i=1
    ^
IndentationError: unexpected indent
>>>     i=3
  File "<stdin>", line 1
    i=3
    ^
IndentationError: unexpected indent
>>> i=1
>>> if(i==3):
... print('somethin')
  File "<stdin>", line 2
    print('somethin')
        ^
IndentationError: expected an indented block
>>> if(i==3):
...   print('something')
...  print('') 
  File "<stdin>", line 3
    print('') 
             ^
IndentationError: unindent does not match any outer indentation level
>>> os.system('clear')

0
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
>>> 
```

# Mockito

#### JUnit
- Step 01 : Need for Unit Testing
- Step 02 : Setting up your First JUnit
- Step 03 : First Successful JUnit. Green Bar and assertEquals
- Step 04 : Refactoring Your First JUnit Test
- Step 05 : Second JUnit Example   assertTrue and assertFalse
- Step 06 : @Before @After
- Step 07 : @BeforeClass @AfterClass
- Step 08 : Comparing Arrays in JUnit Tests
- Step 09 : Testing Exceptions in JUnit Tests
- Step 10 : Testing Performance in JUnit Tests
- Step 11 : Parameterized Tests
- Step 12 : Organize JUnits into Suites

#### Mockito
- Step 01 : Set up an Eclipse Project with JUnit and Mockito frameworks. First Green Bar.
- Step 02 : Example to start understanding why we need mocks.
- Step 03 : What is a stub? Create an unit test using Stub? Disadvantages of Stubs.
- Step 04 : Your first Mockito code! Hurrah!!! Lets use Mockito to mock TodoService.
- Step 05 : Stubbing variations with Mockito. A few mockito examples mocking List class : Multiple return values, Argument Matchers and throwing exceptions.
- Some Theory : Mockito vs EasyMock [https://github.com/mockito/mockito/wiki/Mockito-vs-EasyMock](https://github.com/mockito/mockito/wiki/Mockito-vs-EasyMock)
- Step 06 : Introduction to BDD. Given When Then. BDD Mockito Syntax.
- Step 07 : How to verify calls on a mock? Verify how many times a method is called. We will add deleteTodo method to the TodoService.
- Step 08 : How to capture an argument which is passed to a mock?
- Step 09 : Hamcrest Matchers.
- Step 10 : Let's simplify things with Mockito Annotations. @Mock, @InjectMocks, @RunWith(MockitoJUnitRunner.class), @Captor
- Step 11 : JUnit Rules. Using MockitoJUnit.rule() instead of @RunWith(MockitoJUnitRunner.class).
- Step 12 : Real world Example with Spring
- Step 13 : What is a spy? How to spy with Mockito?
- Step 14 : Some Theory : Why does Mockito not allow stubbing final and private methods?
- Step 15 : Using PowerMock and Mockito to mock a Static Method.
- Step 16 : Using PowerMock and Mockito to invoke a private Method.
- Step 17 : Using PowerMock and Mockito to mock a constructor.
- Step 18 : Good Unit Tests.


## What You Will Learn during this Step:
- Using PowerMock and Mockito to mock a constructor
- PowerMockitoMockingConstructorTest.java
-- 	PowerMockito.whenNew(ArrayList.class).withAnyArguments().thenReturn(
				mockList);

## Files List
### /pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.in28minutes.mockito</groupId>
	<artifactId>mockito-tutorial</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.mockito</groupId>
			<artifactId>mockito-all</artifactId>
			<version>1.10.19</version>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.hamcrest</groupId>
			<artifactId>hamcrest-library</artifactId>
			<version>1.3</version>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.powermock</groupId>
			<artifactId>powermock-api-mockito</artifactId>
			<version>1.6.4</version>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.powermock</groupId>
			<artifactId>powermock-module-junit4</artifactId>
			<version>1.6.4</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>
		</plugins>
	</build>
</project>
```
### /src/main/java/com/in28minutes/business/TodoBusinessImpl.java
```
package com.in28minutes.business;

import java.util.ArrayList;
import java.util.List;

import com.in28minutes.data.api.TodoService;

public class TodoBusinessImpl {

	private TodoService todoService;

	TodoBusinessImpl(TodoService todoService) {
		this.todoService = todoService;
	}

	public List<String> retrieveTodosRelatedToSpring(String user) {
		List<String> filteredTodos = new ArrayList<String>();
		List<String> allTodos = todoService.retrieveTodos(user);
		for (String todo : allTodos) {
			if (todo.contains("Spring")) {
				filteredTodos.add(todo);
			}
		}
		return filteredTodos;
	}

	public void deleteTodosNotRelatedToSpring(String user) {
		List<String> allTodos = todoService.retrieveTodos(user);
		for (String todo : allTodos) {
			if (!todo.contains("Spring")) {
				todoService.deleteTodo(todo);
			}
		}
	}
}
```
### /src/main/java/com/in28minutes/data/api/TodoService.java
```
package com.in28minutes.data.api;

import java.util.List;

// External Service - Lets say this comes from WunderList
public interface TodoService {

	public List<String> retrieveTodos(String user);

	void deleteTodo(String todo);

}
```
### /src/main/java/com/in28minutes/junit/business/ClientBO.java
```
package com.in28minutes.junit.business;

import java.util.List;

import com.in28minutes.junit.business.exception.DifferentCurrenciesException;
import com.in28minutes.junit.model.Amount;
import com.in28minutes.junit.model.Product;

public interface ClientBO {

	Amount getClientProductsSum(List<Product> products)
			throws DifferentCurrenciesException;

}
```
### /src/main/java/com/in28minutes/junit/business/ClientBOImpl.java
```
package com.in28minutes.junit.business;

import java.math.BigDecimal;
import java.util.List;

import com.in28minutes.junit.business.exception.DifferentCurrenciesException;
import com.in28minutes.junit.model.Amount;
import com.in28minutes.junit.model.AmountImpl;
import com.in28minutes.junit.model.Currency;
import com.in28minutes.junit.model.Product;

public class ClientBOImpl implements ClientBO {

	public Amount getClientProductsSum(List<Product> products)
			throws DifferentCurrenciesException {

		if (products.size() == 0)
			return new AmountImpl(BigDecimal.ZERO, Currency.EURO);

		if (!isCurrencySameForAllProducts(products)) {
			throw new DifferentCurrenciesException();
		}

		BigDecimal productSum = calculateProductSum(products);

		Currency firstProductCurrency = products.get(0).getAmount()
				.getCurrency();

		return new AmountImpl(productSum, firstProductCurrency);
	}

	private BigDecimal calculateProductSum(List<Product> products) {
		BigDecimal sum = BigDecimal.ZERO;
		// Calculate Sum of Products
		for (Product product : products) {
			sum = sum.add(product.getAmount().getValue());
		}
		return sum;
	}

	private boolean isCurrencySameForAllProducts(List<Product> products)
			throws DifferentCurrenciesException {

		Currency firstProductCurrency = products.get(0).getAmount()
				.getCurrency();

		for (Product product : products) {
			boolean currencySameAsFirstProduct = product.getAmount()
					.getCurrency().equals(firstProductCurrency);
			if (!currencySameAsFirstProduct) {
				return false;
			}
		}

		return true;
	}
}
```
### /src/main/java/com/in28minutes/junit/business/exception/DifferentCurrenciesException.java
```
package com.in28minutes.junit.business.exception;

public class DifferentCurrenciesException extends Exception {

	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;

}
```
### /src/main/java/com/in28minutes/junit/helper/StringHelper.java
```
package com.in28minutes.junit.helper;

public class StringHelper {

	public String truncateAInFirst2Positions(String str) {
		if (str.length() <= 2)
			return str.replaceAll("A", "");

		String first2Chars = str.substring(0, 2);
		String stringMinusFirst2Chars = str.substring(2);

		return first2Chars.replaceAll("A", "") + stringMinusFirst2Chars;
	}
	
	public boolean areFirstAndLastTwoCharactersTheSame(String str) {

		if (str.length() <= 1)
			return false;
		if (str.length() == 2)
			return true;

		String first2Chars = str.substring(0, 2);

		String last2Chars = str.substring(str.length() - 2);

		return first2Chars.equals(last2Chars);
	}

}
```
### /src/main/java/com/in28minutes/junit/model/Amount.java
```
package com.in28minutes.junit.model;

import java.math.BigDecimal;

public interface Amount {
	BigDecimal getValue();

	Currency getCurrency();
}
```
### /src/main/java/com/in28minutes/junit/model/AmountImpl.java
```
package com.in28minutes.junit.model;

import java.math.BigDecimal;

public class AmountImpl implements Amount {

	BigDecimal value;
	Currency currency;

	public AmountImpl(BigDecimal value, Currency currency) {
		super();
		this.value = value;
		this.currency = currency;
	}

	public void setValue(BigDecimal value) {
		this.value = value;
	}

	@Override
	public BigDecimal getValue() {
		return value;
	}

	public void setCurrency(Currency currency) {
		this.currency = currency;
	}

	@Override
	public Currency getCurrency() {
		return currency;
	}

}
```
### /src/main/java/com/in28minutes/junit/model/Client.java
```
package com.in28minutes.junit.model;

import java.math.BigDecimal;
import java.util.List;

/**
 * Client Model API.
 */
public interface Client {

	long getId();

	String getName();

	Enum<?> getType();

	List<Collateral> getCollaterals();

	List<Product> getProducts();

	void setProductAmount(BigDecimal productAmount);

	BigDecimal getProductAmount();

}
```
### /src/main/java/com/in28minutes/junit/model/ClientImpl.java
```
package com.in28minutes.junit.model;

import java.math.BigDecimal;
import java.util.List;

/**
 * Client Model API.
 */
public class ClientImpl implements Client {

	private long id;

	private String name;

	private ClientType type;

	private List<Collateral> collaterals;

	private List<Product> products;

	private BigDecimal productAmount;

	public ClientImpl(long id, String name, ClientType type,
			List<Collateral> collaterals, List<Product> products) {
		super();
		this.id = id;
		this.name = name;
		this.type = type;
		this.collaterals = collaterals;
		this.products = products;
	}

	public long getId() {
		return id;
	}

	public void setId(long id) {
		this.id = id;
	}

	@Override
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public ClientType getType() {
		return type;
	}

	public void setType(ClientType type) {
		this.type = type;
	}

	@Override
	public List<Collateral> getCollaterals() {
		return collaterals;
	}

	public void setCollaterals(List<Collateral> collaterals) {
		this.collaterals = collaterals;
	}

	@Override
	public List<Product> getProducts() {
		return products;
	}

	public void setProducts(List<Product> products) {
		this.products = products;
	}

	@Override
	public BigDecimal getProductAmount() {
		return productAmount;
	}

	@Override
	public void setProductAmount(BigDecimal productAmount) {
		this.productAmount = productAmount;
	}

}
```
### /src/main/java/com/in28minutes/junit/model/ClientType.java
```
package com.in28minutes.junit.model;

import java.util.Arrays;
import java.util.List;

/**
 * Available types of customers
 */
public enum ClientType {
	/**
     * 
     */
	PRIVATE("P"),
	/**
     * 
     */
	BUSINESS("Z");

	private final String textValue;

	/**
	 * List of natural person types.
	 */
	public static final List<String> NATURAL_PERSON_TYPES = Arrays
			.asList(ClientType.PRIVATE.toString());

	/**
	 * List of corporate types.
	 */
	public static final List<String> CORPORATE_TYPES = Arrays
			.asList(ClientType.BUSINESS.toString());

	ClientType(final String textValue) {
		this.textValue = textValue;
	}

	@Override
	public String toString() {
		return textValue;
	}
}
```
### /src/main/java/com/in28minutes/junit/model/Collateral.java
```
package com.in28minutes.junit.model;

/**
 * Collateral Model API.
 */
public interface Collateral {

	long getId();

	String getName();

	CollateralType getType();
}
```
### /src/main/java/com/in28minutes/junit/model/CollateralImpl.java
```
package com.in28minutes.junit.model;

/**
 * Collateral Model Object.
 */
public class CollateralImpl implements Collateral {

	private long id;

	private String name;

	private CollateralType type;

	public CollateralImpl(long id, String name, CollateralType type) {
		super();
		this.id = id;
		this.name = name;
		this.type = type;
	}

	public long getId() {
		return id;
	}

	public void setId(long id) {
		this.id = id;
	}

	@Override
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public CollateralType getType() {
		return type;
	}

	public void setType(CollateralType type) {
		this.type = type;
	}
}
```
### /src/main/java/com/in28minutes/junit/model/CollateralType.java
```
package com.in28minutes.junit.model;

import java.util.Arrays;
import java.util.List;

/**
 * Available types of customers
 */
public enum CollateralType {
	REAL_ESTATE("REA"), BONDS("BND"), MUTUAL_FUNDS("MFD"), STOCKS("STK");

	private final String textValue;

	/**
	 * All collateral types classified as securities.
	 */
	public static final List<CollateralType> SECURITIES = Arrays.asList(BONDS,
			MUTUAL_FUNDS, STOCKS);

	CollateralType(final String textValue) {
		this.textValue = textValue;
	}

	@Override
	public String toString() {
		return textValue;
	}
}
```
### /src/main/java/com/in28minutes/junit/model/Currency.java
```
package com.in28minutes.junit.model;

public enum Currency {

	EURO("EUR"), UNITED_STATES_DOLLAR("USD"), INDIAN_RUPEE("INR");

	private final String textValue;

	Currency(final String textValue) {
		this.textValue = textValue;
	}

	@Override
	public String toString() {
		return textValue;
	}
}
```
### /src/main/java/com/in28minutes/junit/model/Product.java
```
package com.in28minutes.junit.model;

/**
 * Product Model API.
 */
public interface Product {

	long getId();

	String getName();

	ProductType getType();

	Amount getAmount();
}
```
### /src/main/java/com/in28minutes/junit/model/ProductImpl.java
```
package com.in28minutes.junit.model;

/**
 * Collateral Model Object.
 */
public class ProductImpl implements Product {

	private long id;

	private String name;

	private ProductType type;

	private Amount amount;

	public ProductImpl(long id, String name, ProductType type, Amount amount) {
		super();
		this.id = id;
		this.name = name;
		this.type = type;
		this.amount = amount;
	}

	@Override
	public long getId() {
		return id;
	}

	public void setId(long id) {
		this.id = id;
	}

	@Override
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public ProductType getType() {
		return type;
	}

	public void setType(ProductType type) {
		this.type = type;
	}

	@Override
	public Amount getAmount() {
		return amount;
	}

	public void setAmount(Amount amount) {
		this.amount = amount;
	}
}
```
### /src/main/java/com/in28minutes/junit/model/ProductType.java
```
package com.in28minutes.junit.model;

/**
 * Available types of customers
 */
public enum ProductType {
	LOAN("LN"), KREDIT("KRD"), BANK_GUARANTEE("BG");

	private final String textValue;

	ProductType(final String textValue) {
		this.textValue = textValue;
	}

	@Override
	public String toString() {
		return textValue;
	}
}
```
### /src/main/java/com/in28minutes/powermock/SystemUnderTest.java
```
package com.in28minutes.powermock;

import java.util.ArrayList;
import java.util.List;

interface Dependency {
	List<Integer> retrieveAllStats();
}

public class SystemUnderTest {
	private Dependency dependency;

	public int methodUsingAnArrayListConstructor() {
		ArrayList list = new ArrayList();
		return list.size();
	}

	public int methodCallingAStaticMethod() {
		//privateMethodUnderTest calls static method SomeClass.staticMethod
		List<Integer> stats = dependency.retrieveAllStats();
		long sum = 0;
		for (int stat : stats)
			sum += stat;
		return UtilityClass.staticMethod(sum);
	}

	private long privateMethodUnderTest() {
		List<Integer> stats = dependency.retrieveAllStats();
		long sum = 0;
		for (int stat : stats)
			sum += stat;
		return sum;
	}
}
```
### /src/main/java/com/in28minutes/powermock/UtilityClass.java
```
package com.in28minutes.powermock;

public class UtilityClass {
	static int staticMethod(long value) {
		// Some complex logic is done here...
		throw new RuntimeException(
				"I dont want to be executed. I will anyway be mocked out.");
	}
}
```
### /src/test/java/com/clarity/business/ClientBOTest.java
```
package com.clarity.business;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.fail;

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

import org.junit.Test;

import com.in28minutes.junit.business.ClientBO;
import com.in28minutes.junit.business.ClientBOImpl;
import com.in28minutes.junit.business.exception.DifferentCurrenciesException;
import com.in28minutes.junit.model.Amount;
import com.in28minutes.junit.model.AmountImpl;
import com.in28minutes.junit.model.Currency;
import com.in28minutes.junit.model.Product;
import com.in28minutes.junit.model.ProductImpl;
import com.in28minutes.junit.model.ProductType;

public class ClientBOTest {

	private ClientBO clientBO = new ClientBOImpl();

	@Test
	public void testClientProductSum() throws DifferentCurrenciesException {

		List<Product> products = new ArrayList<Product>();

		products.add(new ProductImpl(100, "Product 15",
				ProductType.BANK_GUARANTEE, new AmountImpl(
						new BigDecimal("5.0"), Currency.EURO)));

		products.add(new ProductImpl(120, "Product 20",
				ProductType.BANK_GUARANTEE, new AmountImpl(
						new BigDecimal("6.0"), Currency.EURO)));

		Amount temp = clientBO.getClientProductsSum(products);

		assertEquals(Currency.EURO, temp.getCurrency());
		assertEquals(new BigDecimal("11.0"), temp.getValue());
	}

	@Test(expected = DifferentCurrenciesException.class)
	public void testClientProductSum1() throws DifferentCurrenciesException {

		List<Product> products = new ArrayList<Product>();

		products.add(new ProductImpl(100, "Product 15",
				ProductType.BANK_GUARANTEE, new AmountImpl(
						new BigDecimal("5.0"), Currency.INDIAN_RUPEE)));

		products.add(new ProductImpl(120, "Product 20",
				ProductType.BANK_GUARANTEE, new AmountImpl(
						new BigDecimal("6.0"), Currency.EURO)));

		@SuppressWarnings("unused")
		Amount temp = null;

		temp = clientBO.getClientProductsSum(products);
	}

	@Test
	public void testClientProductSum2() {

		List<Product> products = new ArrayList<Product>();

		Amount temp = null;

		try {
			temp = clientBO.getClientProductsSum(products);
		} catch (DifferentCurrenciesException e) {
		}
		assertEquals(Currency.EURO, temp.getCurrency());
		assertEquals(BigDecimal.ZERO, temp.getValue());
	}

}
```
### /src/test/java/com/clarity/business/ClientBOTestRefactored.java
```
package com.clarity.business;

import static org.junit.Assert.assertEquals;

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

import org.junit.Test;

import com.in28minutes.junit.business.ClientBO;
import com.in28minutes.junit.business.ClientBOImpl;
import com.in28minutes.junit.business.exception.DifferentCurrenciesException;
import com.in28minutes.junit.model.Amount;
import com.in28minutes.junit.model.AmountImpl;
import com.in28minutes.junit.model.Currency;
import com.in28minutes.junit.model.Product;
import com.in28minutes.junit.model.ProductImpl;
import com.in28minutes.junit.model.ProductType;

public class ClientBOTestRefactored {

	private ClientBO clientBO = new ClientBOImpl();

	@Test
	public void testClientProductSum_AllProductsSameCurrency()
			throws DifferentCurrenciesException {

		Amount[] amounts = {
				new AmountImpl(new BigDecimal("5.0"), Currency.EURO),
				new AmountImpl(new BigDecimal("6.0"), Currency.EURO) };

		Amount expected = new AmountImpl(new BigDecimal("11.0"), Currency.EURO);
		
		List<Product> products = createProductListWithAmounts(amounts);

		Amount actual = clientBO.getClientProductsSum(products);

		assertAmount(actual, expected);
	}

	@Test(expected = DifferentCurrenciesException.class)
	public void testClientProductSum_DifferentCurrencies_ThrowsException()
			throws DifferentCurrenciesException {

		Amount[] amounts = {
				new AmountImpl(new BigDecimal("5.0"), Currency.EURO),
				new AmountImpl(new BigDecimal("6.0"), Currency.INDIAN_RUPEE) };

		List<Product> products = createProductListWithAmounts(amounts);

		@SuppressWarnings("unused")
		Amount actual = clientBO.getClientProductsSum(products);

	}

	@Test
	public void testClientProductSum_NoProducts()
			throws DifferentCurrenciesException {

		Amount[] amounts = {};
		Amount expected = new AmountImpl(BigDecimal.ZERO, Currency.EURO);

		List<Product> products = createProductListWithAmounts(amounts);

		Amount actual = clientBO.getClientProductsSum(products);


		assertAmount(actual, expected);
	}

	private void assertAmount(Amount actual, Amount expected) {
		assertEquals(expected.getCurrency(), actual.getCurrency());
		assertEquals(expected.getValue(), actual.getValue());
	}

	private List<Product> createProductListWithAmounts(Amount[] amounts) {
		List<Product> products = new ArrayList<Product>();
		for (Amount amount : amounts) {
			products.add(new ProductImpl(100, "Product 15",
					ProductType.BANK_GUARANTEE, amount));
		}
		return products;
	}

}
```
### /src/test/java/com/in28minutes/business/TodoBusinessImplMockitoInjectMocksTest.java
```
package com.in28minutes.business;

import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertThat;
import static org.mockito.BDDMockito.given;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import java.util.Arrays;
import java.util.List;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.ArgumentCaptor;
import org.mockito.Captor;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.runners.MockitoJUnitRunner;

import com.in28minutes.data.api.TodoService;

@RunWith(MockitoJUnitRunner.class)
public class TodoBusinessImplMockitoInjectMocksTest {
	@Mock
	TodoService todoService;

	@InjectMocks
	TodoBusinessImpl todoBusinessImpl;

	@Captor
	ArgumentCaptor<String> stringArgumentCaptor;

	@Test
	public void usingMockito() {
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");
		assertEquals(2, todos.size());
	}

	@Test
	public void usingMockito_UsingBDD() {
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		//given
		given(todoService.retrieveTodos("Ranga")).willReturn(allTodos);

		//when
		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");

		//then
		assertThat(todos.size(), is(2));
	}

	@Test
	public void letsTestDeleteNow() {

		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		todoBusinessImpl.deleteTodosNotRelatedToSpring("Ranga");

		verify(todoService).deleteTodo("Learn to Dance");

		verify(todoService, Mockito.never()).deleteTodo("Learn Spring MVC");

		verify(todoService, Mockito.never()).deleteTodo("Learn Spring");

		verify(todoService, Mockito.times(1)).deleteTodo("Learn to Dance");
		// atLeastOnce, atLeast

	}

	@Test
	public void captureArgument() {
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");
		Mockito.when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		todoBusinessImpl.deleteTodosNotRelatedToSpring("Ranga");
		Mockito.verify(todoService).deleteTodo(stringArgumentCaptor.capture());

		assertEquals("Learn to Dance", stringArgumentCaptor.getValue());
	}
}
```
### /src/test/java/com/in28minutes/business/TodoBusinessImplMockitoRulesTest.java
```
package com.in28minutes.business;

import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertThat;
import static org.mockito.BDDMockito.given;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import java.util.Arrays;
import java.util.List;

import org.junit.Rule;
import org.junit.Test;
import org.mockito.ArgumentCaptor;
import org.mockito.Captor;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.MockitoJUnit;
import org.mockito.junit.MockitoRule;

import com.in28minutes.data.api.TodoService;

public class TodoBusinessImplMockitoRulesTest {

	@Rule
	public MockitoRule mockitoRule = MockitoJUnit.rule();

	@Mock
	TodoService todoService;

	@InjectMocks
	TodoBusinessImpl todoBusinessImpl;

	@Captor
	ArgumentCaptor<String> stringArgumentCaptor;

	@Test
	public void usingMockito() {
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");
		assertEquals(2, todos.size());
	}

	@Test
	public void usingMockito_UsingBDD() {
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		//given
		given(todoService.retrieveTodos("Ranga")).willReturn(allTodos);

		//when
		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");

		//then
		assertThat(todos.size(), is(2));
	}

	@Test
	public void letsTestDeleteNow() {

		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		todoBusinessImpl.deleteTodosNotRelatedToSpring("Ranga");

		verify(todoService).deleteTodo("Learn to Dance");

		verify(todoService, Mockito.never()).deleteTodo("Learn Spring MVC");

		verify(todoService, Mockito.never()).deleteTodo("Learn Spring");

		verify(todoService, Mockito.times(1)).deleteTodo("Learn to Dance");
		// atLeastOnce, atLeast

	}

	@Test
	public void captureArgument() {
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");
		Mockito.when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		todoBusinessImpl.deleteTodosNotRelatedToSpring("Ranga");
		Mockito.verify(todoService).deleteTodo(stringArgumentCaptor.capture());

		assertEquals("Learn to Dance", stringArgumentCaptor.getValue());
	}
}
```
### /src/test/java/com/in28minutes/business/TodoBusinessImplMockitoTest.java
```
package com.in28minutes.business;

import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertThat;
import static org.mockito.BDDMockito.given;
import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import java.util.Arrays;
import java.util.List;

import org.junit.Test;
import org.mockito.ArgumentCaptor;
import org.mockito.Mockito;

import com.in28minutes.data.api.TodoService;

public class TodoBusinessImplMockitoTest {

	@Test
	public void usingMockito() {
		TodoService todoService = mock(TodoService.class);
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");
		when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);
		TodoBusinessImpl todoBusinessImpl = new TodoBusinessImpl(todoService);
		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");
		assertEquals(2, todos.size());
	}

	@Test
	public void usingMockito_UsingBDD() {
		TodoService todoService = mock(TodoService.class);
		TodoBusinessImpl todoBusinessImpl = new TodoBusinessImpl(todoService);
		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		//given
		given(todoService.retrieveTodos("Ranga")).willReturn(allTodos);

		//when
		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");

		//then
		assertThat(todos.size(), is(2));
	}

	@Test
	public void letsTestDeleteNow() {

		TodoService todoService = mock(TodoService.class);

		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");

		when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		TodoBusinessImpl todoBusinessImpl = new TodoBusinessImpl(todoService);

		todoBusinessImpl.deleteTodosNotRelatedToSpring("Ranga");

		verify(todoService).deleteTodo("Learn to Dance");

		verify(todoService, Mockito.never()).deleteTodo("Learn Spring MVC");

		verify(todoService, Mockito.never()).deleteTodo("Learn Spring");

		verify(todoService, Mockito.times(1)).deleteTodo("Learn to Dance");
		// atLeastOnce, atLeast

	}

	@Test
	public void captureArgument() {
		ArgumentCaptor<String> argumentCaptor = ArgumentCaptor
				.forClass(String.class);

		TodoService todoService = mock(TodoService.class);

		List<String> allTodos = Arrays.asList("Learn Spring MVC",
				"Learn Spring", "Learn to Dance");
		Mockito.when(todoService.retrieveTodos("Ranga")).thenReturn(allTodos);

		TodoBusinessImpl todoBusinessImpl = new TodoBusinessImpl(todoService);
		todoBusinessImpl.deleteTodosNotRelatedToSpring("Ranga");
		Mockito.verify(todoService).deleteTodo(argumentCaptor.capture());

		assertEquals("Learn to Dance", argumentCaptor.getValue());
	}
}
```
### /src/test/java/com/in28minutes/business/TodoBusinessImplStubTest.java
```
package com.in28minutes.business;

import static org.junit.Assert.assertEquals;

import java.util.List;

import org.junit.Test;

import com.in28minutes.data.api.TodoService;
import com.in28minutes.data.stub.TodoServiceStub;

public class TodoBusinessImplStubTest {

	@Test
	public void usingAStub() {
		TodoService todoService = new TodoServiceStub();
		TodoBusinessImpl todoBusinessImpl = new TodoBusinessImpl(todoService);
		List<String> todos = todoBusinessImpl
				.retrieveTodosRelatedToSpring("Ranga");
		assertEquals(2, todos.size());
	}
}
```
### /src/test/java/com/in28minutes/data/stub/TodoServiceStub.java
```
package com.in28minutes.data.stub;

import java.util.Arrays;
import java.util.List;

import com.in28minutes.data.api.TodoService;

public class TodoServiceStub implements TodoService {
	public List<String> retrieveTodos(String user) {
		return Arrays.asList("Learn Spring MVC", "Learn Spring",
				"Learn to Dance");
	}

	public void deleteTodo(String todo) {

	}
}
```
### /src/test/java/com/in28minutes/junit/helper/ArraysCompareTest.java
```
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import java.util.Arrays;

import org.junit.Test;

public class ArraysCompareTest {

	@Test
	public void testArraySort_RandomArray() {
		int[] numbers = { 12, 3, 4, 1 };
		int[] expected = { 1, 3, 4, 12 };
		Arrays.sort(numbers);
		assertArrayEquals(expected, numbers);
	}

	@Test(expected=NullPointerException.class)
	public void testArraySort_NullArray() {
		int[] numbers = null;
		Arrays.sort(numbers);
	}
	
	@Test(timeout=100)
	public void testSort_Performance(){
		int array[] = {12,23,4};
		for(int i=1;i<=1000000;i++)
		{
			array[0] = i;
			Arrays.sort(array);
		}
	}

}
```
### /src/test/java/com/in28minutes/junit/helper/ArraysTest.java
```
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;


import java.util.Arrays;

import org.junit.Test;

public class ArraysTest {
	@Test(timeout=100)
	public void testPerformance() {
		for(int  i=0;i<1000000;i++){
			Arrays.sort(new int[]{i,i-1,i+1});
		}
	}
}
```
### /src/test/java/com/in28minutes/junit/helper/QuickBeforeAfterTest.java
```
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

public class QuickBeforeAfterTest {
	
	@BeforeClass
	public static void beforeClass(){
		System.out.println("Before Class");
	}
	
	@Before
	public void setup(){
		System.out.println("Before Test");
	}

	@Test
	public void test1() {
		System.out.println("test1 executed");
	}

	@Test
	public void test2() {
		System.out.println("test2 executed");
	}
	
	@After
	public void teardown() {
		System.out.println("After test");
	}
	
	@AfterClass
	public static void afterClass(){
		System.out.println("After Class");
	}

}
```
### /src/test/java/com/in28minutes/junit/helper/StringHelperParameterizedTest.java
```
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

@RunWith(Parameterized.class)
public class StringHelperParameterizedTest {

	// AACD => CD ACD => CD CDEF=>CDEF CDAA => CDAA

	StringHelper helper = new StringHelper();
	
	private String input;
	private String expectedOutput;
	
	public StringHelperParameterizedTest(String input, String expectedOutput) {
		this.input = input;
		this.expectedOutput = expectedOutput;
	}

	@Parameters
	public static Collection<String[]> testConditions() {
		String expectedOutputs[][] = { 
				{ "AACD", "CD" }, 
				{ "ACD", "CD" } };
		return Arrays.asList(expectedOutputs);
	}

	@Test
	public void testTruncateAInFirst2Positions() {
		assertEquals(expectedOutput, 
				helper.truncateAInFirst2Positions(input));
	}
}
```
### /src/test/java/com/in28minutes/junit/helper/StringHelperTest.java
```
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import org.junit.Before;
import org.junit.Test;

public class StringHelperTest {

	// AACD => CD ACD => CD CDEF=>CDEF CDAA => CDAA

	StringHelper helper;
	
	@Before
	public void before(){
		helper = new StringHelper();
	}
	

	@Test
	public void testTruncateAInFirst2Positions_AinFirst2Positions() {
		assertEquals("CD", helper.truncateAInFirst2Positions("AACD"));
	}

	@Test
	public void testTruncateAInFirst2Positions_AinFirstPosition() {
		assertEquals("CD", helper.truncateAInFirst2Positions("ACD"));
	}

	// ABCD => false, ABAB => true, AB => true, A => false
	@Test
	public void testAreFirstAndLastTwoCharactersTheSame_BasicNegativeScenario() {
		assertFalse( 
				helper.areFirstAndLastTwoCharactersTheSame("ABCD"));
	}

	@Test
	public void testAreFirstAndLastTwoCharactersTheSame_BasicPositiveScenario() {
		assertTrue( 
				helper.areFirstAndLastTwoCharactersTheSame("ABAB"));
	}

	
}
```
### /src/test/java/com/in28minutes/junit/suite/DummyTestSuite.java
```
package com.in28minutes.junit.suite;

import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

import com.in28minutes.junit.helper.ArraysTest;
import com.in28minutes.junit.helper.StringHelperTest;

@RunWith(Suite.class)
@SuiteClasses({ArraysTest.class,StringHelperTest.class})
public class DummyTestSuite {

}
```
### /src/test/java/com/in28minutes/mockito/FirstMockitoTest.java
```
package com.in28minutes.mockito;

import static org.junit.Assert.assertTrue;

import org.junit.Test;

public class FirstMockitoTest {

	@Test
	public void test() {
		assertTrue(true);
	}

}
```
### /src/test/java/com/in28minutes/mockito/HamcrestMatcherTest.java
```
package com.in28minutes.mockito;

import static org.hamcrest.CoreMatchers.hasItems;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.arrayContainingInAnyOrder;
import static org.hamcrest.Matchers.arrayWithSize;
import static org.hamcrest.Matchers.greaterThan;
import static org.hamcrest.Matchers.hasSize;
import static org.hamcrest.Matchers.isEmptyOrNullString;
import static org.hamcrest.Matchers.isEmptyString;
import static org.hamcrest.Matchers.lessThan;
import static org.hamcrest.core.Every.everyItem;

import java.util.Arrays;
import java.util.List;

import org.junit.Test;

public class HamcrestMatcherTest {

	@Test
	public void basicHamcrestMatchers() {
		List<Integer> scores = Arrays.asList(99, 100, 101, 105);
		assertThat(scores, hasSize(4));
		assertThat(scores, hasItems(100, 101));
		assertThat(scores, everyItem(greaterThan(90)));
		assertThat(scores, everyItem(lessThan(200)));

		// String
		assertThat("", isEmptyString());
		assertThat(null, isEmptyOrNullString());

		// Array
		Integer[] marks = { 1, 2, 3 };

		assertThat(marks, arrayWithSize(3));
		assertThat(marks, arrayContainingInAnyOrder(2, 3, 1));

	}
}
```
### /src/test/java/com/in28minutes/mockito/ListTest.java
```
package com.in28minutes.mockito;

import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertNull;
import static org.junit.Assert.assertThat;
import static org.mockito.BDDMockito.given;
import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.when;

import java.util.List;

import org.junit.Test;
import org.mockito.Mockito;

public class ListTest {

	@Test
	public void letsMockListSize() {
		List list = mock(List.class);
		when(list.size()).thenReturn(10);
		assertEquals(10, list.size());
	}

	@Test
	public void letsMockListSizeWithMultipleReturnValues() {
		List list = mock(List.class);
		when(list.size()).thenReturn(10).thenReturn(20);
		assertEquals(10, list.size()); // First Call
		assertEquals(20, list.size()); // Second Call
	}

	@Test
	public void letsMockListGet() {
		List<String> list = mock(List.class);
		when(list.get(0)).thenReturn("in28Minutes");
		assertEquals("in28Minutes", list.get(0));
		assertNull(list.get(1));
	}

	@Test(expected = RuntimeException.class)
	public void letsMockListGetToThrowException() {
		List<String> list = mock(List.class);
		when(list.get(Mockito.anyInt())).thenThrow(
				new RuntimeException("Something went wrong"));
		list.get(0);
	}

	@Test
	public void letsMockListGetWithAny() {
		List<String> list = mock(List.class);
		Mockito.when(list.get(Mockito.anyInt())).thenReturn("in28Minutes");
		// If you are using argument matchers, all arguments
		// have to be provided by matchers.
		assertEquals("in28Minutes", list.get(0));
		assertEquals("in28Minutes", list.get(1));
	}

	@Test
	public void bddAliases_UsingGivenWillReturn() {
		List<String> list = mock(List.class);

		//given
		given(list.get(Mockito.anyInt())).willReturn("in28Minutes");

		//then
		assertThat("in28Minutes", is(list.get(0)));
		assertThat("in28Minutes", is(list.get(0)));
	}
}
```
### /src/test/java/com/in28minutes/mockito/SpyTest.java
```
package com.in28minutes.mockito;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.spy;
import static org.mockito.Mockito.stub;
import static org.mockito.Mockito.verify;

import java.util.ArrayList;
import java.util.List;

import org.junit.Test;

public class SpyTest {

	@Test
	public void creatingASpyOnArrayList() {
		List<String> listSpy = spy(ArrayList.class);
		listSpy.add("Ranga");
		listSpy.add("in28Minutes");

		verify(listSpy).add("Ranga");
		verify(listSpy).add("in28Minutes");

		assertEquals(2, listSpy.size());
		assertEquals("Ranga", listSpy.get(0));
	}

	@Test
	public void creatingASpyOnArrayList_overridingSpecificMethods() {
		List<String> listSpy = spy(ArrayList.class);
		listSpy.add("Ranga");
		listSpy.add("in28Minutes");

		stub(listSpy.size()).toReturn(-1);

		assertEquals(-1, listSpy.size());
		assertEquals("Ranga", listSpy.get(0));

		// @Spy Annotation
	}

}
```
### /src/test/java/com/in28minutes/powermock/PowerMockitoMockingConstructorTest.java
```
package com.in28minutes.powermock;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.stub;

import java.util.ArrayList;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.powermock.api.mockito.PowerMockito;
import org.powermock.core.classloader.annotations.PrepareForTest;
import org.powermock.modules.junit4.PowerMockRunner;

@RunWith(PowerMockRunner.class)
@PrepareForTest({ SystemUnderTest.class /*To be able to mock the Constructor, we need to add in the Class that creates the new object*/})
public class PowerMockitoMockingConstructorTest {

	private static final int SOME_DUMMY_SIZE = 100;

	@Mock
	Dependency dependencyMock;

	@InjectMocks
	SystemUnderTest systemUnderTest;

	@Test
	public void powerMockito_MockingAConstructor() throws Exception {

		ArrayList<String> mockList = mock(ArrayList.class);

		stub(mockList.size()).toReturn(SOME_DUMMY_SIZE);

		PowerMockito.whenNew(ArrayList.class).withAnyArguments().thenReturn(
				mockList);

		int size = systemUnderTest.methodUsingAnArrayListConstructor();

		assertEquals(SOME_DUMMY_SIZE, size);
	}
}
```
### /src/test/java/com/in28minutes/powermock/PowerMockitoMockingStaticMethodTest.java
```
package com.in28minutes.powermock;

import static org.junit.Assert.assertEquals;
import static org.mockito.Matchers.anyLong;
import static org.mockito.Mockito.when;

import java.util.Arrays;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.powermock.api.mockito.PowerMockito;
import org.powermock.core.classloader.annotations.PrepareForTest;
import org.powermock.modules.junit4.PowerMockRunner;

@RunWith(PowerMockRunner.class)
@PrepareForTest({ UtilityClass.class /*The class with static method to be mocked*/})
public class PowerMockitoMockingStaticMethodTest {

	@Mock
	Dependency dependencyMock;

	@InjectMocks
	SystemUnderTest systemUnderTest;

	@Test
	public void powerMockito_MockingAStaticMethodCall() {

		when(dependencyMock.retrieveAllStats()).thenReturn(
				Arrays.asList(1, 2, 3));

		PowerMockito.mockStatic(UtilityClass.class);

		when(UtilityClass.staticMethod(anyLong())).thenReturn(150);

		assertEquals(150, systemUnderTest.methodCallingAStaticMethod());

		//To verify a specific method call
		//First : Call PowerMockito.verifyStatic() 
		//Second : Call the method to be verified
		PowerMockito.verifyStatic();
		UtilityClass.staticMethod(1 + 2 + 3);

		// verify exact number of calls
		//PowerMockito.verifyStatic(Mockito.times(1));

	}
}
```
### /src/test/java/com/in28minutes/powermock/PowerMockitoTestingPrivateMethodTest.java
```
package com.in28minutes.powermock;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.when;

import java.util.Arrays;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.powermock.modules.junit4.PowerMockRunner;
import org.powermock.reflect.Whitebox;

@RunWith(PowerMockRunner.class)
public class PowerMockitoTestingPrivateMethodTest {

	@Mock
	Dependency dependencyMock;

	@InjectMocks
	SystemUnderTest systemUnderTest;

	@Test
	public void powerMockito_CallingAPrivateMethod() throws Exception {
		when(dependencyMock.retrieveAllStats()).thenReturn(
				Arrays.asList(1, 2, 3));
		long value = (Long) Whitebox.invokeMethod(systemUnderTest,
				"privateMethodUnderTest");
		assertEquals(6, value);
	}
}
```


# Unit Testing with Spring, JUnit and Mockito

## Learn Unit Testing with most popular frameworks - Spring Boot, JUnit and Mockito

Spring Boot is the most popular framework to develop RESTful Services. It has awesome unit testing capabilities through Spring Boot Starter Test. Mockito is the most popular mocking framework. JUnit is most popular Java Unit Testing Framework.

In this course, you will learn to build unit tests for simple RESTful Services with Spring Boot Starter Test, Mockito and JUnit. You will learn to write independent unit tests for RESTful web services talking with multiple layers - web, business and data. You will learn how to write integration tests using an in memory database H2.

You will build the unit tests step by step - in more than 50 steps. This course would be a perfect first step as an introduction to unit testing with Spring Boot and Mockito Frameworks.

You will be using Spring (Dependency Management), Spring Boot, Maven (dependencies management), Eclipse (IDE), in memory database H2 and Tomcat Embedded Web Server. We will help you set up each one of these.

You will use all the frameworks that are part of Spring Boot Starter Test - JUnit, Spring Test, Spring Boot Test, AssertJ, Hamcrest, Mockito, JSONassert and JsonPath.

You will learn to use the most important Unit Testing Annotations - @RunWith(SpringRunner.class), @SpringBootTest, @WebMvcTest, @DataJpaTest and @MockBean.

### Recommended Tools
- Java 8 or Later
- Eclipse Oxygen or Later
- Spring Boot 2.0.0.RELEASE or Later

### Installing Java 8 and Eclipse
- Installation Video : https://www.youtube.com/playlist?list=PLBBog2r6uMCSmMVTW_QmDLyASBvovyAO3
- GIT Repository For Installation : https://github.com/in28minutes/getting-started-in-5-steps
- PDF : https://github.com/in28minutes/SpringIn28Minutes/blob/master/InstallationGuide-JavaEclipseAndMaven_v2.pdf

### References
- Intellij
  - https://www.jetbrains.com/help/idea/configuring-testing-libraries.html
  - https://blog.jetbrains.com/idea/2016/08/using-junit-5-in-intellij-idea/
- Spring & Spring Boot Framework - https://www.youtube.com/watch?v=PSP1-2cN7vM&t=893s
- Introduction to JPA and Hibernate using Spring Boot Data Jpa - http://www.springboottutorial.com/introduction-to-jpa-with-spring-boot-data-jpa
- Functional Programming - https://youtu.be/aFCNPHfvqEU
- JUnit - https://junit.org/junit5/docs/current/user-guide/
- AssertJ - https://joel-costigliola.github.io/assertj/
- Mockito - https://github.com/mockito/mockito/wiki/FAQ
- JsonPath - https://github.com/json-path/JsonPath
- Setting up JUnit 5 with Mockito and Spring Boot 2.0 - https://medium.com/@dSebastien/using-junit-5-with-spring-boot-2-kotlin-and-mockito-d5aea5b0c668
- Good Unit Testing 
  - https://github.com/mockito/mockito/wiki/How-to-write-good-tests
  - FIRST. https://pragprog.com/magazines/2012-01/unit-tests-are-first
  - Patterns - http://xunitpatterns.com
- Mocking Static, Private Methods and Constructors 
  - https://github.com/in28minutes/MockitoTutorialForBeginners/blob/master/Step15.md
  - https://github.com/in28minutes/MockitoTutorialForBeginners/tree/master/src/test/java/com/in28minutes/powermock

### Mockito

Easier Static Imports
```
Window > Preferences > Java > Editor > Content Assist > Favorites
org.junit.Assert
org.mockito.BDDMockito
org.mockito.Mockito
org.assertj.core.api.Assertions
org.hamcrest.Matchers
org.hamcrest.CoreMatchers
org.hamcrest.MatcherAssert
```
### What You will learn
- You will learn to write great Unit and Integration tests using Spring Boot Starter Test
- You will learn to write unit tests using Mocks and Spys created with Mockito
- You will learn to write independent unit tests for RESTful web services talking with multiple layers - web, business and data
- You will learn to write integration tests using an in memory database - H2
- You will learn to use all the frameworks that are part of Spring Boot Starter Test - JUnit, Spring Test, Spring Boot Test, AssertJ, Hamcrest, Mockito, JSONassert and JsonPath.
- You will learn to use the most important Unit Testing Annotations - @RunWith(SpringRunner.class), @SpringBootTest, @WebMvcTest, @DataJpaTest and @MockBean.

### Requirements
- You should have working knowledge of Java and Annotations. 
- We will help you install Eclipse and get up and running with Maven and Tomcat.
- You should have basic knowledge about Spring, Spring Boot and JPA/Hibernate. We provide resources that can be used as starting points to enrich your knowledge in the course.
                                                                                
## Mockito

### Step By Step Details

- Step 01: Setting up the project using Spring Initializr
- Step 02: Writing Unit Test for a Simple Business Service
- Step 03: Setting up a Business Service to call a Data Service
- Step 04: Writing your first unit test with Stub
  - Exercise - Update Tests 2 & 3
- Step 05: Exercise Solution - Updating Tests 2 & 3 to use Stubs - Problem with Stubs.
- Step 06: Writing Unit Tests with Mocking using Mockito
  - Exercise - Updating Tests 2 & 3 to use Mockito
- Step 07: Exercise Solution - Updating Tests 2 & 3 to use Mockito
- Step 08: More Refactoring - @Mock, @InjectMocks and @RunWith(MockitoJUnitRunner.class)
- Step 09: Mockito Tips - Multiple Return Values and Specific Argument Matchers
- Step 10: Mockito Tips - Argument Matchers
- Step 11: Mockito Tips - Verify method calls
- Step 12: Mockito Tips - Argument Capture
- Step 13: Mockito Tips - Argument Capture on Multiple Calls
- Step 14: Introduction to Spy
- Step 15: Mockito FAQ

## Spring Boot & Mockito - Unit Testing

### Step By Step Details

- Step 01: Creating a Hello World Controller
- Step 02: Using Mock Mvc to test Hello World Controller
- Step 03: Using Response Matchers to check status and content
- Step 04: Creating a Basic REST Service in Item Controller
- Step 05: Unit Testing Item Controller and Basic JSON Assertions
- Step 06: Digging deeper into JSON Assert
- Step 07: Writing a REST Service talking to Business Layer
- Step 08: Writing Unit Test for REST Service mocking Business Layer
- Step 09 - 01 - Prepare Data Layers with JPA, Hibernate and H2
- Step 10: Create Item Entity and Populate data with data.sql
- Step 11: Create a RESTful Service talking to the database
- Step 12: Writing Unit Test for Web Layer - Controller - Using Mock MVC
- Step 13: Exercise & Solution - Writing Unit Test for Business Layer - Mocking
- Step 14: Writing Unit Test for Data Layer - Data JPA Test
  - Exercise - Write Unit Test for findById method retrieving item with id 10001
- Step 15: Writing an Integration Test using @SpringBootTest
  - Exercise - Make Asserts Better
- Step 16: Tip : Using @MockBean to mock out dependencies you do not want to talk to!
- Step 17: Tip : Creating Different Test Configuration
- Step 18: Writing Unit Tests for Other Request Methods
- Step 19: Refactor SomeBusinessImpl to use Functional Programming
  - Exercise - Convert the second method to use Functional Approach
- Step 20: Better Assertions with Hamcrest - HamcrestMatcherTest
- Step 21: Better Assertions with AssertJ - AssertJTest
- Step 22: Better Assertions with JSONPath - JSONPathTest
- Step 23: Easier Static Imports
- Step 24: Tip : Measuring Test Coverage with Eclipse
- Step 25: Tip : Keep an eye on performance of unit tests!
- Step 26: Good Unit Tests


<!---
Current Directory : /in28Minutes/git/spring-unit-testing-with-junit-and-mockito
-->

## Complete Code Example


### /src/main/java/com/in28minutes/unittesting/unittesting/business/ItemBusinessService.java

```java
package com.in28minutes.unittesting.unittesting.business;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import com.in28minutes.unittesting.unittesting.data.ItemRepository;
import com.in28minutes.unittesting.unittesting.model.Item;

@Component
public class ItemBusinessService {
	
	@Autowired
	private ItemRepository repository;
	
	public Item retreiveHardcodedItem() {
		return new Item(1, "Ball", 10, 100);
	}
	
	public List<Item> retrieveAllItems() {
		List<Item> items = repository.findAll();
		
		for(Item item:items) {
			item.setValue(item.getPrice() * item.getQuantity());
		}
		
		return items;	
	}
	
}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/business/SomeBusinessImpl.java

```java
package com.in28minutes.unittesting.unittesting.business;

import com.in28minutes.unittesting.unittesting.data.SomeDataService;

public class SomeBusinessImpl {
	
	private SomeDataService someDataService;
	
	public void setSomeDataService(SomeDataService someDataService) {
		this.someDataService = someDataService;
	}

	public int calculateSum(int[] data) {
		int sum = 0;
		for(int value:data) {
			sum += value;
		}
		return sum;
		//Functional Style
		//return Arrays.stream(data).reduce(Integer::sum).orElse(0);
	}
	
	public int calculateSumUsingDataService() {
		int sum = 0;
		int[] data = someDataService.retrieveAllData();
		for(int value:data) {
			sum += value;
		}
		
		//someDataService.storeSum(sum);
		return sum;
		//Functional Style
		//return Arrays.stream(data).reduce(Integer::sum).orElse(0);
	}

}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/controller/HelloWorldController.java

```java
package com.in28minutes.unittesting.unittesting.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

	@GetMapping("/hello-world")
	public String helloWorld() {
		return "Hello World";
	}
	
}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/controller/ItemController.java

```java
package com.in28minutes.unittesting.unittesting.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import com.in28minutes.unittesting.unittesting.business.ItemBusinessService;
import com.in28minutes.unittesting.unittesting.model.Item;

@RestController
public class ItemController {
	
	@Autowired
	private ItemBusinessService businessService;

	@GetMapping("/dummy-item")
	public Item dummyItem() {
		return new Item(1, "Ball", 10, 100);
	}
	
	@GetMapping("/item-from-business-service")
	public Item itemFromBusinessService() {
		Item item = businessService.retreiveHardcodedItem();
		
		return item;
	}
	
	@GetMapping("/all-items-from-database")
	public List<Item> retrieveAllItems() {
		return businessService.retrieveAllItems();
	}
	
}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/data/ItemRepository.java

```java
package com.in28minutes.unittesting.unittesting.data;

import org.springframework.data.jpa.repository.JpaRepository;

import com.in28minutes.unittesting.unittesting.model.Item;

public interface ItemRepository extends JpaRepository<Item, Integer>{

}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/data/SomeDataService.java

```java
package com.in28minutes.unittesting.unittesting.data;

public interface SomeDataService {

	int[] retrieveAllData();
	
	//int retrieveSpecificData();

}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/model/Item.java

```java
package com.in28minutes.unittesting.unittesting.model;

import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Transient;

@Entity
public class Item {

	@Id
	private int id;
	private String name;
	private int price;
	private int quantity;

	@Transient
	private int value;

	protected Item() {
		
	}
	
	public Item(int id, String name, int price, int quantity) {
		this.id = id;
		this.name = name;
		this.price = price;
		this.quantity = quantity;
	}

	public int getId() {
		return id;
	}

	public String getName() {
		return name;
	}

	public int getPrice() {
		return price;
	}

	public int getQuantity() {
		return quantity;
	}

	public int getValue() {
		return value;
	}

	public void setValue(int value) {
		this.value = value;
	}

	public String toString() {
		return String.format("Item[%d, %s, %d, %d]", id, name, price, quantity);
	}
}
```
---

### /src/main/java/com/in28minutes/unittesting/unittesting/UnitTestingApplication.java

```java
package com.in28minutes.unittesting.unittesting;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class UnitTestingApplication {

	public static void main(String[] args) {
		SpringApplication.run(UnitTestingApplication.class, args);
	}
}
```
---

### /src/main/resources/application.properties

```properties
spring.jpa.show-sql=true
spring.h2.console.enabled=true
```
---

### /src/main/resources/data.sql

```
insert into item(id, name, price, quantity) values(10001,'Item1',10,20);
insert into item(id, name, price, quantity) values(10002,'Item2',5,10);
insert into item(id, name, price, quantity) values(10003,'Item3',15,2);
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/business/ItemBusinessServiceTest.java

```java
package com.in28minutes.unittesting.unittesting.business;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.when;

import java.util.Arrays;
import java.util.List;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.MockitoJUnitRunner;

import com.in28minutes.unittesting.unittesting.data.ItemRepository;
import com.in28minutes.unittesting.unittesting.model.Item;

@RunWith(MockitoJUnitRunner.class)
public class ItemBusinessServiceTest {

	@InjectMocks
	private ItemBusinessService business;

	@Mock
	private ItemRepository repository;

	@Test
	public void retrieveAllItems_basic() {
		when(repository.findAll()).thenReturn(Arrays.asList(new Item(2,"Item2",10,10),
				new Item(3,"Item3",20,20)));
		List<Item> items = business.retrieveAllItems();
		
		assertEquals(100, items.get(0).getValue());
		assertEquals(400, items.get(1).getValue());
	}
}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/business/ListMockTest.java

```java
package com.in28minutes.unittesting.unittesting.business;

import static org.junit.Assert.assertEquals;
import static org.mockito.ArgumentMatchers.anyInt;
import static org.mockito.Mockito.atLeast;
import static org.mockito.Mockito.atLeastOnce;
import static org.mockito.Mockito.atMost;
import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.never;
import static org.mockito.Mockito.spy;
import static org.mockito.Mockito.times;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import java.util.ArrayList;
import java.util.List;

import org.junit.Ignore;
import org.junit.Test;
import org.mockito.ArgumentCaptor;

public class ListMockTest {

	List<String> mock = mock(List.class);

	@Test
	public void size_basic() {
		when(mock.size()).thenReturn(5);
		assertEquals(5, mock.size());
	}

	@Test
	public void returnDifferentValues() {
		when(mock.size()).thenReturn(5).thenReturn(10);
		assertEquals(5, mock.size());
		assertEquals(10, mock.size());
	}

	@Test
	@Ignore
	public void returnWithParameters() {
		when(mock.get(0)).thenReturn("in28Minutes");
		assertEquals("in28Minutes", mock.get(0));
		assertEquals(null, mock.get(1));
	}

	@Test
	public void returnWithGenericParameters() {
		when(mock.get(anyInt())).thenReturn("in28Minutes");

		assertEquals("in28Minutes", mock.get(0));
		assertEquals("in28Minutes", mock.get(1));
	}

	@Test
	public void verificationBasics() {
		// SUT
		String value1 = mock.get(0);
		String value2 = mock.get(1);

		// Verify
		verify(mock).get(0);
		verify(mock, times(2)).get(anyInt());
		verify(mock, atLeast(1)).get(anyInt());
		verify(mock, atLeastOnce()).get(anyInt());
		verify(mock, atMost(2)).get(anyInt());
		verify(mock, never()).get(2);
	}

	@Test
	public void argumentCapturing() {
		
		//SUT
		mock.add("SomeString");
		
		//Verification
		ArgumentCaptor<String> captor = ArgumentCaptor.forClass(String.class);
		verify(mock).add(captor.capture());
		
		assertEquals("SomeString", captor.getValue());
		
	}
	
	@Test
	public void multipleArgumentCapturing() {
		
		//SUT
		mock.add("SomeString1");
		mock.add("SomeString2");
		
		//Verification
		ArgumentCaptor<String> captor = ArgumentCaptor.forClass(String.class);
		
		verify(mock, times(2)).add(captor.capture());
		
		List<String> allValues = captor.getAllValues();
		
		assertEquals("SomeString1", allValues.get(0));
		assertEquals("SomeString2", allValues.get(1));
		
	}

	@Test
	public void mocking() {
		ArrayList arrayListMock = mock(ArrayList.class);
		System.out.println(arrayListMock.get(0));//null
		System.out.println(arrayListMock.size());//0
		arrayListMock.add("Test");
		arrayListMock.add("Test2");
		System.out.println(arrayListMock.size());//0
		when(arrayListMock.size()).thenReturn(5);
		System.out.println(arrayListMock.size());//5
	}

	@Test
	public void spying() {
		ArrayList arrayListSpy = spy(ArrayList.class);
		arrayListSpy.add("Test0");
		System.out.println(arrayListSpy.get(0));//Test0
		System.out.println(arrayListSpy.size());//1
		arrayListSpy.add("Test");
		arrayListSpy.add("Test2");
		System.out.println(arrayListSpy.size());//3
		
		when(arrayListSpy.size()).thenReturn(5);
		System.out.println(arrayListSpy.size());//5
		
		arrayListSpy.add("Test4");
		System.out.println(arrayListSpy.size());//5
		
		verify(arrayListSpy).add("Test4");
	}

	
}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/business/SomeBusinessMockTest.java

```java
package com.in28minutes.unittesting.unittesting.business;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.when;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.MockitoJUnitRunner;

import com.in28minutes.unittesting.unittesting.data.SomeDataService;

@RunWith(MockitoJUnitRunner.class)
public class SomeBusinessMockTest {

	@InjectMocks
	SomeBusinessImpl business;

	@Mock
	SomeDataService dataServiceMock;

	@Test
	public void calculateSumUsingDataService_basic() {
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] { 1, 2, 3 });
		assertEquals(6, business.calculateSumUsingDataService());
	}

	@Test
	public void calculateSumUsingDataService_empty() {
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] {});
		assertEquals(0, business.calculateSumUsingDataService());
	}

	@Test
	public void calculateSumUsingDataService_oneValue() {
		when(dataServiceMock.retrieveAllData()).thenReturn(new int[] { 5 });
		assertEquals(5, business.calculateSumUsingDataService());
	}
}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/business/SomeBusinessStubTest.java

```java
package com.in28minutes.unittesting.unittesting.business;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

import com.in28minutes.unittesting.unittesting.data.SomeDataService;

class SomeDataServiceStub implements SomeDataService {
	@Override
	public int[] retrieveAllData() {
		return new int[] { 1, 2, 3 };
	}
}

class SomeDataServiceEmptyStub implements SomeDataService {
	@Override
	public int[] retrieveAllData() {
		return new int[] { };
	}
}

class SomeDataServiceOneElementStub implements SomeDataService {
	@Override
	public int[] retrieveAllData() {
		return new int[] { 5 };
	}
}

public class SomeBusinessStubTest {

	@Test
	public void calculateSumUsingDataService_basic() {
		SomeBusinessImpl business = new SomeBusinessImpl();
		business.setSomeDataService(new SomeDataServiceStub());
		int actualResult = business.calculateSumUsingDataService();
		int expectedResult = 6;
		assertEquals(expectedResult, actualResult);
	}

	@Test
	public void calculateSumUsingDataService_empty() {
		SomeBusinessImpl business = new SomeBusinessImpl();
		business.setSomeDataService(new SomeDataServiceEmptyStub());
		int actualResult = business.calculateSumUsingDataService();//new int[] {}
		int expectedResult = 0;
		assertEquals(expectedResult, actualResult);
	}

	@Test
	public void calculateSumUsingDataService_oneValue() {
		SomeBusinessImpl business = new SomeBusinessImpl();
		business.setSomeDataService(new SomeDataServiceOneElementStub());
		int actualResult = business.calculateSumUsingDataService();//new int[] { 5 }
		int expectedResult = 5;
		assertEquals(expectedResult, actualResult);
	}
}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/business/SomeBusinessTest.java

```java
package com.in28minutes.unittesting.unittesting.business;

import static org.junit.Assert.*;

import org.junit.Test;

public class SomeBusinessTest {

	@Test
	public void calculateSum_basic() {
		SomeBusinessImpl business = new SomeBusinessImpl();
		int actualResult = business.calculateSum(new int[] { 1,2,3});
		int expectedResult = 6;
		assertEquals(expectedResult, actualResult);	
	}

	@Test
	public void calculateSum_empty() {
		SomeBusinessImpl business = new SomeBusinessImpl();
		int actualResult = business.calculateSum(new int[] { });
		int expectedResult = 0;
		assertEquals(expectedResult, actualResult);	
	}

	@Test
	public void calculateSum_oneValue() {
		SomeBusinessImpl business = new SomeBusinessImpl();
		int actualResult = business.calculateSum(new int[] { 5});
		int expectedResult = 5;
		assertEquals(expectedResult, actualResult);	
	}
}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/controller/HelloWorldControllerTest.java

```java
package com.in28minutes.unittesting.unittesting.controller;

import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.http.MediaType;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.MvcResult;
import org.springframework.test.web.servlet.RequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

@RunWith(SpringRunner.class)
@WebMvcTest(HelloWorldController.class)
public class HelloWorldControllerTest {
	
	@Autowired
	private MockMvc mockMvc;
	
	@Test
	public void helloWorld_basic() throws Exception {
		//call GET "/hello-world"  application/json
		
		RequestBuilder request = MockMvcRequestBuilders
				.get("/hello-world")
				.accept(MediaType.APPLICATION_JSON);
		
		MvcResult result = mockMvc.perform(request)
				.andExpect(status().isOk())
				.andExpect(content().string("Hello World"))
				.andReturn();
	
		//verify "Hello World"
		//assertEquals("Hello World", result.getResponse().getContentAsString());
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/controller/ItemControllerIT.java

```java
package com.in28minutes.unittesting.unittesting.controller;

import org.json.JSONException;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.skyscreamer.jsonassert.JSONAssert;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment=WebEnvironment.RANDOM_PORT)
public class ItemControllerIT {
	
	@Autowired
	private TestRestTemplate restTemplate;
		
	@Test
	public void contextLoads() throws JSONException {	
		
		String response = this.restTemplate.getForObject("/all-items-from-database", String.class);
		
		JSONAssert.assertEquals("[{id:10001},{id:10002},{id:10003}]", 
				response, false);
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/controller/ItemControllerTest.java

```java
package com.in28minutes.unittesting.unittesting.controller;

import static org.mockito.Mockito.when;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import java.util.Arrays;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.MvcResult;
import org.springframework.test.web.servlet.RequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

import com.in28minutes.unittesting.unittesting.business.ItemBusinessService;
import com.in28minutes.unittesting.unittesting.model.Item;

@RunWith(SpringRunner.class)
@WebMvcTest(ItemController.class)
public class ItemControllerTest {
	
	@Autowired
	private MockMvc mockMvc;
	
	@MockBean
	private ItemBusinessService businessService;
	
	@Test
	public void dummyItem_basic() throws Exception {
		
		RequestBuilder request = MockMvcRequestBuilders
				.get("/dummy-item")
				.accept(MediaType.APPLICATION_JSON);
		
		MvcResult result = mockMvc.perform(request)
				.andExpect(status().isOk())
				.andExpect(content().json("{\"id\": 1,\"name\":\"Ball\",\"price\":10,\"quantity\":100}"))
				.andReturn();
		//JSONAssert.assertEquals(expected, result.getResponse().getContentAsString(), false);
		
	}

	@Test
	public void itemFromBusinessService_basic() throws Exception {
		when(businessService.retreiveHardcodedItem()).thenReturn(
				new Item(2,"Item2",10,10));
		
		RequestBuilder request = MockMvcRequestBuilders
				.get("/item-from-business-service")
				.accept(MediaType.APPLICATION_JSON);
		
		MvcResult result = mockMvc.perform(request)
				.andExpect(status().isOk())
				.andExpect(content().json("{id:2,name:Item2,price:10}"))
				.andReturn();
		//JSONAssert.assertEquals(expected, result.getResponse().getContentAsString(), false);
		
	}
	
	@Test
	public void retrieveAllItems_basic() throws Exception {
		when(businessService.retrieveAllItems()).thenReturn(
				Arrays.asList(new Item(2,"Item2",10,10),
						new Item(3,"Item3",20,20))
				);
		
		RequestBuilder request = MockMvcRequestBuilders
				.get("/all-items-from-database")
				.accept(MediaType.APPLICATION_JSON);
		
		MvcResult result = mockMvc.perform(request)
				.andExpect(status().isOk())
				.andExpect(content().json("[{id:3,name:Item3,price:20}, {id:2,name:Item2,price:10}]"))
				.andReturn();
		//JSONAssert.assertEquals(expected, result.getResponse().getContentAsString(), false);
		
	}

	@Test
	public void retrieveAllItems_noitems() throws Exception {
		when(businessService.retrieveAllItems()).thenReturn(
				Arrays.asList()
				);
		
		RequestBuilder request = MockMvcRequestBuilders
				.get("/all-items-from-database")
				.accept(MediaType.APPLICATION_JSON);
		
		MvcResult result = mockMvc.perform(request)
				.andExpect(status().isOk())
				.andExpect(content().json("[]"))
				.andReturn();
		//JSONAssert.assertEquals(expected, result.getResponse().getContentAsString(), false);
		
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/data/ItemRepositoryTest.java

```java
package com.in28minutes.unittesting.unittesting.data;

import static org.junit.Assert.assertEquals;

import java.util.List;
import java.util.Optional;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.test.context.junit4.SpringRunner;

import com.in28minutes.unittesting.unittesting.model.Item;

@RunWith(SpringRunner.class)
@DataJpaTest
public class ItemRepositoryTest {
	
	@Autowired
	private ItemRepository repository;
	
	@Test
	public void testFindAll() {
		List<Item> items = repository.findAll();
		assertEquals(3,items.size());
	}

	@Test
	public void testFindOne() {
		Item item = repository.findById(10001).get();
		
		assertEquals("Item1",item.getName());
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/spike/AssertJTest.java

```java
package com.in28minutes.unittesting.unittesting.spike;

import static org.assertj.core.api.Assertions.assertThat;

import java.util.Arrays;
import java.util.List;

import org.junit.Test;

public class AssertJTest {
	
	@Test
	public void learning() {
		List<Integer> numbers = Arrays.asList(12,15,45);
		
		//assertThat(numbers, hasSize(3));
		assertThat(numbers).hasSize(3)
						.contains(12,15)
						.allMatch(x -> x > 10)
						.allMatch(x -> x < 100)
						.noneMatch(x -> x < 0);
		
		assertThat("").isEmpty();
		assertThat("ABCDE").contains("BCD")
						.startsWith("ABC")
						.endsWith("CDE");		
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/spike/HamcrestMatchersTest.java

```java
package com.in28minutes.unittesting.unittesting.spike;

import static org.hamcrest.CoreMatchers.everyItem;
import static org.hamcrest.CoreMatchers.hasItems;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.Matchers.containsString;
import static org.hamcrest.Matchers.endsWith;
import static org.hamcrest.Matchers.greaterThan;
import static org.hamcrest.Matchers.hasSize;
import static org.hamcrest.Matchers.isEmptyString;
import static org.hamcrest.Matchers.lessThan;
import static org.hamcrest.Matchers.startsWith;

import java.util.Arrays;
import java.util.List;

import org.junit.Test;

public class HamcrestMatchersTest {
	
	@Test
	public void learning() {
		List<Integer> numbers = Arrays.asList(12,15,45);
		
		assertThat(numbers, hasSize(3));
		assertThat(numbers, hasItems(12,45));
		assertThat(numbers, everyItem(greaterThan(10)));
		assertThat(numbers, everyItem(lessThan(100)));
		
		assertThat("", isEmptyString());
		assertThat("ABCDE", containsString("BCD"));
		assertThat("ABCDE", startsWith("ABC"));
		assertThat("ABCDE", endsWith("CDE"));
				
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/spike/JsonAssertTest.java

```java
package com.in28minutes.unittesting.unittesting.spike;

import org.json.JSONException;
import org.junit.Test;
import org.skyscreamer.jsonassert.JSONAssert;

public class JsonAssertTest {
	
	String actualResponse = "{\"id\":1,\"name\":\"Ball\",\"price\":10,\"quantity\":100}";
	
	@Test
	public void jsonAssert_StrictTrue_ExactMatchExceptForSpaces() throws JSONException {
		String expectedResponse = "{\"id\": 1, \"name\":\"Ball\", \"price\":10, \"quantity\":100}";
		JSONAssert.assertEquals(expectedResponse, actualResponse, true);
	}

	@Test
	public void jsonAssert_StrictFalse() throws JSONException {
		String expectedResponse = "{\"id\": 1, \"name\":\"Ball\", \"price\":10}";
		JSONAssert.assertEquals(expectedResponse, actualResponse, false);
	}

	@Test
	public void jsonAssert_WithoutEscapeCharacters() throws JSONException {
		String expectedResponse = "{id:1, name:Ball, price:10}";
		JSONAssert.assertEquals(expectedResponse, actualResponse, false);
	}
}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/spike/JsonPathTest.java

```java
package com.in28minutes.unittesting.unittesting.spike;

import static org.assertj.core.api.Assertions.assertThat;

import java.util.List;

import org.junit.Test;

import com.jayway.jsonpath.DocumentContext;
import com.jayway.jsonpath.JsonPath;

public class JsonPathTest {
	
	@Test
	public void learning() {
		String responseFromService = "[" + 
				"{\"id\":10000, \"name\":\"Pencil\", \"quantity\":5}," + 
				"{\"id\":10001, \"name\":\"Pen\", \"quantity\":15}," + 
				"{\"id\":10002, \"name\":\"Eraser\", \"quantity\":10}" + 
				"]";
		
		DocumentContext context = JsonPath.parse(responseFromService);
		
		int length = context.read("$.length()");
		assertThat(length).isEqualTo(3);
		
		List<Integer> ids = context.read("$..id");

		assertThat(ids).containsExactly(10000,10001,10002);
		
		System.out.println(context.read("$.[1]").toString());
		System.out.println(context.read("$.[0:2]").toString());
		System.out.println(context.read("$.[?(@.name=='Eraser')]").toString());
		System.out.println(context.read("$.[?(@.quantity==5)]").toString());
		
	}

}
```
---

### /src/test/java/com/in28minutes/unittesting/unittesting/UnitTestingApplicationTests.java

```java
package com.in28minutes.unittesting.unittesting;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
//@TestPropertySource(locations= {"classpath:test-configuration.properties"})
public class UnitTestingApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /src/test/resources/application.properties

```properties
spring.jpa.show-sql=false
spring.h2.console.enabled=false
```
---

# Your First Full Stack Application with React and Spring Boot

## Complete Code Example


### /frontend/todo-app/public/index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <meta name="theme-color" content="#000000" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>My Todo Application</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```
---

### /frontend/todo-app/public/manifest.json

```json
{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    }
  ],
  "start_url": ".",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```
---

### /frontend/todo-app/src/Constants.js

```js
export const API_URL = 'http://localhost:8080'
export const JPA_API_URL = 'http://localhost:8080/jpa'
```
---

### /frontend/todo-app/src/bootstrap.css

```css
@import url(https://unpkg.com/bootstrap@4.1.0/dist/css/bootstrap.min.css)
```
---

### /frontend/todo-app/src/App.css

```css
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 40px;
  background-color: #222222;
}

.App {
  text-align: center;
}

.App-logo {
  animation: App-logo-spin infinite 20s linear;
  height: 40vmin;
  pointer-events: none;
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```
---

### /frontend/todo-app/src/index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```
---

### /frontend/todo-app/src/index.css

```css
body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
    monospace;
}
```
---

### /frontend/todo-app/src/components/todo/WelcomeComponent.jsx

```
import React, { Component } from 'react'
import { Link } from 'react-router-dom'
import HelloWorldService from '../../api/todo/HelloWorldService.js'

class WelcomeComponent extends Component {

    constructor(props) {
        super(props)
        this.retrieveWelcomeMessage = this.retrieveWelcomeMessage.bind(this)
        this.state = {
            welcomeMessage: ''
        }
        this.handleSuccessfulResponse = this.handleSuccessfulResponse.bind(this)
        this.handleError = this.handleError.bind(this)
    }

    render() {
        return (
            <>
                <h1>Welcome!</h1>
                <div className="container">
                    Welcome {this.props.match.params.name}.
                    You can manage your todos <Link to="/todos">here</Link>.
                </div>
                <div className="container">
                    Click here to get a customized welcome message.
                    <button onClick={this.retrieveWelcomeMessage}
                        className="btn btn-success">Get Welcome Message</button>
                </div>
                <div className="container">
                    {this.state.welcomeMessage}
                </div>

            </>
        )
    }

    retrieveWelcomeMessage() {
        // HelloWorldService.executeHelloWorldService()
        // .then( response => this.handleSuccessfulResponse(response) )

        // HelloWorldService.executeHelloWorldBeanService()
        // .then( response => this.handleSuccessfulResponse(response) )

        HelloWorldService.executeHelloWorldPathVariableService(this.props.match.params.name)
            .then(response => this.handleSuccessfulResponse(response))
            .catch(error => this.handleError(error))
    }

    handleSuccessfulResponse(response) {
        console.log(response)
        this.setState({ welcomeMessage: response.data.message })
    }

    handleError(error) {

        console.log(error.response)

        let errorMessage = '';

        if (error.message)
            errorMessage += error.message

        if (error.response && error.response.data) {
            errorMessage += error.response.data.message
        }

        this.setState({ welcomeMessage: errorMessage })
    }

}


export default WelcomeComponent
```
---

### /frontend/todo-app/src/components/todo/ListTodosComponent.jsx

```
import React, { Component } from 'react'
import TodoDataService from '../../api/todo/TodoDataService.js'
import AuthenticationService from './AuthenticationService.js'
import moment from 'moment'

class ListTodosComponent extends Component {
    constructor(props) {
        console.log('constructor')
        super(props)
        this.state = {
            todos: [],
            message: null
        }
        this.deleteTodoClicked = this.deleteTodoClicked.bind(this)
        this.updateTodoClicked = this.updateTodoClicked.bind(this)
        this.addTodoClicked = this.addTodoClicked.bind(this)
        this.refreshTodos = this.refreshTodos.bind(this)
    }

    componentWillUnmount() {
        console.log('componentWillUnmount')
    }

    shouldComponentUpdate(nextProps, nextState) {
        console.log('shouldComponentUpdate')
        console.log(nextProps)
        console.log(nextState)
        return true
    }

    componentDidMount() {
        console.log('componentDidMount')
        this.refreshTodos();
        console.log(this.state)
    }

    refreshTodos() {
        let username = AuthenticationService.getLoggedInUserName()
        TodoDataService.retrieveAllTodos(username)
            .then(
                response => {
                    //console.log(response);
                    this.setState({ todos: response.data })
                }
            )
    }

    deleteTodoClicked(id) {
        let username = AuthenticationService.getLoggedInUserName()
        //console.log(id + " " + username);
        TodoDataService.deleteTodo(username, id)
            .then(
                response => {
                    this.setState({ message: `Delete of todo ${id} Successful` })
                    this.refreshTodos()
                }
            )

    }

    addTodoClicked() {
        this.props.history.push(`/todos/-1`)
    }

    updateTodoClicked(id) {
        console.log('update ' + id)
        this.props.history.push(`/todos/${id}`)
        // /todos/${id}
        // let username = AuthenticationService.getLoggedInUserName()
        // //console.log(id + " " + username);
        // TodoDataService.deleteTodo(username, id)
        //  .then (
        //      response => {
        //         this.setState({message : `Delete of todo ${id} Successful`})
        //         this.refreshTodos()
        //      }
        //  )

    }

    render() {
        console.log('render')
        return (
            <div>
                <h1>List Todos</h1>
                {this.state.message && <div class="alert alert-success">{this.state.message}</div>}
                <div className="container">
                    <table className="table">
                        <thead>
                            <tr>
                                <th>Description</th>
                                <th>Target Date</th>
                                <th>IsCompleted?</th>
                                <th>Update</th>
                                <th>Delete</th>
                            </tr>
                        </thead>
                        <tbody>
                            {
                                this.state.todos.map(
                                    todo =>
                                        <tr key={todo.id}>
                                            <td>{todo.description}</td>
                                            <td>{moment(todo.targetDate).format('YYYY-MM-DD')}</td>
                                            <td>{todo.done.toString()}</td>
                                            <td><button className="btn btn-success" onClick={() => this.updateTodoClicked(todo.id)}>Update</button></td>
                                            <td><button className="btn btn-warning" onClick={() => this.deleteTodoClicked(todo.id)}>Delete</button></td>
                                        </tr>
                                )
                            }
                        </tbody>
                    </table>
                    <div className="row">
                        <button className="btn btn-success" onClick={this.addTodoClicked}>Add</button>
                    </div>
                </div>
            </div>
        )
    }
}

export default ListTodosComponent
```
---

### /frontend/todo-app/src/components/todo/HeaderComponent.jsx

```
import React, { Component } from 'react'
import { Link } from 'react-router-dom'
import AuthenticationService from './AuthenticationService.js'


class HeaderComponent extends Component {
    render() {
        const isUserLoggedIn = AuthenticationService.isUserLoggedIn();
        //console.log(isUserLoggedIn);

        return (
            <header>
                <nav className="navbar navbar-expand-md navbar-dark bg-dark">
                    <div><a href="http://www.in28minutes.com" className="navbar-brand">in28Minutes</a></div>
                    <ul className="navbar-nav">
                        {isUserLoggedIn && <li><Link className="nav-link" to="/welcome/in28minutes">Home</Link></li>}
                        {isUserLoggedIn && <li><Link className="nav-link" to="/todos">Todos</Link></li>}
                    </ul>
                    <ul className="navbar-nav navbar-collapse justify-content-end">
                        {!isUserLoggedIn && <li><Link className="nav-link" to="/login">Login</Link></li>}
                        {isUserLoggedIn && <li><Link className="nav-link" to="/logout" onClick={AuthenticationService.logout}>Logout</Link></li>}
                    </ul>
                </nav>
            </header>
        )
    }
}

export default HeaderComponent
```
---

### /frontend/todo-app/src/components/todo/AuthenticatedRoute.jsx

```
import React, { Component } from 'react'
import { Route, Redirect } from 'react-router-dom'
import AuthenticationService from './AuthenticationService.js'

class AuthenticatedRoute extends Component {
    render() {
        if (AuthenticationService.isUserLoggedIn()) {
            return <Route {...this.props} />
        } else {
            return <Redirect to="/login" />
        }

    }
}

export default AuthenticatedRoute
```
---

### /frontend/todo-app/src/components/todo/FooterComponent.jsx

```
import React, { Component } from 'react'

class FooterComponent extends Component {
    render() {
        return (
            <footer className="footer">
                <span className="text-muted">All Rights Reserved 2018 @in28minutes</span>
            </footer>
        )
    }
}

export default FooterComponent
```
---

### /frontend/todo-app/src/components/todo/LoginComponent.jsx

```
import React, { Component } from 'react'
import AuthenticationService from './AuthenticationService.js'

class LoginComponent extends Component {

    constructor(props) {
        super(props)

        this.state = {
            username: 'in28minutes',
            password: '',
            hasLoginFailed: false,
            showSuccessMessage: false
        }
        // this.handleUsernameChange = this.handleUsernameChange.bind(this)
        // this.handlePasswordChange = this.handlePasswordChange.bind(this)
        this.handleChange = this.handleChange.bind(this)
        this.loginClicked = this.loginClicked.bind(this)
    }

    handleChange(event) {
        //console.log(this.state);
        this.setState(
            {
                [event.target.name]
                    : event.target.value
            }
        )
    }

    // handleUsernameChange(event) {
    //     console.log(event.target.name);
    //     this.setState(
    //         {
    //             [event.target.name]
    //               :event.target.value
    //         }
    //     )
    // }

    // handlePasswordChange(event) {
    //     console.log(event.target.value);
    //     this.setState({password:event.target.value})
    // }

    loginClicked() {
        //in28minutes,dummy
        // if(this.state.username==='in28minutes' && this.state.password==='dummy'){
        //     AuthenticationService.registerSuccessfulLogin(this.state.username,this.state.password)
        //     this.props.history.push(`/welcome/${this.state.username}`)
        //     //this.setState({showSuccessMessage:true})
        //     //this.setState({hasLoginFailed:false})
        // }
        // else {
        //     this.setState({showSuccessMessage:false})
        //     this.setState({hasLoginFailed:true})
        // }

        // AuthenticationService
        // .executeBasicAuthenticationService(this.state.username, this.state.password)
        // .then(() => {
        //     AuthenticationService.registerSuccessfulLogin(this.state.username,this.state.password)
        //     this.props.history.push(`/welcome/${this.state.username}`)
        // }).catch( () =>{
        //     this.setState({showSuccessMessage:false})
        //     this.setState({hasLoginFailed:true})
        // })
        AuthenticationService
            .executeJwtAuthenticationService(this.state.username, this.state.password)
            .then((response) => {
                AuthenticationService.registerSuccessfulLoginForJwt(this.state.username, response.data.token)
                this.props.history.push(`/welcome/${this.state.username}`)
            }).catch(() => {
                this.setState({ showSuccessMessage: false })
                this.setState({ hasLoginFailed: true })
            })

    }

    render() {
        return (
            <div>
                <h1>Login</h1>
                <div className="container">
                    {/*<ShowInvalidCredentials hasLoginFailed={this.state.hasLoginFailed}/>*/}
                    {this.state.hasLoginFailed && <div className="alert alert-warning">Invalid Credentials</div>}
                    {this.state.showSuccessMessage && <div>Login Sucessful</div>}
                    {/*<ShowLoginSuccessMessage showSuccessMessage={this.state.showSuccessMessage}/>*/}
                    User Name: <input type="text" name="username" value={this.state.username} onChange={this.handleChange} />
                    Password: <input type="password" name="password" value={this.state.password} onChange={this.handleChange} />
                    <button className="btn btn-success" onClick={this.loginClicked}>Login</button>
                </div>
            </div>
        )
    }
}

export default LoginComponent
```
---

### /frontend/todo-app/src/components/todo/TodoComponent.jsx

```
import React, { Component } from 'react'
import moment from 'moment'
import { Formik, Form, Field, ErrorMessage } from 'formik';
import TodoDataService from '../../api/todo/TodoDataService.js'
import AuthenticationService from './AuthenticationService.js'

class TodoComponent extends Component {
    constructor(props) {
        super(props)

        this.state = {
            id: this.props.match.params.id,
            description: '',
            targetDate: moment(new Date()).format('YYYY-MM-DD')
        }

        this.onSubmit = this.onSubmit.bind(this)
        this.validate = this.validate.bind(this)

    }

    componentDidMount() {

        if (this.state.id === -1) {
            return
        }

        let username = AuthenticationService.getLoggedInUserName()

        TodoDataService.retrieveTodo(username, this.state.id)
            .then(response => this.setState({
                description: response.data.description,
                targetDate: moment(response.data.targetDate).format('YYYY-MM-DD')
            }))
    }

    validate(values) {
        let errors = {}
        if (!values.description) {
            errors.description = 'Enter a Description'
        } else if (values.description.length < 5) {
            errors.description = 'Enter atleast 5 Characters in Description'
        }

        if (!moment(values.targetDate).isValid()) {
            errors.targetDate = 'Enter a valid Target Date'
        }

        return errors

    }

    onSubmit(values) {
        let username = AuthenticationService.getLoggedInUserName()

        let todo = {
            id: this.state.id,
            description: values.description,
            targetDate: values.targetDate
        }

        if (this.state.id === -1) {
            TodoDataService.createTodo(username, todo)
                .then(() => this.props.history.push('/todos'))
        } else {
            TodoDataService.updateTodo(username, this.state.id, todo)
                .then(() => this.props.history.push('/todos'))
        }

        console.log(values);
    }

    render() {

        let { description, targetDate } = this.state
        //let targetDate = this.state.targetDate

        return (
            <div>
                <h1>Todo</h1>
                <div className="container">
                    <Formik
                        initialValues={{ description, targetDate }}
                        onSubmit={this.onSubmit}
                        validateOnChange={false}
                        validateOnBlur={false}
                        validate={this.validate}
                        enableReinitialize={true}
                    >
                        {
                            (props) => (
                                <Form>
                                    <ErrorMessage name="description" component="div"
                                        className="alert alert-warning" />
                                    <ErrorMessage name="targetDate" component="div"
                                        className="alert alert-warning" />
                                    <fieldset className="form-group">
                                        <label>Description</label>
                                        <Field className="form-control" type="text" name="description" />
                                    </fieldset>
                                    <fieldset className="form-group">
                                        <label>Target Date</label>
                                        <Field className="form-control" type="date" name="targetDate" />
                                    </fieldset>
                                    <button className="btn btn-success" type="submit">Save</button>
                                </Form>
                            )
                        }
                    </Formik>

                </div>
            </div>
        )
    }
}

export default TodoComponent
```
---

### /frontend/todo-app/src/components/todo/AuthenticationService.js

```js
import axios from 'axios'
import { API_URL } from '../../Constants'

export const USER_NAME_SESSION_ATTRIBUTE_NAME = 'authenticatedUser'

class AuthenticationService {

    executeBasicAuthenticationService(username, password) {
        return axios.get(`${API_URL}/basicauth`,
            { headers: { authorization: this.createBasicAuthToken(username, password) } })
    }

    executeJwtAuthenticationService(username, password) {
        return axios.post(`${API_URL}/authenticate`, {
            username,
            password
        })
    }

    createBasicAuthToken(username, password) {
        return 'Basic ' + window.btoa(username + ":" + password)
    }

    registerSuccessfulLogin(username, password) {
        //let basicAuthHeader = 'Basic ' +  window.btoa(username + ":" + password)
        //console.log('registerSuccessfulLogin')
        sessionStorage.setItem(USER_NAME_SESSION_ATTRIBUTE_NAME, username)
        this.setupAxiosInterceptors(this.createBasicAuthToken(username, password))
    }

    registerSuccessfulLoginForJwt(username, token) {
        sessionStorage.setItem(USER_NAME_SESSION_ATTRIBUTE_NAME, username)
        this.setupAxiosInterceptors(this.createJWTToken(token))
    }

    createJWTToken(token) {
        return 'Bearer ' + token
    }


    logout() {
        sessionStorage.removeItem(USER_NAME_SESSION_ATTRIBUTE_NAME);
    }

    isUserLoggedIn() {
        let user = sessionStorage.getItem(USER_NAME_SESSION_ATTRIBUTE_NAME)
        if (user === null) return false
        return true
    }

    getLoggedInUserName() {
        let user = sessionStorage.getItem(USER_NAME_SESSION_ATTRIBUTE_NAME)
        if (user === null) return ''
        return user
    }

    setupAxiosInterceptors(token) {

        axios.interceptors.request.use(
            (config) => {
                if (this.isUserLoggedIn()) {
                    config.headers.authorization = token
                }
                return config
            }
        )
    }
}

export default new AuthenticationService()
```
---

### /frontend/todo-app/src/components/todo/ErrorComponent.jsx

```
import React from 'react'

function ErrorComponent() {
    return <div>An Error Occurred. I don't know what to do! Contact support at abcd-efgh-ijkl</div>
}

export default ErrorComponent
```
---

### /frontend/todo-app/src/components/todo/TodoApp.jsx

```
import React, {Component} from 'react'
import {BrowserRouter as Router, Route, Switch} from 'react-router-dom'
import AuthenticatedRoute from './AuthenticatedRoute.jsx'
import LoginComponent from './LoginComponent.jsx'
import ListTodosComponent from './ListTodosComponent.jsx'
import ErrorComponent from './ErrorComponent.jsx'
import HeaderComponent from './HeaderComponent.jsx'
import FooterComponent from './FooterComponent.jsx'
import LogoutComponent from './LogoutComponent.jsx'
import WelcomeComponent from './WelcomeComponent.jsx'
import TodoComponent from './TodoComponent.jsx'

class TodoApp extends Component {
    render() {
        return (
            <div className="TodoApp">
                <Router>
                    <>
                        <HeaderComponent/>
                        <Switch>
                            <Route path="/" exact component={LoginComponent}/>
                            <Route path="/login" component={LoginComponent}/>
                            <AuthenticatedRoute path="/welcome/:name" component={WelcomeComponent}/>
                            <AuthenticatedRoute path="/todos/:id" component={TodoComponent}/>
                            <AuthenticatedRoute path="/todos" component={ListTodosComponent}/>
                            <AuthenticatedRoute path="/logout" component={LogoutComponent}/>
                            
                            <Route component={ErrorComponent}/>
                        </Switch>
                        <FooterComponent/>
                    </>
                </Router>
                {/*<LoginComponent/>
                <WelcomeComponent/>*/}
            </div>
        )
    }
}

export default TodoApp
```
---

### /frontend/todo-app/src/components/todo/LogoutComponent.jsx

```
import React, { Component } from 'react'

class LogoutComponent extends Component {
    render() {
        return (
            <>
                <h1>You are logged out</h1>
                <div className="container">
                    Thank You for Using Our Application.
                </div>
            </>
        )
    }
}

export default LogoutComponent
```
---

### /frontend/todo-app/src/components/learning-examples/FirstComponent.jsx

```
import React, { Component } from 'react'

//Class Component
class FirstComponent extends Component {
  render() {
    return (
      <div className="firstComponent">
        FirstComponent
        </div>
    )
  }
}

export default FirstComponent
```
---

### /frontend/todo-app/src/components/learning-examples/ThirdComponent.jsx

```
import React from 'react'

function ThirdComponent() {
  return (
    <div className="thirdComponent">
      Third Component
    </div>
  )
}

export default ThirdComponent
```
---

### /frontend/todo-app/src/components/learning-examples/SecondComponent.jsx

```
import React, { Component } from 'react'

class SecondComponent extends Component {
  render() {
    return (
      <div className="secondComponent">
        Second Component
        </div>
    )
  }
}

export default SecondComponent
```
---

### /frontend/todo-app/src/components/counter/Counter.css

```css
/*
button {
    background-color: green;
    font-size : 16px;
    padding : 15px 30px;
    color : white;
    width : 100px;
}

.count {
    font-size : 50px;
    padding : 15px 30px;
}

.reset {
    background-color: red;
    width : 200px;
}

body {
    padding : 15px 30px;
}
*/
```
---

### /frontend/todo-app/src/components/counter/Counter.jsx

```
import React, { Component } from 'react'
import PropTypes from 'prop-types'
import './Counter.css'

class Counter extends Component {

    constructor() {

        super(); //Error 1

        this.state = {
            counter: 0
        }

        this.increment = this.increment.bind(this);
        this.decrement = this.decrement.bind(this);
        this.reset = this.reset.bind(this);
    }

    render() {
        return (
            <div className="counter">
                <CounterButton by={1} incrementMethod={this.increment} decrementMethod={this.decrement} />
                <CounterButton by={5} incrementMethod={this.increment} decrementMethod={this.decrement} />
                <CounterButton by={10} incrementMethod={this.increment} decrementMethod={this.decrement} />
                <span className="count">{this.state.counter}</span>
                <div><button className="reset" onClick={this.reset}>Reset</button></div>
            </div>
        );
    }

    reset() {
        this.setState({ counter: 0 });
    }

    increment(by) {
        //console.log(`increment from child - ${by}`)
        this.setState(
            (prevState) => {
                return { counter: prevState.counter + by }
            }
        );
    }

    decrement(by) {
        //console.log(`increment from child - ${by}`)
        this.setState(
            (prevState) => {
                return { counter: prevState.counter - by }
            }
        );
    }

}

class CounterButton extends Component {
    //Define the initial state in a constructor
    //state => counter 0
    //constructor() {
    //    super(); //Error 1

    //   this.state = {
    //       counter : 0
    //   }

    //   this.increment = this.increment.bind(this);
    //   this.decrement = this.decrement.bind(this);
    //}

    render() {
        //render = () =>  {
        //const style = {fontSize : "50px", padding : "15px 30px"};
        return (
            <div className="counter">
                <button onClick={() => this.props.incrementMethod(this.props.by)} >+{this.props.by}</button>
                <button onClick={() => this.props.decrementMethod(this.props.by)} >-{this.props.by}</button>
                {/*<span className="count" 
            >{this.state.counter}</span>*/}
            </div>
        )
    }

    //   increment() { //Update state - counter++
    //    //console.log('increment');
    //     //this.state.counter++; //Bad Practice
    //     this.setState({
    //         counter: this.state.counter + this.props.by
    //     });

    //     this.props.incrementMethod(this.props.by);
    //   }

    //   decrement () {
    //     this.setState({
    //         counter: this.state.counter - this.props.by
    //     });

    //     this.props.decrementMethod(this.props.by);
    //   }
}

CounterButton.defaultProps = {
    by: 1
}

CounterButton.propTypes = {
    by: PropTypes.number
}

export default Counter
```
---

### /frontend/todo-app/src/App.test.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

it('renders without crashing', () => {
  const div = document.createElement('div');
  ReactDOM.render(<App />, div);
  ReactDOM.unmountComponentAtNode(div);
});
```
---

### /frontend/todo-app/src/api/todo/TodoDataService.js

```js
import axios from 'axios'
import { API_URL, JPA_API_URL } from '../../Constants'

class TodoDataService {

    retrieveAllTodos(name) {
        //console.log('executed service')
        return axios.get(`${JPA_API_URL}/users/${name}/todos`);
    }

    retrieveTodo(name, id) {
        //console.log('executed service')
        return axios.get(`${JPA_API_URL}/users/${name}/todos/${id}`);
    }

    deleteTodo(name, id) {
        //console.log('executed service')
        return axios.delete(`${JPA_API_URL}/users/${name}/todos/${id}`);
    }

    updateTodo(name, id, todo) {
        //console.log('executed service')
        return axios.put(`${JPA_API_URL}/users/${name}/todos/${id}`, todo);
    }

    createTodo(name, todo) {
        //console.log('executed service')
        return axios.post(`${JPA_API_URL}/users/${name}/todos/`, todo);
    }

}

export default new TodoDataService()
```
---

### /frontend/todo-app/src/api/todo/HelloWorldService.js

```js
import axios from 'axios'

class HelloWorldService {

    executeHelloWorldService() {
        //console.log('executed service')
        return axios.get('http://localhost:8080/hello-world');
    }

    executeHelloWorldBeanService() {
        //console.log('executed service')
        return axios.get('http://localhost:8080/hello-world-bean');
    }

    executeHelloWorldPathVariableService(name) {
        //console.log('executed service')
        // let username = 'in28minutes'
        // let password = 'dummy'

        // let basicAuthHeader = 'Basic ' +  window.btoa(username + ":" + password)

        return axios.get(`http://localhost:8080/hello-world/path-variable/${name}`
            // , 
            //     {
            //         headers : {
            //             authorization: basicAuthHeader
            //         }
            //     }
        );
    }

}

export default new HelloWorldService()
```
---
---

### /frontend/todo-app/src/App.js

```js
import React, { Component } from 'react';
//import FirstComponent from './components/learning-examples/FirstComponent'
//import SecondComponent from './components/learning-examples/SecondComponent'
//import ThirdComponent from './components/learning-examples/ThirdComponent'
//import Counter from './components/counter/Counter'
import TodoApp from './components/todo/TodoApp'
import './App.css';
import './bootstrap.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        {/*<Counter/>*/}
        <TodoApp />
      </div>
    );
  }
}

// class LearningComponents extends Component {
//   render() {
//     return (
//       <div className="LearningComponents">
//          My Hello World
//          <FirstComponent></FirstComponent>
//          <SecondComponent></SecondComponent>
//          <ThirdComponent></ThirdComponent>
//       </div>
//     );
//   }
// }

export default App;
```
---

### /frontend/todo-app/package.json

```json
{
  "name": "todo-app",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "axios": "^0.18.0",
    "formik": "^1.5.1",
    "moment": "^2.24.0",
    "react": "^16.8.4",
    "react-dom": "^16.8.4",
    "react-router-dom": "^4.3.1",
    "react-scripts": "2.1.8"
  },
  "scripts": {
    "start": "PORT=4200 react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ]
}
```
---

### Docker, Kubernetes, AWSm Azure and Cloud Courses

```
brew install kompose
kompose convert

kubectl delete all -l app=todo-web-application-h2

kubectl apply -f mysql-database-data-volume-persistentvolumeclaim.yaml,mysql-deployment.yaml,mysql-service.yaml
kubectl get svc
kubectl apply -f todo-web-application-deployment.yaml,todo-web-application-service.yaml
docker push in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
kubectl logs todo-web-application-b65cc44d9-7h9pr -f

kubectl apply -f mysql-service.yaml
kubectl get pv
kubectl get pvc
kubectl describe pod/mysql-5ccbbbdcd8-5zjqg 

kubectl create configmap todo-web-application-config --from-literal=RDS_DB_NAME=todos
kubectl get configmap todo-web-application-config
kubectl describe configmap/todo-web-application-config

kubectl edit configmap/todo-web-application-config
kubectl scale deployment todo-web-application --replicas=0
kubectl scale deployment todo-web-application --replicas=1

kubectl edit configmap/todo-web-application-config
kubectl apply -f todo-web-application-deployment.yaml 
kubectl edit configmap todo-web-application-config
kubectl scale deployment todo-web-application --replicas=0
kubectl scale deployment todo-web-application --replicas=1

kubectl create secret generic todo-web-application-secrets --from-literal=RDS_PASSWORD=dummytodos
kubectl get secret/todo-web-application-secrets
kubectl describe secret/todo-web-application-secrets
kubectl apply -f todo-web-application-deployment.yaml 

kubectl delete -f mysql-database-data-volume-persistentvolumeclaim.yaml,mysql-deployment.yaml,mysql-service.yaml,todo-web-application-deployment.yaml,todo-web-application-service.yaml

apiVersion: v1
data:
  RDS_DB_NAME: todos
  RDS_HOSTNAME: mysql
  RDS_PORT: "3306"
  RDS_USERNAME: todos-user
kind: ConfigMap
metadata:
  name: todo-web-application-config
  namespace: default

cd /in28Minutes/git/kubernetes-crash-course/04-currency-exchange-microservice-basic 
mvn clean install
docker push in28min/currency-exchange:0.0.1-RELEASE
kubectl apply -f deployment.yaml
curl 34.67.103.178:8000/currency-exchange/from/USD/to/INR

kubectl create configmap currency-conversion --from-literal=YOUR_PROPERTY=value --from-literal=YOUR_PROPERTY_2=value2

kubectl autoscale deployment currency-exchange --min=1 --max=3 --cpu-percent=10 
kubectl get events
kubectl get hpa
kubectl get hpa -o yaml
kubectl get hpa -o yaml > 01-hpa.yaml
kubectl get hpa currency-exchange -o yaml > 01-hpa.yaml

kubectl set image deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.4-SNAPSHOT
kubectl apply -f ingress.yaml
kubectl get ingress
kubectl describe gateway-ingress
kubectl describe gateway gateway-ingress
kubectl describe ingress gateway-ingress
kubectl apply -f rbac.yml
 
docker push in28min/currency-conversion:0.0.5-RELEASE

kubectl create configmap currency-conversion --from-literal=YOUR_PROPERTY=value --from-literal=YOUR_PROPERTY_2=value2

kubectl describe configmap/currency-conversion


kubectl label namespace default istio-injection=enabled

kubectl get svc --namespace istio-system
kubectl apply -f 01-helloworld-deployment.yaml 
kubectl apply -f 02-creating-http-gateway.yaml 
kubectl apply -f 03-creating-virtualservice-external.yaml 
kubectl get svc --namespace istio-system
kubectl get svc istio-ingressgateway --namespace istio-system
kubectl scale deployment hello-world-rest-api --replicas=4
kubectl delete all -l app=hello-world-rest-api
kubectl apply -f 04-helloworld-multiple-deployments.yaml 
kubectl apply -f 05-helloworld-mirroring.yaml 
kubectl apply -f 06-helloworld-canary.yaml 
watch -n 0.1 curl 35.223.25.220/hello-world

gcloud container clusters get-credentials in28minutes-cluster-istio --zone us-central1-a --project solid-course-258105
kubectl create namespace istio-system
curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.2.2 sh -
ls istio-1.2.2
ls istio-1.2.2/install/kubernetes/helm/istio-init/files/crd*yaml
cd istio-1.2.2
for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
helm template install/kubernetes/helm/istio --name istio --set global.mtls.enabled=false --set tracing.enabled=true --set kiali.enabled=true --set grafana.enabled=true --namespace istio-system > istio.yaml
kubectl apply -f istio.yaml
kubectl get pods --namespace istio-system
kubectl get services --namespace istio-system


docker push in28min/currency-exchange:3.0.0-RELEASE
kubectl apply -f deployment.yaml 
kubectl apply -f 11-istio-scripts-and-configuration/07-hw-virtualservice-all-services.yaml 
kubectl get secret -n istio-system kiali
kubectl create secret generic kiali -n istio-system --from-literal=username=admin --from-literal=passphrase=admin
kubectl get svc --namespace istio-system


gcloud container clusters get-credentials helm-cluster --zone us-central1-a --project solid-course-258105
helm init
kubectl get deploy,svc tiller-deploy -n kube-system
clear
unzip 12-helm.zip
ls helm-tiller.sh
chmod +x helm-tiller.sh

gcloud container clusters get-credentials helm-cluster --zone us-central1-a --project solid-course-258105
./helm-tiller.sh
cat helm-tiller.sh 
kubectl get deploy,svc tiller-deploy -n kube-system
helm install ./currency-exchange/ --name=currency-services
helm install ./currency-conversion/ --name=currency-services-1
helm install ./currency-conversion/ --name=currency-services-3 --debug --dry-run
helm history currency-services-1
helm upgrade currency-services-1 ./currency-conversion/
helm rollback currency-services-1 1
helm upgrade currency-services-1 ./currency-conversion/ --debug --dry-run
helm upgrade currency-services-1 ./currency-conversion/
helm history currency-services-1

cf --version
cf login
cf help -a
cf help login
cf login -a https://api.run.pivotal.io
cf target
cf help target
cf push hello-world-rest-api
cf push hello-world-rest-api -r hello-world-rest-api-001.cfapps.io
cf push hello-world-rest-api --random-route
cf logout
cf login -a https://api.run.pivotal.io
cf push hello-world-rest-api -p target/hello-world-rest-api.jar
cf apps
cf routes
cf map-route hello-world-rest-api-ranga-101 cfapps.io --hostname hello-world-rest-api
cf map-route hello-world-rest-api cfapps.io --hostname hello-world-rest-api-ranga-101
cf spaces
cf orgs
cf stop hello-world-rest-api
cf start hello-world-rest-api
cf restart hello-world-rest-api

cf create-app-manifest hello-world-rest-api

cf v3-droplets hello-world-rest-api
ls target/hello-world-rest-api.jar

docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7

docker container list
docker stop 9a8dfcfa01d4
docker rm 9a8dfcfa01d4

cf services
cf help create-service 
cf v3-delete todo-web-application-mysql


cf scale currency-exchange-service -i 2

cf install-plugin ~/Downloads/autoscaler-for-pcf-cliplugin-macosx64-binary-2.0.199

cf autoscaling-apps
cf autoscaling-events currency-exchange-service
cf routes
cf events currency-conversion-service
cf events currency-exchange-service
cf disable-autoscaling currency-exchange-service
cf set-env currency-conversion-service CURRENCY_EXCHANGE_URI http://currency-exchange-service-ranga-101.cfapps.io
cf env currency-conversion-service
cf help -a
cf unset-env currency-conversion-service CURRENCY_EXCHANGE_URI

cf create-user-provided-service spring-boot-route-service -r https://spring-boot-route-service-ranga-101.cfapps.io
cf routes
cf bind-route-service cfapps.io --hostname currency-exchange-service-ranga-101 spring-boot-route-service
cf bind-route-service cfapps.io --hostname currency-conversion-service-ranga-101 spring-boot-route-service
cf unbind-route-service cfapps.io --hostname currency-exchange-service-ranga-101 spring-boot-route-service
cf unbind-route-service cfapps.io --hostname currency-conversion-service-ranga-101 spring-boot-route-service
cf stop spring-boot-route-service

cd /in28Minutes/git/config-server 
git init
git add *
git status
git commit -m "first commit"
git remote add origin https://github.com/in28minutes/config-server.git
git push -u origin master


cf create-service p-config-server trial config-server -c config-server.json

cf update-service config-server -c  '{ "count":1, "git":{  "uri":"https://github.com/in28minutes/dev-config-server-test.git", "label":"master", "searchPaths":"currency-exchange-service" }}'

cf set-env currency-conversion-service hystrix.command.default.circuitBreaker.requestVolumeThreshold 2


cf set-health-check currency-conversion-service http --endpoint /manage/health
cf set-health-check currency-conversion-service http --endpoint /manage/health-error
cf set-health-check currency-conversion-service http --endpoint /manage/health

cf set-env currency-exchange-service spring.cloud.services.registrationMethod direct
cf network-policies
cf remove-network-policy currency-conversion-service --destination-app currency-exchange-service --protocol tcp --port 8080
cf network-policies
cf unset-env currency-exchange-service spring.cloud.services.registrationMethod

cf map-route hello-world-rest-api-green cfapps.io --hostname hello-world-rest-api-ranga-101
cf unmap-route hello-world-rest-api cfapps.io --hostname hello-world-rest-api-ranga-101

docker container exec unruffled_tereshkova ls /tmp
docker container cp target/hello-world-rest-api.jar 54cf414254e48d5f68c4d468b2dd4cbdd95d17f9e2074fdb9df7f64987697f2b:/tmp
docker container commit unruffled_tereshkova in28min/hello-world-rest-api:manual 
docker run -p 8080:8080 in28min/hello-world-rest-api:manual
docker container commit --change='CMD ["java","-jar","/tmp/hello-world-rest-api.jar"]' unruffled_tereshkova in28min:hello-world-rest-api:manual2
docker run -p 8080:8080 in28min/hello-world-rest-api:manual2
docker inspect in28min/hello-world-rest-api:dockerfile1
docker history in28min/hello-world-rest-api:dockerfile1

docker build -t in28min/hello-world-rest-api:dockerfile1 .
docker run -p 8080:8080 in28min/hello-world-rest-api:dockerfile1
docker history in28min/hello-world-rest-api:dockerfile1

docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1-SNAPSHOT

mvn docker:build
docker run -p 8080:8080 webservices/01-hello-world-rest-api

docker run -dit 51297c224d60
docker container exec 7714 ls /maven
docker run -p 8080:8080 01-hello-world-rest-api:latest

#/02-todo-web-application-h2/
docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT ping google.com
docker run -p 8080:8080 in28min/hello-world-rest-api:dockerfile1 param1 param2
docker run -p 8080:8080 in28min/todo-web-application-mysql:0.0.1-SNAPSHOT

docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping http://localhost:8080 

docker network ls
docker inspect bridge
docker container run -p 8080:8080 --link=mysql -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT

docker network create web-application-mysql-network
docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
docker container restart mysql
docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT

docker container prune


docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network --volume mysql-database-volume:/var/lib/mysql  mysql:5.7


#/04-spring-boot-react-full-stack-h2/restful-web-services/
docker tag 3f4765872126 in28min/rest-api-full-stack:2stagebuild
docker run -p 8080:8080 in28min/rest-api-full-stack:2stagebuild

npm install
npm start
npm run build

docker network create currency-network
docker run -p 8000:8000 --network=currency-network --name=currency-exchange-service in28min/currency-exchange-service:0.0.1-SNAPSHOT
docker run -p 8100:8100 --network=currency-network --name=currency-conversion-service --env CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 -d in28min/currency-conversion-service:0.0.1-SNAPSHOT

docker-compose up
docker-compose up -d
docker-compose scale currency-conversion-service=2
docker-compose logs
docker-compose logs -f

docker system prun
docker system prune -a

docker search mysql
docker images
docker tag in28min/todo-rest-api-h2:1.0.0.RELEASE latest
docker rmi latest:latest
docker pull mysql
docker image ls --format='{{json .}}'

docker container run -p 5000:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE
docker container pause 6478
docker container unpause 6478

docker run -p 5000:5000 in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
docker run -p 5000:5000 -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
docker run -p 5000:5000 -d --restart=always in28min/todo-rest-api-h2:0.0.1-SNAPSHOT

docker events
docker top c710
docker stats
docker run -m 512m --cpu-quota 50000
docker system df

docker container stop 1b1
docker container kill 9b8

docker-compose config
docker-compose images
docker-compose ps
docker-compose top
docker-compose pause
docker-compose unpause
docker-compose rm
docker-compose build
docker-compose events

Deleted Networks:
web-application-mysql-network
03-todo-web-application-mysql_todo-web-application-network
currency-network
05-microservices_currency-compose-network

# Azure Kubernetes Cluster Info
az login
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/<<azure_subscription_id>>"

# Create Public Key for SSH Access
ssh-keygen -m PEM -t rsa -b 4096 # PEM - Privacy Enhanced Mail - Certificate Format RSA- Encryption Algorithm

# ls /Users/rangakaranam/.ssh/id_rsa.pub

# Get Cluster Credentials
az aks get-credentials --name <<MyManagedCluster>> --resource-group <<MyResourceGroup>>


# AWS Kubernetes Cluster Info
aws configure
aws eks --region us-east-1 update-kubeconfig --name in28minutes-cluster 
kubectl get pods
kubectl get svc
kubectl get serviceaccounts
kubectl get serviceaccounts default -o yaml
kubectl get secret default-token-hqkvj -o yaml
kubectl cluster-info


cd /in28Minutes/git/devops-master-class/ansible 
ansible --version
ansible -m ping all
ansible all -a "whoami"
ansible all -a "uname"
ssh -vvv -i ~/aws/aws_keys/default-ec2.pem ec2-user@3.83.104.44
ls ~/aws/aws_keys/default-ec2.pem
chmod 400 /Users/rangaraokaranam/aws/aws_keys/default-ec2.pem
ansible all -a "uname"
ansible all -a "uname -a"
ansible all -a "pwd"
ansible all -a "python --version"
ansible dev -a "python --version"
ansible qa -a "python --version"
ansible first -a "python --version"
ansible groupofgroups -a "python --version"
ansible devsubset -a "python --version"
ansible --list-host all
ansible --list-host dev
ansible --list-host first
ansible --list-host \!first
ansible --list-host qa:dev
ansible-playbook playbooks/01-ping.yml
ansible-playbook playbooks/02-shell.yml 
ansible-playbook playbooks/03-variables.yml 
ansible-playbook playbooks/03-variables.yml -e variable1=CommandLineValue
ansible-playbook playbooks/04-ansible-facts.yml 
ansible-playbook playbooks/05-install-apache.yml 
ansible-playbook playbooks/06-playbooks.yml 
ansible-playbook playbooks/06-playbooks.yml --list-tasks
ansible-playbook playbooks/06-playbooks.yml --list-hosts
ansible-playbook playbooks/06-playbooks.yml --list-tags
ansible-playbook -l dev playbooks/01-ping.yml
ansible-playbook playbooks/07-conditionals-and-loops.yml 
ansible-inventory --list
ansible-inventory --graph
ansible-playbook playbooks/08-dynamic-inventory-ping.yml 
ansible-playbook playbooks/09-create-ec2.yml 
docker --version
docker run -p 5000:5000 in28min/hello-world-python:0.0.1.RELEASE
docker run -p 5000:5000 in28min/hello-world-java:0.0.1.RELEASE
docker run -p 5000:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker run -d -p 5000:5000 in28min/hello-world-nodejs:0.0.1.RELEASE
docker run -d -p 5001:5000 in28min/hello-world-python:0.0.1.RELEASE
docker logs 04e52ff9270f5810eefe1f77222852dc1461c22440d4ecd6228b5c38f09d838e
docker logs c2ba
docker images
docker container ls
docker container ls -a
docker container stop f708b7ee1a8b
docker run -d -p 5001:8080 in28min/hello-world-rest-api:0.0.1.RELEASE
docker pull mysql
docker search mysql
docker image history in28min/hello-world-java:0.0.1.RELEASE
docker image history 100229ba687e
docker image inspect 100229ba687e
docker image remove mysql
docker image remove in28min/hello-world-java:0.0.1.RELEASE
docker container rm 3e657ae9bd16
docker container ls -a
docker container pause 832
docker container unpause 832
docker container stop 832
docker container inspect ff521fa58db3
docker container prune
docker system
docker system df
docker system info
docker system prune -a
docker top 9009722eac4d
docker stats 9009722eac4d
docker container run -p 5000:5000 -d -m 512m in28min/hello-world-java:0.0.1.RELEASE
docker container run -p 5000:5000 -d -m 512m --cpu-quota=50000  in28min/hello-world-java:0.0.1.RELEASE
docker system events

docker container stats 4faca1ea914e3e4587d1d790948ec6cb8fa34f26e900c12632fd64d4722fd59a
docker stats 42f170966ce613d2a16d7404495af7b3295e01aeb9142e1fa1762bbdc581f502

cd /in28Minutes/git/devops-master-class/projects/hello-world/hello-world-python 
docker build -t in28min/hello-world-python:0.0.2.RELEASE . 
docker run -p 5000:5000 -d in28min/hello-world-python:0.0.2.RELEASE
docker history e66dc383f7a0
docker push in28min/hello-world-python:0.0.2.RELEASE

cd ../hello-world-nodejs/
docker build -t in28min/hello-world-nodejs:0.0.2.RELEASE . 
docker container run -d -p 5000:5000 in28min/hello-world-nodejs:0.0.2.RELEASE
docker push in28min/hello-world-nodejs:0.0.2.RELEASE

cd ../hello-world-java/
docker build -t in28min/hello-world-java:0.0.2.RELEASE . 
docker run -d -p 5000:5000 in28min/hello-world-java:0.0.2.RELEASE
docker push in28min/hello-world-java:0.0.2.RELEASE

docker run -d -p 5001:5000 in28min/hello-world-nodejs:0.0.3.RELEASE ping google.com


docker run -d -p 8000:8000 --name=currency-exchange in28min/currency-exchange:0.0.1-RELEASE
docker run -d -p 8100:8100 --name=currency-conversion in28min/currency-conversion:0.0.1-RELEASE

docker network ls
docker network inspect bridge

docker run -d -p 8100:8100 --env CURRENCY_EXCHANGE_SERVICE_HOST=http://currency-exchange --name=currency-conversion --link currency-exchange in28min/currency-conversion:0.0.1-RELEASE

docker network create currency-network
docker container stop currency-exchange
docker container stop currency-conversion
docker run -d -p 8000:8000 --name=currency-exchange --network=currency-network in28min/currency-exchange:0.0.1-RELEASE
docker run -d -p 8100:8100 --env CURRENCY_EXCHANGE_SERVICE_HOST=http://currency-exchange --name=currency-conversion --network=currency-network in28min/currency-conversion:0.0.1-RELEASE

docker-compose --version
cd ../../microservices/
docker-compose up
docker-compose up -d
docker container ls
docker network ls
docker network inspect microservices_currency-compose-network
docker-compose down
docker container ls -a
docker system prune -a
docker-compose config
docker-compose images
docker-compose ps
docker-compose top

docker build -t in28min/hello-world-java:0.0.1.RELEASE .
docker push in28min/hello-world-java:0.0.1.RELEASE

docker build -t in28min/hello-world-python:0.0.1.RELEASE .
docker push in28min/hello-world-python:0.0.1.RELEASE

docker build -t in28min/hello-world-nodejs:0.0.1.RELEASE .
docker push in28min/hello-world-nodejs:0.0.1.RELEASE

kubectl create deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.1.RELEASE
kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
kubectl scale deployment hello-world-rest-api --replicas=3
kubectl delete pod hello-world-rest-api-58ff5dd898-62l9d
kubectl autoscale deployment hello-world-rest-api --max=10 --cpu-percent=70
kubectl edit deployment hello-world-rest-api #minReadySeconds: 15
kubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.2.RELEASE

gcloud container clusters get-credentials in28minutes-cluster --zone us-central1-a --project solid-course-258105
kubectl create deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.1.RELEASE
kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
kubectl set image deployment hello-world-rest-api hello-world-rest-api=DUMMY_IMAGE:TEST
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.2.RELEASE
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get componentstatuses
kubectl get pods --all-namespaces

kubectl get events
kubectl get pods
kubectl get replicaset
kubectl get deployment
kubectl get service

kubectl get pods -o wide

kubectl explain pods
kubectl get pods -o wide

kubectl describe pod hello-world-rest-api-58ff5dd898-9trh2

kubectl get replicasets
kubectl get replicaset

kubectl scale deployment hello-world-rest-api --replicas=3
kubectl get pods
kubectl get replicaset
kubectl get events
kubectl get events --sort.by=.metadata.creationTimestamp

kubectl get rs
kubectl get rs -o wide
kubectl set image deployment hello-world-rest-api hello-world-rest-api=DUMMY_IMAGE:TEST
kubectl get rs -o wide
kubectl get pods
kubectl describe pod hello-world-rest-api-85995ddd5c-msjsm
kubectl get events --sort-by=.metadata.creationTimestamp

kubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.2.RELEASE
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get pods -o wide
kubectl delete pod hello-world-rest-api-67c79fd44f-n6c7l
kubectl get pods -o wide
kubectl delete pod hello-world-rest-api-67c79fd44f-8bhdt

kubectl get componentstatuses
kubectl get pods --all-namespaces

gcloud auth login
kubectl version
gcloud container clusters get-credentials in28minutes-cluster --zone us-central1-a --project solid-course-258105

kubectl rollout history deployment hello-world-rest-api
kubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.3.RELEASE --record=true
kubectl rollout undo deployment hello-world-rest-api --to-revision=1

kubectl logs hello-world-rest-api-58ff5dd898-6ctr2
kubectl logs -f hello-world-rest-api-58ff5dd898-6ctr2

kubectl get deployment hello-world-rest-api -o yaml
kubectl get deployment hello-world-rest-api -o yaml > deployment.yaml
kubectl get service hello-world-rest-api -o yaml > service.yaml
kubectl apply -f deployment.yaml
kubectl get all -o wide
kubectl delete all -l app=hello-world-rest-api

kubectl get svc --watch
kubectl diff -f deployment.yaml
kubectl delete deployment hello-world-rest-api
kubectl get all -o wide
kubectl delete replicaset.apps/hello-world-rest-api-797dd4b5dc

kubectl get pods --all-namespaces
kubectl get pods --all-namespaces -l app=hello-world-rest-api
kubectl get services --all-namespaces
kubectl get services --all-namespaces --sort-by=.spec.type
kubectl get services --all-namespaces --sort-by=.metadata.name
kubectl cluster-info
kubectl cluster-info dump
kubectl top node
kubectl top pod
kubectl get services
kubectl get svc
kubectl get ev
kubectl get rs
kubectl get ns
kubectl get nodes
kubectl get no
kubectl get pods
kubectl get po

kubectl delete all -l app=hello-world-rest-api
kubectl get all

kubectl apply -f deployment.yaml 
kubectl apply -f ../currency-conversion/deployment.yaml 

brew install terraform
terraform --version
terraform version
terraform init
export AWS_ACCESS_KEY_ID=*******
export AWS_SECRET_ACCESS_KEY=*********
terraform plan
terraform console
terraform apply -refresh=false
terraform plan -out iam.tfplan
terraform apply "iam.tfplan"
terraform apply -target=aws_iam_user.my_iam_user
terraform destroy
terraform validate
terraform fmt
terraform show
export TF_VAR_iam_user_name_prefix = FROM_ENV_VARIABLE_IAM_PREFIX
export TF_VAR_iam_user_name_prefix=FROM_ENV_VARIABLE_IAM_PREFIX
terraform plan -refresh=false -var="iam_user_name_prefix=VALUE_FROM_COMMAND_LINE"
terraform apply -target=aws_default_vpc.default
terraform apply -target=data.aws_subnet_ids.default_subnets
terraform apply -target=data.aws_ami_ids.aws_linux_2_latest_ids
terraform apply -target=data.aws_ami.aws_linux_2_latest
terraform workspace show
terraform workspace new prod-env
terraform workspace select default
terraform workspace list
terraform workspace select prod-env
```

## Enviroment Variables

SSM URN - `arn:aws:ssm:us-east-1:<account-id>:parameter/<name>`

- /dev/currency-conversion-service/CURRENCY_EXCHANGE_URI
- /dev/currency-exchange-service/RDS_DB_NAME  - exchange_db
- /dev/currency-exchange-service/RDS_HOSTNAME 
- /dev/currency-exchange-service/RDS_PASSWORD 
- /dev/currency-exchange-service/RDS_PORT     - 3306
- /dev/currency-exchange-service/RDS_USERNAME - exchange_db_user

## Setting up App Mesh

#### Virtual nodes 
- currency-exchange-service-vn - currency-exchange-service.in28minutes-dev.com
- currency-conversion-service-vn - currency-conversion-service.in28minutes-dev.com

#### Virtual services 
- currency-exchange-service.in28minutes-dev.com -> currency-exchange-service-vn
- currency-conversion-service.in28minutes-dev.com -> currency-conversion-service-vn

#### Backend Registration
- currency-conversion-service-vn -> currency-exchange-service.in28minutes-dev.com

#### Task Definition Updates
- aws-currency-conversion-service
- aws-currency-exchange-service-h2
- ```ENVOY_LOG_LEVEL-trace, ENABLE_ENVOY_XRAY_TRACING-1```

#### Service Updates
- aws-currency-conversion-service-appmesh
- aws-currency-exchange-service-appmesh

## Deploying Version 2 of Currency Exchange Service to ECS and App Mesh

#### App Mesh - New Virtual Node
currency-exchange-service-v2-vn - currency-exchange-service-v2.in28minutes-dev.com

#### ECS Fargate - Update Task Definition
aws-currency-exchange-service-h2
 - in28min/aws-currency-exchange-service-h2:1.0.1-RELEASE
 - Use New Virtual Node
 
#### ECS Fargate - Create New Service 
aws-currency-exchange-service-v2-appmesh
- Service Discovery - currency-exchange-service-v2

#### App Mesh - Create Virtual Router
currency-exchange-service-vr distributing traffic to
- currency-exchange-service-vn
- currency-exchange-service-v2-vn

#### App Mesh - Update Service to Use Virtual Router
currency-exchange-service.in28minutes-dev.com -> currency-exchange-service-vr


#### jq

```
sudo yum install jq
```

#### AWS CLI Hosted Zones

```
aws --version
aws configure
aws servicediscovery list-services
aws servicediscovery delete-service --id={id}
aws servicediscovery list-services

aws servicediscovery list-namespaces
aws servicediscovery delete-namespace --id={id}
aws servicediscovery list-namespaces

aws servicediscovery delete-service --id=srv-7q3fkztnbo6aa5kc
aws servicediscovery delete-service --id=srv-mdybugm4bh5u4ugx
aws servicediscovery delete-service --id=srv-7upzjx3mhfleyfoz
aws servicediscovery delete-namespace --id=ns-ctvtysasurklojm3
```
