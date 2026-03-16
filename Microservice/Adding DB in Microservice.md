# Adding a Database to the Microservice

In the previous step, the microservice stored data in memory using a simple list.
In this step, we will connect the microservice to a real database and persist data.

We will use:

* Spring Data JPA
* PostgreSQL
* Entity mapping
* Repository interface

This allows the service to store and retrieve data from a database instead of temporary memory storage.

---

# What You Will Learn

In this step you will learn:

* How to connect Spring Boot to a database
* How to configure PostgreSQL
* How to create JPA entities
* How to use Spring Data JPA repositories
* How to perform CRUD operations with a database

---

# Add Dependencies

Open the `pom.xml` file and add the following dependencies if they are not already present.

```xml
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
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>

</dependencies>
```

The dependencies provide:

| Dependency                   | Purpose                    |
| ---------------------------- | -------------------------- |
| spring-boot-starter-data-jpa | ORM and repository support |
| postgresql                   | PostgreSQL database driver |

---

# Configure Database Connection

Open the file:

```
src/main/resources/application.properties
```

Add the following configuration.

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/microservice_db
spring.datasource.username=postgres
spring.datasource.password=postgres

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

Explanation:

| Property            | Description                          |
| ------------------- | ------------------------------------ |
| datasource.url      | Database connection URL              |
| datasource.username | Database username                    |
| datasource.password | Database password                    |
| ddl-auto=update     | Automatically creates/updates tables |
| show-sql            | Displays SQL queries in logs         |

---

# Create the Database

Before running the application, create the database.

Example using PostgreSQL:

```sql
CREATE DATABASE microservice_db;
```

---

# Update the Entity

Update the existing `User` class to make it a JPA entity.

File:

```
src/main/java/com/example/helloservice/model/User.java
```

```java
package com.example.helloservice.model;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;

@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;

    public User() {}

    public User(Long id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
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

Annotations used:

| Annotation        | Purpose                              |
| ----------------- | ------------------------------------ |
| `@Entity`         | Marks the class as a database entity |
| `@Id`             | Primary key                          |
| `@GeneratedValue` | Auto-generates the ID                |

---

# Update the Repository

Spring Data JPA allows us to remove manual repository code.

Update the repository file.

File:

```
src/main/java/com/example/helloservice/repository/UserRepository.java
```

```java
package com.example.helloservice.repository;

import com.example.helloservice.model.User;
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

This provides built-in methods such as:

* `findAll()`
* `findById()`
* `save()`
* `deleteById()`

No implementation is required.

---

# Update the Service Layer

File:

```
src/main/java/com/example/helloservice/service/UserService.java
```

```java
package com.example.helloservice.service;

import com.example.helloservice.model.User;
import com.example.helloservice.repository.UserRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User createUser(User user) {
        return userRepository.save(user);
    }
}
```

---

# Update the Controller

File:

```
src/main/java/com/example/helloservice/controller/UserController.java
```

```java
package com.example.helloservice.controller;

import com.example.helloservice.model.User;
import com.example.helloservice.service.UserService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public List<User> getUsers() {
        return userService.getAllUsers();
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
}
```

---

# Run the Application

Start the application the same way as before.

Run the main class:

```
HelloServiceApplication.java
```

Or from terminal:

```
./mvnw spring-boot:run
```

---

# Test the API

Create a user.

POST request:

```
http://localhost:8080/users
```

Body:

```json
{
  "name": "Sahil",
  "email": "sahil@example.com"
}
```

Response:

```json
{
  "id": 1,
  "name": "Sahil",
  "email": "sahil@example.com"
}
```

---

Retrieve users.

GET request:

```
http://localhost:8080/users
```

Response:

```json
[
  {
    "id": 1,
    "name": "Sahil",
    "email": "sahil@example.com"
  }
]
```

---

# Result

The microservice now stores data in a real database using Spring Data JPA.

The application now includes:

* Controller layer
* Service laye
