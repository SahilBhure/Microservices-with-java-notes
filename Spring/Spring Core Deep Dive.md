

## Spring Core Deep Dive (IoC Container & Beans)

---

## 2. What is a Bean?

A **Bean** is simply:

> An object that is managed by the Spring container

Example:

```java
public class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}
```

When Spring manages it → it becomes a **Spring Bean**

---

## 3. What is IoC Container?

The **IoC Container** is the core of Spring.

Responsibilities:

* Create objects (Beans)
* Inject dependencies
* Manage lifecycle
* Configure application

---

## 4. Types of IoC Containers

### 4.1 BeanFactory (Basic)

* Lazy initialization
* Lightweight
* Rarely used directly

### 4.2 ApplicationContext (Advanced)

Most commonly used container.

Features:

* Eager initialization (by default)
* Event propagation
* Internationalization (i18n)
* AOP support

Example:

```java
ApplicationContext context =
    new AnnotationConfigApplicationContext(AppConfig.class);
```

---

## 5. How Spring Creates Beans

Spring reads configuration metadata from:

* XML
* Java Config
* Annotations

Then:

1. Scans classes
2. Creates objects
3. Stores them in container
4. Injects dependencies

---

## 6. Ways to Define Beans

### 6.1 Using XML (Old Way)

```xml
<bean id="engine" class="com.example.Engine"/>
```

---

### 6.2 Using Java Configuration

```java
@Configuration
public class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine();
    }
}
```

---

### 6.3 Using Annotations (Most Used)

```java
@Component
public class Engine {
}
```

Other stereotype annotations:

* `@Component`
* `@Service`
* `@Repository`
* `@Controller`

---

## 7. Component Scanning

Spring automatically detects beans using:

```java
@ComponentScan("com.example")
```

It scans the package and registers all annotated classes as beans.

---

## 8. Bean Scope

Defines **lifecycle and visibility** of a bean.

### Types:

| Scope               | Description                |
| ------------------- | -------------------------- |
| Singleton (default) | One instance per container |
| Prototype           | New instance every time    |
| Request             | One per HTTP request       |
| Session             | One per user session       |

Example:

```java
@Scope("prototype")
@Component
public class Engine {
}
```

---

## 9. Bean Lifecycle (Important for Interviews)

Steps:

1. Bean Instantiation
2. Dependency Injection
3. `BeanNameAware`
4. `BeanFactoryAware`
5. Pre-initialization (`@PostConstruct`)
6. Initialization (`InitializingBean`)
7. Bean is ready to use
8. Destruction (`@PreDestroy`)

---

## 10. Dependency Injection Types

### 10.1 Constructor Injection (Recommended)

```java
@Component
public class Car {

    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

---

### 10.2 Setter Injection

```java
@Autowired
public void setEngine(Engine engine) {
    this.engine = engine;
}
```

---

### 10.3 Field Injection (Not Recommended)

```java
@Autowired
private Engine engine;
```

Reason:

* Hard to test
* Breaks encapsulation

---

## 11. Autowiring Modes

Spring resolves dependencies automatically.

Modes:

* byType (most common)
* byName
* constructor

Example:

```java
@Autowired
private Engine engine;
```

---

## 12. Qualifier (Handling Multiple Beans)

```java
@Component
@Qualifier("dieselEngine")
public class DieselEngine implements Engine {}
```

```java
@Autowired
@Qualifier("dieselEngine")
private Engine engine;
```

---

## 13. Primary Annotation

```java
@Primary
@Component
public class PetrolEngine implements Engine {}
```

Spring will use this by default if multiple beans exist.

---

## 14. Lazy Initialization

```java
@Lazy
@Component
public class Engine {}
```

Bean is created only when needed.

---

## 15. Practical Flow (Important)

1. Application starts
2. Spring container initializes
3. Beans are created
4. Dependencies injected
5. Application runs

---

## 16. Common Mistakes

* Using field injection everywhere
* Not understanding bean scope
* Circular dependencies
* Overusing `@ComponentScan`

---
