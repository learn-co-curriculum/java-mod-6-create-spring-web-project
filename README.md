# Create Spring Web Project

## Learning Goals

- Initialize Spring Web project.
- Set up database, model, and repository.

## Introduction

We will be using Spring Boot to create an api that can accept and send JSON
response.

Spring Boot provides default configurations that set up the web server which
handles the communication layer. We can focus on the business logic and let
Spring Boot handle most of the boilerplate configurations.

Spring Web provides bundles several dependencies that make it easy to build a
web application. For example, we don’t have to add configuration for converting
object models to and from JSON. Instead, we can use annotations to automatically
indicate what kind of data we want to return to the client.

We will be using the following model:

![Member database model diagram](https://curriculum-content.s3.amazonaws.com/java-spring-1/db-diagram-member.png)

And this is what the API endpoints will look like:

| Method | URI                   | Description                                                                  |
| ------ | --------------------- | ---------------------------------------------------------------------------- |
| GET    | /api/members          | Retrieves all members from the database.                                     |
| GET    | /api/members/memberId | Retrieves the member with the ID of “memberId”.                              |
| POST   | /api/members          | Creates a new member with the data submitted by the client (as JSON).        |
| PUT    | /api/members/memberId | Replaces the member with the ID “memberID” with data provided by the client. |
| DELETE | /api/members/memberId | Deletes the member with the ID “memberId”.                                   |

## Initialize the Project

Go to [https://start.spring.io/](https://start.spring.io/) and generate a
project with the settings shown in the image below. Open the project in
IntelliJ.

![Spring Initializr settings for Spring Web project](https://curriculum-content.s3.amazonaws.com/java-spring-1/spring-initializr-spring-web.png)

## Configure the Database

We will be using a similar configuration to the one we used for our Spring Data
project. Open up the `application.properties` file and add the following:

```java
# connect to database
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.username=sa
spring.datasource.password=
spring.datasource.driver-class-name=org.h2.Driver

# configure database
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.H2Dialect
```

## Project Structure

Since we will be using the MVC pattern, we need to create package to hold the
various units. Create the following packages in the `org.example.springwebdemo`
package:

- `controller`
- `model`
- `repository`
- `service` (discussed in later lessons)

Your project structure should look like this:

```
├── HELP.md
├── mvnw
├── mvnw.cmd
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── org
    │   │       └── example
    │   │           └── springwebdemo
    │   │               ├── SpringWebDemoApplication.java
    │   │               ├── controller
    │   │               │   └── MemberController.java
    │   │               ├── model
    │   │               │   └── Member.java
    │   │               ├── repository
    │   │               │   └── MemberRepository.java
    │   │               └── service
    │   │                   └── MemberService.java
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

## Model and Repository Setup

We have learned in the Spring Data section how to define models and set up
repositories in our applications. We will be following a similar procedure for
this project.

Create a `Member` class in the `model` package and add the following code:

```java
package org.example.springwebdemo.model;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Member {
    @Id
    @GeneratedValue
    private int id;

    private String name;

    private String email;

    public int getId() {
        return id;
    }

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
}
```

Now create a `MemberRepository` class in the `repository` package and add the
following code:

```java
package org.example.springwebdemo.repository;

import org.example.springwebdemo.model.Member;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface MemberRepository extends JpaRepository<Member, Integer> {

}
```

Notice that we are extending the [`JpaRepository`
interface](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html#getReferenceById-ID-)
instead of
[`CrudRepository`](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html)`.
The

`JpaRepository` interface a few JPA specific extensions that makes it more
convenient. For example, its `findAll` method returns a `List` instead of an
`Iterable` which makes it easier to serialize the data.

## Conclusion

We have set up the basic structure of our application. In the next few lessons,
we will add the service and controller classes to our application.
