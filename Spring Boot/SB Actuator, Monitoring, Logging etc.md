

## Spring Boot Actuator, Monitoring, Logging & Production Readiness

---

## 1. Why This Topic Matters

Building an application is only half the job.

In real-world systems, you must:

* Monitor application health
* Track metrics
* Debug issues in production
* Ensure reliability and uptime

Spring Boot provides built-in tools for this:

> **Actuator + Logging + Metrics + External Monitoring Integration**

---

## 2. Spring Boot Actuator (Core Concept)

Spring Boot Actuator adds **production-ready endpoints** to your application.

These endpoints expose:

* Health status
* Application metrics
* Environment properties
* Thread info
* Beans info

---

## 3. Adding Actuator

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## 4. Actuator Endpoints (Deep Understanding)

### Important Endpoints

* `/actuator/health`
* `/actuator/info`
* `/actuator/metrics`
* `/actuator/env`
* `/actuator/beans`
* `/actuator/loggers`
* `/actuator/threaddump`
* `/actuator/heapdump`

---

### Example: Health Endpoint

```json
{
  "status": "UP"
}
```

---

### Advanced Health Info

You can include:

* Database health
* Disk space
* Custom checks

---

## 5. Exposing Endpoints

By default, only limited endpoints are exposed.

```properties
management.endpoints.web.exposure.include=*
```

---

## 6. Securing Actuator Endpoints

Never expose all endpoints publicly in production.

```java
http
  .authorizeHttpRequests(auth -> auth
      .requestMatchers("/actuator/**").hasRole("ADMIN")
  );
```

---

## 7. Custom Health Indicators

You can create your own health checks.

```java
@Component
public class CustomHealthIndicator implements HealthIndicator {

    public Health health() {
        if (serviceIsUp()) {
            return Health.up().build();
        }
        return Health.down().withDetail("error", "Service down").build();
    }
}
```

---

## 8. Metrics (Micrometer Integration)

Spring Boot uses **Micrometer** for metrics collection.

---

### Common Metrics

* JVM memory
* CPU usage
* HTTP request count
* Response time

---

### Example Endpoint

```
/actuator/metrics/http.server.requests
```

---

## 9. Exporting Metrics

Metrics can be sent to:

* Prometheus
* Grafana
* Datadog
* New Relic

---

## 10. Logging (Deep Dive)

Logging is critical for debugging and monitoring.

---

### Default Logger

Spring Boot uses:

> Logback

---

### Log Levels

* TRACE
* DEBUG
* INFO
* WARN
* ERROR

---

### Configuration

```properties
logging.level.root=INFO
logging.level.com.example=DEBUG
```

---

## 11. Logback Configuration

Custom config file:

```
logback-spring.xml
```

---

### Example

```xml
<configuration>
    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>app.log</file>
    </appender>
</configuration>
```

---

## 12. Structured Logging

Use JSON logs for production systems.

Why:

* Easy parsing
* Works with ELK stack (Elasticsearch, Logstash, Kibana)

---

## 13. Distributed Tracing (Concept)

In microservices:

* One request → multiple services

Tracing tools:

* Zipkin
* OpenTelemetry

---

## 14. Correlation ID

Used to track a request across services.

Example:

```
X-Correlation-ID: 12345
```

---

## 15. Externalized Configuration

Production apps must not hardcode configs.

---

### application.properties

```properties
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/db
```

---

### Profiles

```properties
spring.profiles.active=prod
```

---

### Profile-based Config

```
application-dev.properties
application-prod.properties
```

---

## 16. Environment Variables

Used in production:

```properties
spring.datasource.url=${DB_URL}
```

---

## 17. Configuration Priority (Important)

Order of precedence:

1. Command line args
2. Environment variables
3. application.properties
4. Default values

---

## 18. Graceful Shutdown

Allows app to finish ongoing requests before stopping.

```properties
server.shutdown=graceful
```

---

## 19. Thread Management (Tomcat)

```properties
server.tomcat.threads.max=200
```

---

## 20. Production Best Practices

* Never expose all actuator endpoints
* Always secure sensitive endpoints
* Use centralized logging
* Monitor metrics continuously
* Use health checks for load balancers
* Enable graceful shutdown

---

