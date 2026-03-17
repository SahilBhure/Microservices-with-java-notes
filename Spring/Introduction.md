# Spring Framework – In-Depth Learning Notes (Part 1: Introduction)

## 1. What is Spring Framework?

The **Spring Framework** is a powerful, lightweight framework used to build **Java applications**, especially **enterprise-level applications**.

It provides:

* Infrastructure support
* Dependency management
* Simplified development
* Integration with various technologies

---

## 2. Why Spring?

Before Spring, Java enterprise development using **Java EE (J2EE)** was:

* Complex
* Heavyweight
* Difficult to test
* Tightly coupled

Spring solves these problems by:

* Promoting **loose coupling**
* Making code **testable**
* Reducing boilerplate code
* Providing **modular architecture**

---

## 3. Core Concepts of Spring

### 3.1 Dependency Injection (DI)

Dependency Injection is the **heart of Spring**.

Instead of creating objects manually:

```java
Car car = new Car(new Engine());
```

Spring does it for you:

```java
@Autowired
Engine engine;
```

Benefits:

* Loose coupling
* Easy testing
* Better maintainability

---

### 3.2 Inversion of Control (IoC)

IoC means:

> The control of object creation is transferred from the developer to the Spring container.

Spring container:

* Creates objects (Beans)
* Manages lifecycle
* Injects dependencies

---

### 3.3 Spring Container

The container is responsible for:

* Creating beans
* Injecting dependencies
* Managing lifecycle

Types:

* BeanFactory (basic)
* ApplicationContext (advanced, commonly used)

---

## 4. Spring Architecture Overview

Spring is modular. Major modules include:

### 4.1 Core Container

* Core
* Beans
* Context
* Expression Language (SpEL)

### 4.2 Data Access

* JDBC
* ORM
* Transactions

### 4.3 Web

* Spring MVC
* REST APIs

### 4.4 AOP (Aspect-Oriented Programming)

* Logging
* Security
* Transactions

---

## 5. Key Advantages

* Lightweight and flexible
* Easy integration (Hibernate, JPA, etc.)
* Supports microservices (with Spring Boot)
* Strong community support
* Production-ready ecosystem

---

## 6. Spring vs Spring Boot

| Feature       | Spring Framework     | Spring Boot       |
| ------------- | -------------------- | ----------------- |
| Configuration | Manual               | Auto-configured   |
| Setup         | Complex              | Quick             |
| Use Case      | Large, flexible apps | Rapid development |

---

## 7. Real-World Use Cases

* Web applications (REST APIs)
* Microservices
* Enterprise systems
* Banking & fintech apps

---

