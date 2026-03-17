
## Testing in Spring (Unit, Integration, Mocking, Test Architecture)

---

## 1. Why Testing is Critical in Spring Applications

In real-world systems:

* Code changes frequently
* Multiple developers work on same codebase
* Bugs in production are costly

Testing ensures:

* Code correctness
* Stability during refactoring
* Confidence in deployments

---

## 2. Types of Testing in Spring Ecosystem

### 2.1 Unit Testing

* Tests individual classes
* No Spring context
* Fast execution

---

### 2.2 Integration Testing

* Tests interaction between components
* Loads Spring context
* Slower but more realistic

---

### 2.3 End-to-End Testing

* Tests full system flow
* Includes database, APIs, and services

---

## 3. Testing Stack in Spring

* JUnit → Testing framework
* Mockito → Mocking dependencies
* Spring Test → Integration support
* MockMvc → API testing

---

## 4. Unit Testing (Deep Understanding)

### Goal

Test business logic in isolation.

---

### Example

```java
class UserServiceTest {

    private UserRepository userRepository = Mockito.mock(UserRepository.class);
    private UserService userService = new UserService(userRepository);

    @Test
    void shouldReturnUser() {
        Mockito.when(userRepository.findById(1L))
               .thenReturn(Optional.of(new User()));

        User user = userService.getUser(1L);

        assertNotNull(user);
    }
}
```

---

### Key Insight

> No Spring Boot startup → extremely fast

---

## 5. Mockito (Mocking Framework)

### Why Needed

To isolate unit under test.

---

### Common Methods

* `mock()` → create mock object
* `when()` → define behavior
* `verify()` → check interactions

---

### Example

```java
verify(userRepository).findById(1L);
```

---

## 6. @Mock vs @InjectMocks

### @Mock

Creates mock dependency

### @InjectMocks

Injects mocks into class under test

---

### Example

```java
@Mock
UserRepository repo;

@InjectMocks
UserService service;
```

---

## 7. Integration Testing (Spring Context)

Loads full or partial Spring container.

---

### Annotation

```java
@SpringBootTest
```

---

### Behavior

* Starts application context
* Autowires beans
* Uses real components

---

### Example

```java
@SpringBootTest
class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;

    @Test
    void testRealFlow() {
    }
}
```

---

## 8. Slice Testing (Important Optimization)

Instead of loading full context, load only required parts.

---

### Types

* `@WebMvcTest` → Controller layer
* `@DataJpaTest` → Repository layer
* `@RestClientTest` → REST clients

---

### Example

```java
@WebMvcTest(UserController.class)
class UserControllerTest {
}
```

---

### Key Insight

> Faster than full integration tests

---

## 9. Testing Controllers with MockMvc

### Purpose

Test HTTP layer without starting server.

---

### Example

```java
@Autowired
private MockMvc mockMvc;

@Test
void testGetUser() throws Exception {
    mockMvc.perform(get("/users/1"))
           .andExpect(status().isOk());
}
```

---

### What it Simulates

* HTTP request
* Controller execution
* Response validation

---

## 10. Testing REST APIs (Full Flow)

```java
@SpringBootTest
@AutoConfigureMockMvc
class ApiTest {

    @Autowired
    MockMvc mockMvc;
}
```

---

## 11. Database Testing

### Problem

Tests should not affect real DB.

---

### Solution

* Use H2 in-memory database

---

### Example

```properties
spring.datasource.url=jdbc:h2:mem:testdb
```

---

## 12. @DataJpaTest (Repository Testing)

* Loads only JPA components
* Uses in-memory DB

---

### Example

```java
@DataJpaTest
class UserRepositoryTest {

    @Autowired
    UserRepository repo;
}
```

---

## 13. Transaction Rollback in Tests

By default:

* Transactions rollback after each test

---

### Benefit

* Clean database state

---

## 14. Test Configuration

Use separate config:

```properties
application-test.properties
```

---

## 15. Test Profiles

```java
@ActiveProfiles("test")
```

---

## 16. Mocking External Services

### Problem

External APIs should not be called in tests.

---

### Solution

* Mock REST clients
* Use WireMock

---

## 17. Testcontainers (Advanced)

Run real services in Docker during tests.

---

### Example

* PostgreSQL container
* Kafka container

---

### Benefit

> Realistic integration testing

---

## 18. Performance Testing Considerations

* Avoid full context when not needed
* Use slice tests
* Parallel test execution

---

## 19. Common Pitfalls

* Overusing @SpringBootTest
* Not mocking dependencies
* Using real DB in unit tests
* Slow test suite

---

## 20. Test Pyramid (Important Concept)

```text
        E2E Tests (Few)
     Integration Tests (Some)
  Unit Tests (Many)
```

---

### Key Insight

> Majority should be unit tests for speed and maintainability

---

## 21. Real-World Testing Strategy

* Unit tests for services
* Slice tests for controllers/repositories
* Integration tests for critical flows
* E2E tests for business scenarios

---

