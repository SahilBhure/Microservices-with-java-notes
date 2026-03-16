

# Step 1: Bootstrap the Project with Spring Initializr

1. Open your browser and go to
   https://start.spring.io/

2. Configure the project with the following settings:

**Project**

* Project: Maven
* Language: Java
* Spring Boot: Latest Stable Version

**Project Metadata**

* Group: `com.example`
* Artifact: `hello-service`
* Name: `hello-service`
* Package name: `com.example.helloservice`
* Packaging: Jar
* Java: 17 (or your installed version)

**Dependencies**
Add the following dependency:

* **Spring Web**

3. Click **Generate**.

4. A `.zip` file will download.

5. Extract the project.

6. Open the project in your IDE:

* IntelliJ IDEA
* VS Code
* Eclipse

---

# Step 2: Understand the Project Structure

After opening the project, you will see a structure like this:

```
hello-service
│
├── src
│   ├── main
│   │   ├── java/com/example/helloservice
│   │   │   └── HelloServiceApplication.java
│   │   │
│   │   └── resources
│   │       └── application.properties
│
├── pom.xml
```

Important files:

| File                           | Purpose                      |
| ------------------------------ | ---------------------------- |
| `HelloServiceApplication.java` | Main Spring Boot entry point |
| `pom.xml`                      | Maven dependencies           |
| `application.properties`       | Configuration file           |

---

# Step 3: Create the Controller

Spring Boot APIs are created using **Controllers**.

Navigate to:

```
src/main/java/com/example/helloservice/
```

Create a new file:

```
HelloController.java
```

Add the following code:

```java
package com.example.helloservice;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello World! Your Microservice is running.";
    }
}
```

---

# Understanding the Code

### `@RestController`

```java
@RestController
```

This tells Spring Boot that this class will handle **REST API requests**.

---

### `@GetMapping`

```java
@GetMapping("/hello")
```

This maps HTTP **GET requests** to the `/hello` endpoint.

Example request:

```
GET /hello
```

---

### Method Response

```java
public String sayHello()
```

This method returns a simple **String response** which becomes the HTTP response body.

Response:

```
Hello World! Your Microservice is running.
```

---

# Step 4: Run the Microservice

There are two ways to run the application.

---

# Option 1: Run Using IDE

Locate this file:

```
HelloServiceApplication.java
```

Example:

```java
package com.example.helloservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HelloServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(HelloServiceApplication.class, args);
    }

}
```

Run the application:

1. Right-click the file
2. Click **Run HelloServiceApplication**

The application will start.

You should see logs like this in the console:

```
Tomcat started on port(s): 8080
Started HelloServiceApplication
```

---

# Option 2: Run Using Terminal (Maven)

Open a terminal in the **project root folder**.

Run:

### Mac / Linux

```bash
./mvnw spring-boot:run
```

### Windows

```bash
mvnw spring-boot:run
```

Spring Boot will start the embedded **Tomcat server**.

---

# Step 5: Access the API

Once the application is running, open your browser and go to:

```
http://localhost:8080/hello
```

You will see:

```
Hello World! Your Microservice is running.
```

---

# Step 6: Test Using Curl (Optional)

You can also test your API using the terminal.

```bash
curl http://localhost:8080/hello
```

Response:

```
Hello World! Your Microservice is running.
```

---

# Step 7: Test Using Postman (Optional)

1. Open **Postman**
2. Create a new request
3. Method: `GET`
4. URL:

```
http://localhost:8080/hello
```

Click **Send**

Response:

```
Hello World! Your Microservice is running.
```

---

# Step 8: Build the Application JAR

You can package the application as a **JAR file**.

Run:

```bash
./mvnw clean package
```

This creates:

```
target/hello-service-0.0.1-SNAPSHOT.jar
```

---

# Step 9: Run the JAR File

Run the microservice with:

```bash
java -jar target/hello-service-0.0.1-SNAPSHOT.jar
```

Your microservice will start on:

```
http://localhost:8080
```
---
