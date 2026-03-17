
## Advanced Data Handling & Transactions (JPA, Hibernate, Performance, Scaling)

---

## 1. Why This Matters

In real-world systems:

* Data layer becomes the **bottleneck**
* Poor queries = slow APIs
* Bad transaction design = data inconsistency

This section goes beyond basics into:

> **Performance, internals, and real-world database design with Spring**

---

## 2. JPA vs Hibernate (Deep Understanding)

### JPA

* Specification (interface/standard)
* Defines how ORM should work

### Hibernate

* Implementation of JPA
* Provides actual behavior

---

### Key Insight

> You code against JPA, but Hibernate executes everything under the hood

---

## 3. Entity Lifecycle (Critical for Interviews)

Entities go through multiple states:

1. **Transient**

   * Object created but not persisted

2. **Persistent**

   * Managed by EntityManager
   * Synced with DB

3. **Detached**

   * No longer managed

4. **Removed**

   * Marked for deletion

---

### Example Flow

```java
User user = new User(); // Transient
entityManager.persist(user); // Persistent
entityManager.detach(user); // Detached
entityManager.remove(user); // Removed
```

---

## 4. Persistence Context (First-Level Cache)

### What it is

A cache inside EntityManager.

---

### Behavior

* Stores entities during transaction
* Prevents duplicate DB queries

---

### Example

```java
User u1 = entityManager.find(User.class, 1);
User u2 = entityManager.find(User.class, 1);
```

Only one DB query is executed.

---

### Key Insight

> Persistence context ensures identity and consistency

---

## 5. Dirty Checking Mechanism

Hibernate automatically tracks changes.

---

### Example

```java
User user = entityManager.find(User.class, 1);
user.setName("New Name");
```

No explicit save call needed.

---

### What happens internally

* Hibernate compares old vs new state
* Generates SQL UPDATE automatically

---

## 6. Flushing (Very Important)

### What is Flush?

Synchronizing persistence context with DB.

---

### When it happens

* Before transaction commit
* Before query execution

---

### Manual Flush

```java
entityManager.flush();
```

---

### Key Insight

> Flush does NOT commit transaction — it only syncs changes

---

## 7. Transaction Management (Deep Dive)

### @Transactional Internals

Spring uses:

* AOP proxies
* PlatformTransactionManager

---

### Flow

1. Method annotated with @Transactional
2. Proxy intercepts method
3. Starts transaction
4. Executes method
5. Commit / Rollback

---

### Example

```java
@Transactional
public void createUser() {
}
```

---

## 8. Transaction Propagation

Defines behavior when multiple transactions exist.

---

### Important Types

* REQUIRED (default)
* REQUIRES_NEW
* SUPPORTS
* MANDATORY

---

### Example

```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
```

---

### Key Insight

> Controls transaction boundaries in complex flows

---

## 9. Isolation Levels

Control concurrency behavior.

---

### Types

* READ_UNCOMMITTED
* READ_COMMITTED
* REPEATABLE_READ
* SERIALIZABLE

---

### Problem Solved

* Dirty reads
* Phantom reads
* Non-repeatable reads

---

## 10. N+1 Query Problem (Very Important)

### Problem

Fetching related entities causes multiple queries.

---

### Example

```java
List<User> users = userRepository.findAll();
for (User u : users) {
    u.getOrders(); // triggers extra query
}
```

---

### Result

1 query + N queries = performance issue

---

### Solutions

* Fetch Join
* EntityGraph
* Batch fetching

---

## 11. Lazy vs Eager Loading

### Lazy (default for collections)

* Loads data when accessed

### Eager

* Loads immediately

---

### Key Insight

> Use Lazy by default to avoid performance issues

---

## 12. Fetch Join (Optimization)

```java
@Query("SELECT u FROM User u JOIN FETCH u.orders")
List<User> findAllUsersWithOrders();
```

---

## 13. Second-Level Cache

### What it is

Cache shared across sessions.

---

### Tools

* EhCache
* Redis

---

### Key Insight

> Reduces DB load significantly

---

## 14. Pagination & Sorting

### Why Important

Avoid loading huge datasets.

---

### Example

```java
Pageable pageable = PageRequest.of(0, 10);
userRepository.findAll(pageable);
```

---

## 15. Indexing (Database Level)

Indexes improve query performance.

---

### Example

```sql
CREATE INDEX idx_user_email ON users(email);
```

---

## 16. Batch Processing

### Problem

Saving thousands of records individually is slow.

---

### Solution

```java
hibernate.jdbc.batch_size=50
```

---

### Key Insight

> Reduces DB round trips

---

## 17. Optimistic vs Pessimistic Locking

### Optimistic

* Uses version field
* No lock until conflict

### Pessimistic

* Locks row in DB

---

### Example

```java
@Version
private int version;
```

---

## 18. DTO Projections (Performance Optimization)

Avoid loading full entity.

---

### Example

```java
@Query("SELECT new com.dto.UserDTO(u.name) FROM User u")
```

---

## 19. Native Queries vs JPQL

### JPQL

* Works on entities

### Native SQL

* Direct DB query

---

### Trade-off

* JPQL → portable
* Native → faster but DB-specific

---

## 20. Open Session in View (OSIV)

### What it does

Keeps session open during view rendering.

---

### Problem

* Can cause hidden DB queries
* Performance issues

---

### Recommendation

Disable in production.

---

## 21. Connection Pooling

### Why Important

Creating DB connections is expensive.

---

### Tool

* HikariCP (default in Spring Boot)

---

## 22. Performance Tuning Checklist

* Use Lazy loading
* Avoid N+1 queries
* Use pagination
* Add indexes
* Use caching
* Optimize queries

---

## 23. Real-World Flow

```text
Controller
  ↓
Service (@Transactional)
  ↓
Repository (JPA)
  ↓
Hibernate
  ↓
Database
```

---
