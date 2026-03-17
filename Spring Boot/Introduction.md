## Spring Boot Deep Dive (Core to Advanced)

---

## 1. What is Spring Boot?

Spring Boot is an extension of Spring that:

> **Eliminates boilerplate configuration and helps you build production-ready applications quickly**

It simplifies:

* Project setup
* Configuration
* Deployment

---

## 2. Why Spring Boot Was Introduced

Problems in traditional Spring:

* Heavy XML/Java configuration
* Manual dependency management
* No embedded server
* Slow setup

Spring Boot solves this by:

* Auto-configuration
* Starter dependencies
* Embedded servers
* Opinionated defaults

---

## 3. Core Features of Spring Boot

### 3.1 Auto-Configuration

Automatically configures beans based on:

* Classpath dependencies
* Existing beans
* Properties

---

### 3.2 Starter Dependencies

Example:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

This includes:

* Spring MVC
* Jackson
* Tomcat

---

### 3.3 Embedded Server

No need to deploy WAR:

* Tomcat (default)
* Jetty
* Undertow

Run app directly:

```bash
mvn spring-boot:run
```

---

### 3.4 Production-Ready Features

* Actuator (monitoring)
* Metrics
* Health checks
* External configuration

---

## 4. Spring Boot Architecture

```text
Main Class → Auto Configuration → Beans → Application
```

---

## 5. @SpringBootApplication (Very Important)

```java
@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```

This annotation combines:

* @Configuration
* @EnableAutoConfiguration
* @ComponentScan

---

## 6. Auto-Configuration Deep Dive

Spring Boot auto-config works using:

### 6.1 Conditional Annotations

* @ConditionalOnClass
* @ConditionalOnMissingBean
* @ConditionalOnProperty

Example:

```java
@ConditionalOnClass(DataSource.class)
```

---

### 6.2 spring.factories (Internal Mechanism)

Spring Boot scans:

```text
META-INF/spring.factories
```

This file contains:

* Auto-configuration classes

---

### 6.3 Flow

1. App starts
2. Spring Boot checks classpath
3. Matches conditions
4. Registers beans automatically

---

## 7. Configuration in Spring Boot

### 7.1 application.properties

```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/db
```

---

### 7.2 application.yml

```yaml
server:
  port: 8081

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/db
```

---

### 7.3 Priority Order

1. Command line args
2. Environment variables
3. application.properties
4. Default values

---

## 8. @ConfigurationProperties (Advanced)

```java
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
}
```

Better than @Value because:

* Type-safe
* Cleaner
* Supports nested objects

---

## 9. Profiles in Spring Boot

```properties
spring.profiles.active=dev
```

Files:

* application-dev.properties
* application-prod.properties

---

## 10. Logging in Spring Boot

Default:

* Logback

Config:

```properties
logging.level.root=INFO
logging.level.com.example=DEBUG
```

---

## 11. Spring Boot Actuator (Production Feature)

Add dependency:

```xml
spring-boot-starter-actuator
```

Endpoints:

* /actuator/health
* /actuator/info
* /actuator/metrics

---

## 12. Exception Handling (Advanced)

Global handler:

```java
@ControllerAdvice
public class GlobalHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handle(Exception ex) {
        return ResponseEntity.badRequest().body(ex.getMessage());
    }
}
```

---

## 13. Custom Error Handling

Override:

```properties
server.error.include-message=always
```

Or create custom error response class.

---

## 14. Bean Management in Spring Boot

Still uses:

* IoC Container
* Beans
* DI

But:

> Configuration is mostly automatic

---

## 15. Running Spring Boot Applications

### Using Maven

```bash
mvn spring-boot:run
```

### Using JAR

```bash
java -jar app.jar
```

---

## 16. Packaging

Spring Boot creates:

* **Fat JAR (Uber JAR)**

Includes:

* All dependencies
* Embedded server

---

## 17. DevTools (Development Productivity)

Dependency:

```xml
spring-boot-devtools
```

Features:

* Auto restart
* Live reload

---

## 18. Spring Boot vs Spring Framework

| Feature | Spring   | Spring Boot |
| ------- | -------- | ----------- |
| Setup   | Manual   | Auto        |
| Config  | Heavy    | Minimal     |
| Server  | External | Embedded    |
| Speed   | Slow     | Fast        |

---

## 19. Real-World Flow

```text
Request → Controller → Service → Repository → DB
```

Spring Boot handles:

* Configuration
* Server
* Wiring

---

## 20. Common Mistakes

* Overriding auto-config unnecessarily
* Ignoring profiles
* Poor property management
* Not understanding auto-config

---

## 21. Best Practices

* Use starters
* Keep configs minimal
* Use profiles properly
* Externalize configs
* Use @ConfigurationProperties

---

## 22. Advanced Concepts You Should Know

* Custom auto-configuration
* Conditional beans
* External config sources
* Boot lifecycle

---

## 23. Spring Boot Startup Flow (Important)

1. main() runs
2. SpringApplication starts
3. Environment prepared
4. Context created
5. Auto-config applied
6. Beans initialized
7. App ready

---

## 24. Practice Task

1. Create Spring Boot app
2. Add:

   * REST API
   * Database config
3. Use:

   * application.properties
   * Profiles
4. Enable actuator
5. Run and test endpoints

---

