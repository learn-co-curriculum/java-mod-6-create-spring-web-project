# Create Spring Web Project

## Learning Goals

- Create a Spring Boot Project with the Spring Web dependency.
- Consider some model requirements.
- Review the project structure.

## Create the Spring Boot Project

In a similar fashion as before, let's create a Spring Boot project and add the
Spring Web dependency to create a Spring MVC!

1. Go to [https://start.spring.io/](https://start.spring.io/).
2. Select the project properties.
   1. Select "Maven Project", as we will use Maven as the build tool.
   2. Select "Java" as the language.
   3. Select the most recent version of Spring Boot 2. (Make sure it does not have
      "SNAPSHOT" listed after it.)
   4. Change the "Artifact" metadata field to "spring-web-demo". (This will update
      the "Name" and "Package name" metadata fields too).
   5. Change the "Description" metadata field to "Demo project for Spring Web".
   6. Select the appropriate Java JDK version.
3. Add dependencies.
   1. Let's add the Spring Web dependency to create a Spring web application.
   2. Click "ADD DEPENDENCIES".
   3. Search for "spring web".
   4. Select "Spring Web" from the list.
4. Click on the "Generate" button on the bottom. This will download a zip file
   containing the Spring Boot Project.
5. Unzip the archive and open it in IntelliJ or a preferred code editor.

![Spring Initializr settings for Spring Web project](https://curriculum-content.s3.amazonaws.com/spring-mod-1/spring-web-project/spring-initializr-web.png)

Spring Boot provides default configurations that set up the web server which
handles the communication layer. We can focus on the business logic and let
Spring Boot handle most of the boilerplate configurations.

Spring Web provides bundles several dependencies that make it easy to build a
web application. We'll see how helpful this is to us in a couple of lessons!
In the meantime, we can see that our Spring Web dependency has been added by
looking in the pom.xml file under `<dependencies>`:

```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
```

## The Model Requirements

Remember from the previous lesson that the model is the data and its relationships
we would like to represent in a web application. So let's pick something to model!

Since this is our first API we are creating, let's start simple. Consider a
cafeteria. We will create the following options:

- Greet the customer.
- Tell the customer the daily lunch special.
- Thank the customer for coming into our cafeteria.

Great! Now let's set this up in our project!

## Project Structure

Since we will be using the MVC pattern, we need to create package to hold the
various units. Create the following packages in the `com.example.springwebdemo`
package:

- `controller`
- `service`

Your project structure should look like this:

```text
├── HELP.md
├── mvnw
├── mvnw.cmd
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           └── springwebdemo
    │   │               ├── SpringWebDemoApplication.java
    │   │               ├── controller
    │   │               │   └── LunchController.java
    │   │               └── service
    │   │                   └── LunchService.java
    │   └── resources
    │       ├── application.properties
    │       ├── static
    │       └── templates
    └── test
        └── java
            └── org
                └── example
                    └── springwebdemo
                        └── SpringWebDemoApplicationTests.java
```

## Conclusion

Congratulations! We have set up the basic structure of our application. Now we
created two packages with two classes: a controller and a service. But what are
those classes? Let's find out in the next lessons!

## References

- [Spring Web MVC Documentation](https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/mvc.html)
- [Spring Initializr](https://start.spring.io/)
