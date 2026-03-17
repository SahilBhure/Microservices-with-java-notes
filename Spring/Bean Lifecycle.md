
## Bean Lifecycle Deep Dive

---

## 2. Complete Bean Lifecycle Flow

1. Container starts
2. Bean instantiated
3. Dependencies injected
4. Aware interfaces called
5. Pre-initialization
6. Initialization
7. Bean ready for use
8. Destruction

---

## 3. Step-by-Step Lifecycle

### 3.1 Bean Instantiation

Spring creates the object:

```java id="3o9t2k"
Engine engine = new Engine();
```

---

### 3.2 Dependency Injection

Dependencies are injected:

```java id="9m6b3r"
new Car(engine);
```

---

### 3.3 Aware Interfaces

Spring provides context information via:

* `BeanNameAware`
* `BeanFactoryAware`
* `ApplicationContextAware`

Example:

```java id="k6p4sj"
public class MyBean implements BeanNameAware {
    public void setBeanName(String name) {
        System.out.println("Bean Name: " + name);
    }
}
```

---

## 4. BeanPostProcessor (VERY IMPORTANT)

This is one of the most powerful features in Spring.

It allows you to:

> Modify bean behavior before and after initialization

```java id="e4y8pw"
@Component
public class CustomProcessor implements BeanPostProcessor {

    public Object postProcessBeforeInitialization(Object bean, String name) {
        System.out.println("Before Init: " + name);
        return bean;
    }

    public Object postProcessAfterInitialization(Object bean, String name) {
        System.out.println("After Init: " + name);
        return bean;
    }
}
```

Used internally by Spring for:

* AOP
* Proxies
* Security
* Transactions

---

## 5. Initialization Phase

### 5.1 @PostConstruct (Recommended)

```java id="9q8v2m"
@PostConstruct
public void init() {
    System.out.println("Bean initialized");
}
```

---

### 5.2 InitializingBean Interface

```java id="4d2r8x"
public class MyBean implements InitializingBean {
    public void afterPropertiesSet() {
        System.out.println("Init via interface");
    }
}
```

---

### 5.3 Custom Init Method

```java id="8y3f7n"
@Bean(initMethod = "init")
public MyBean myBean() {
    return new MyBean();
}
```

---

## 6. Bean Ready to Use

At this stage:

* Bean is fully initialized
* Dependencies are injected
* Ready for application use

---

## 7. Destruction Phase

Triggered when:

* Application shuts down
* Context is closed

---

### 7.1 @PreDestroy (Recommended)

```java id="0x6k2p"
@PreDestroy
public void destroy() {
    System.out.println("Bean destroyed");
}
```

---

### 7.2 DisposableBean Interface

```java id="2r7h4v"
public class MyBean implements DisposableBean {
    public void destroy() {
        System.out.println("Destroyed via interface");
    }
}
```

---

### 7.3 Custom Destroy Method

```java id="7c1d9u"
@Bean(destroyMethod = "cleanup")
public MyBean myBean() {
    return new MyBean();
}
```

---

## 8. Lifecycle Order (Important)

Execution order:

1. Constructor
2. Dependency Injection
3. Aware Interfaces
4. `postProcessBeforeInitialization()`
5. `@PostConstruct`
6. `afterPropertiesSet()`
7. Custom init()
8. `postProcessAfterInitialization()`
9. Bean ready

On shutdown:
10. `@PreDestroy`
11. destroy()
12. custom destroy()

---

## 9. Real-World Use Cases

### Logging

```java id="3f9a1x"
@PostConstruct
public void logStart() {
    System.out.println("Service started");
}
```

### Resource Initialization

* DB connections
* Cache loading
* File reading

### Cleanup

* Closing DB connections
* Stopping threads

---

## 10. Singleton vs Prototype Lifecycle

### Singleton

* Full lifecycle managed
* Destroy methods called

### Prototype

* Spring creates bean
* DOES NOT manage destruction

Important:

> You must manually clean prototype beans

---

## 11. Common Mistakes

* Using multiple init methods unnecessarily
* Forgetting destruction logic
* Misunderstanding BeanPostProcessor
* Assuming prototype beans are destroyed automatically

---

## 12. Best Practices

* Prefer `@PostConstruct` and `@PreDestroy`
* Avoid overusing interfaces
* Use BeanPostProcessor only when needed
* Keep lifecycle logic lightweight

---
