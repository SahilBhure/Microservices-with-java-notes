

## Dependency Injection Deep Dive

---

## 2. What is Dependency Injection (Revisited)

Dependency Injection means:

> Providing required objects (dependencies) to a class instead of the class creating them.

Without DI:

```java
class Car {
    Engine engine = new Engine(); // tight coupling
}
```

With DI:

```java
class Car {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

---

## 3. How Spring Performs DI Internally

Steps:

1. Scans classes (`@ComponentScan`)
2. Creates Bean definitions
3. Resolves dependencies
4. Injects them using reflection

Spring uses:

* Reflection API
* BeanFactory / ApplicationContext
* Dependency resolution algorithms

---

## 4. Constructor Injection (Deep Dive)

### Why it is Best Practice

* Ensures immutability
* Makes dependencies mandatory
* Easier unit testing
* Prevents null values

Example:

```java
@Component
public class Car {

    private final Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

No need for `@Autowired` (Spring 4.3+)

---

## 5. Setter Injection (When to Use)

Used when:

* Dependency is optional
* You want to change dependency later

```java
@Component
public class Car {

    private Engine engine;

    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}
```

---

## 6. Field Injection (Why NOT to Use)

```java
@Autowired
private Engine engine;
```

Problems:

* Hard to test (no constructor)
* Breaks encapsulation
* Cannot be immutable

Use only for:

* Quick prototypes
* Not production code

---

## 7. Circular Dependencies (Very Important)

### Problem Example:

```java
@Component
class A {
    private B b;

    public A(B b) { this.b = b; }
}

@Component
class B {
    private A a;

    public B(A a) { this.a = a; }
}
```

This causes:

> BeanCurrentlyInCreationException

---

### Solutions:

1. Use `@Lazy`

```java
public A(@Lazy B b) { this.b = b; }
```

2. Switch to Setter Injection

3. Redesign architecture (Best solution)

---

## 8. @Autowired Deep Behavior

Spring resolves dependencies by:

1. Type
2. Qualifier (if multiple beans)
3. Primary (fallback)

---

## 9. Multiple Implementations Problem

Example:

```java
interface Engine {}
```

```java
@Component
class PetrolEngine implements Engine {}
```

```java
@Component
class DieselEngine implements Engine {}
```

Error:

> NoUniqueBeanDefinitionException

---

### Solution 1: @Qualifier

```java
@Autowired
@Qualifier("dieselEngine")
private Engine engine;
```

---

### Solution 2: @Primary

```java
@Primary
@Component
class PetrolEngine implements Engine {}
```

---

## 10. Injecting Collections

Spring can inject multiple beans:

```java
@Autowired
private List<Engine> engines;
```

Spring injects:

* All Engine implementations

---

## 11. Optional Dependencies

```java
@Autowired(required = false)
private Engine engine;
```

OR better:

```java
private Optional<Engine> engine;
```

---

## 12. Lazy Injection

```java
@Autowired
@Lazy
private Engine engine;
```

* Bean created only when used
* Useful for performance & circular dependencies

---

## 13. Injection with @Value (External Config)

```java
@Value("${engine.type}")
private String engineType;
```

Used for:

* Config values
* Environment variables

---

## 14. Real-World Pattern (Important)

### Service Layer Injection

```java
@Service
public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

This pattern is used in:

* Microservices
* Enterprise apps
* REST APIs

---

## 15. Common Mistakes

* Using field injection everywhere
* Ignoring constructor injection
* Not handling multiple beans
* Creating circular dependencies

---

## 16. Best Practices

* Always prefer constructor injection
* Keep dependencies minimal
* Avoid circular references
* Use interfaces for flexibility
* Use `@Qualifier` properly

---

End of Part 3
