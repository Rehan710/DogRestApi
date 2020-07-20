# DogRestApi
REST API that returns a list of dogs from an embedded H2 in memory database.

To make it simple, I've divided project in 2 parts.


PART1: Creating REST API.
PART2: Adding security to API 


Part 1: creating REST API.

Set Up
Step 1: Use Spring Initializr to bootstrap a simple project.
Add the H2 Database, Spring Web Starter, and the Spring Data JPA dependencies before generating the project.

Step 2: Set-up the H2 in-memory database.
Enable the console, add a path for the console, and create a url for the datasource using H2.

Within application.properties (found within /src/main/resources/), you could add the following code:

spring.h2.console.enabled=true
spring.h2.console.path=/h2

spring.datasource.url=jdbc:h2:mem:dogdata

---Build a Dog REST API

Step 1: Create an entity called Dog.
The dog should have three attributes:
Name
Breed
Origin

Step 2: Create a web controller using @RestController.

Step 3: Create a repository that extends CrudRepository.
This repository is for creating, reading, updating, and deleting Dog objects.


Step 4: Update the web controller.
The updated controller should handle requests for retrieving:
a list of Dog breeds
a list of Dog breeds by Id
a list of Dog names


Step 5: Make sure errors are handled appropriately.
If an id is requested that doesn’t exist, appropriately handle the error


Step 6: Create a data.sql file.
The file should create sample dog data in the database.


Step 7: Check that you are able to access your API.
If everything is implemented correctly, once you run your code, you should be able to visit localhost:8080/h2 to first reach the H2 console. 

After clicking "Connect", you should go to the next H2 page, where you should be able to "Run" the query and see everything you added to data.sql.


PART: 2

The Security case study retrieves a list of locations from a database in a secure fashion.

Step 1: Add the necessary dependencies for Spring Security.


Given your code for the REST API from before, you just need to add the following two dependencies to the Maven POM file:

<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-test</artifactId>
</dependency>


Step 2: Create the necessary security configuration class.
the class should extend WebSecurityConfigurerAdapter to secure your API with Basic Authentication.


First, add a config package to your Dog REST API code, and then add a SpringSecurityConfig class within it that extends WebSecurityConfigurerAdapter from Spring Security.

Step 3: Test that your API is now secured.
It should use basic authentication
The API should still operate appropriately for an authenticated user

You can test this out in multiple ways. First, I tried to access localhost:8080/dogs in the browser, and got a "Sign in" window. If I click cancel, I get a 401 error - Unauthorized. If I enter in my basic authentication information, I can access the page.



I can also test this in Postman instead, where I change the "Authorization" tab to use "Basic Auth", make sure I am using a GET request, and then first attempt without a username and password. I will again get a status code of 401 meaning I am unauthorized. If I add the correct username and password, I can access the API.

