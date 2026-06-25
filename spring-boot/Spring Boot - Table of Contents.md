> **Baseline:** Spring Boot 3.2+, Java 17+, Jakarta EE namespaces (`jakarta.*`, not `javax.*`).

---

## 1. Introduction to Spring Boot

- Introduction
- Setting Up a Spring Boot Project (Initializr, `pom.xml`, starters, config files — `.yml` vs `.properties`)
- Beans
- Dependency Injection
- Spring Framework vs Spring Boot
- Auto-Configuration
- Startup Flow
- Maven Lifecycles and Commands

---

## 2. Spring MVC and REST APIs

- Spring MVC Architecture (`DispatcherServlet`, `HandlerMapping`, `ViewResolver`)
- Presentation Layer (`@RestController`, `@RequestMapping`, `@PathVariable`, `@RequestParam`, `@RequestBody`, DTOs)
- Persistence Layer (orientation; `@Entity` + `JpaRepository`, Lombok, `findById` Optional, H2 — see 3.1 Hibernate and JPA for full JPA)
- Service Layer (`@Service`, `@Transactional`, self-invocation)
- `ResponseEntity` (status codes, headers, builder methods)
- Request Validation (`@Valid`, Bean Validation, `MethodArgumentNotValidException`)
- Exception Handling (`ProblemDetail` RFC 7807, custom `ApiError` with trace ID, `@RestControllerAdvice`, `@ResponseStatus`)
- API Response Patterns (`Page<T>`, custom `ApiResponse<T>` envelope, `ResponseBodyAdvice` auto-wrap, plain REST vs wrapped)

---

## 3. Hibernate and Spring Data JPA

- Hibernate and JPA (ORM fundamentals, `@Entity`, `@Id` / `@GeneratedValue`, `@EmbeddedId` / `@IdClass`, `@MapsId`)
- Spring Data JPA (`JpaRepository`, CRUD, derived queries, `@Query`, `@Modifying`, `@Procedure`)
- Sorting and Pagination (`Sort`, `Pageable`, `Page<T>`, `Slice<T>`, cursor/keyset)
- Projections (interface-based, DTO, record, dynamic, closed vs open)
- `EntityManager`, Persistence Context & Entity Lifecycle (factory + EM hierarchy, transient/persistent/detached/removed, dirty checking, equals/hashCode, persist vs merge vs save, L1 vs L2 cache)
- Entity Relationships (`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`, owning vs inverse, bidirectional sync helpers)
- Cascading and Orphan Removal (`CascadeType`, `orphanRemoval`, soft delete with `@SQLDelete` / `@SQLRestriction` or Hibernate 6.4+ `@SoftDelete`)
- Transactions (JPA persistence context binding, `LazyInitializationException` behavior — see 11.6 `@Transactional` Annotation for full coverage)
- N+1 Query Problem (`JOIN FETCH`, `@EntityGraph`, batch fetching, DTO projection)

---

## 4. Production-Ready Features

- Dev Tools (auto-restart, LiveReload, two-classloader model)
- Auditing (`@CreatedDate`, `@LastModifiedDate`)
- REST Client (`RestTemplate`, `WebClient`, `RestClient`)
- Logging (SLF4J, Logback)
- Spring Boot Actuator (health, metrics, info endpoints)
- OpenAPI and Swagger (Springdoc, `@Operation`, `@Schema`)

---

## 5. Spring Security Fundamentals

- Security Concepts and Attacks (SOP, CORS, CSRF, XSS, SQL Injection)
- Spring Security Filter Chain
- Authentication Core Components (`AuthenticationManager`, `UserDetailsService`)
- Filter Chain Configuration (`HttpSecurity` options, `SecurityFilterChain` patterns, generic reference)
- Session-Based Authentication (`.formLogin()`, API-style backend, in-memory users, remember-me, session-based CSRF)
- Understanding JWT (structure, claims, signing)
- JWT Implementation (`JwtService`, `AuthService`, `AuthController`, `SecurityConfig`, `JwtAuthFilter`, exception handling, project recap)

### Appendix

- Encoding & Password Hashing (Hex / Base64 / Base64URL, bcrypt anatomy, salts, cost factor)

---

## 6. Spring Security Advanced

- Access and Refresh Tokens (lifetimes, rotation, storage trade-offs)
- User Sessions Management with JWT (multi-device, session limit, logout)
- Google OAuth2 Client Authentication (`@EnableOAuth2Client`, IdP, auth-code flow)
- Role Based Authorization (`hasRole`, `hasAnyRole`, `GrantedAuthority`)
- Granular Authorization with Permissions (role vs authority, permission decoupling)
- Method-Level Security (`@Secured`, `@PreAuthorize`, SpEL, layered security)

---

## 7. Spring Boot Testing

- Introduction to Testing
- JUnit and AssertJ (`@Test`, `assertThat`)
- Unit vs Integration Testing (test pyramid)
- Persistence Layer Testing and TestContainers (`@DataJpaTest`)
- Service Layer Unit Testing with Mockito (`@Mock`, `@Spy`, `@InjectMocks`, `ArgumentCaptor`)
- Integration Testing (`@SpringBootTest`, `WebTestClient`)
- Spring Security Testing (`@WithMockUser`, `@WithUserDetails`, JWT in tests, CSRF helpers)
- JaCoCo Test Report Generation

---

## 8. Deployment & CI/CD

- Spring Profiles (`@Profile`, `application-{profile}.properties`, `spring.profiles.active`)
- Database Migration with Flyway (versioned SQL, `flyway_schema_history`, baseline-on-migrate)
- Setup Production Database with RDS
- Deploy on Elastic Beanstalk
- CI/CD with AWS CodePipeline and CodeBuild

---

## 10. Aspect-Oriented Programming

- Introduction to Aspect Oriented Programming (cross-cutting concerns, aspect/joinpoint/pointcut/advice/weaving)
- Declaring Pointcuts in AOP (`execution`, `within`, `@annotation`, `JoinPoint`, `@Pointcut`)
- Declaring Advice in AOP (`@Before`, `@After`, `@Around`, `@AfterReturning`, `@AfterThrowing`)
- Spring Proxy and Internal Working of AOP (JDK dynamic proxy vs CGLIB, self-invocation, weaving)
- Real World Use Cases of AOP (logging, monitoring, vs built-in `@Transactional` / `@Cacheable` / `@PreAuthorize`)

> Section 9 is a placeholder for a topic to be added later.

---

## 11. Caching and Concurrent Transaction Management

- Introduction to Caching (cache-aside, write-through, eviction)
- Spring Boot Default Caching (`@Cacheable`, `@CacheEvict`, `@CachePut`)
- Redis Cache in Spring Boot (TTL, serialization, distributed cache)
- Database Transactions and ACID Properties (`BEGIN`/`COMMIT`/`ROLLBACK`, Atomicity/Consistency/Isolation/Durability)
- Concurrent Transaction Management and Isolation Levels (Dirty/Non-Repeatable/Phantom Reads, Read Committed/Repeatable Read/Serializable)
- `@Transactional` Annotation in Spring Boot (propagation, isolation, `rollbackFor`, self-invocation)
- Optimistic and Pessimistic Locks in Spring Data JPA (`@Version`, `@Lock`, `FOR UPDATE`)

---

## 12. Microservices

- Introduction to Microservice Architecture (monolith vs microservices, when-to-use)
- Setting Up the Order and Inventory Services (Order + Inventory services, DB-per-service)
- Service Registration and Discovery with Eureka (`@EnableEurekaServer`, `DiscoveryClient`, heartbeats)
- Spring Cloud API Gateway (Routes, Predicates, Filters, `StripPrefix`, `lb://`)
- Service-to-Service Communication with OpenFeign (`@FeignClient`, `@EnableFeignClients`, declarative HTTP)
- Circuit Breaker, Retry and Rate Limiter with Resilience4J (`@CircuitBreaker`, `@Retry`, `@RateLimiter`, fallback)

---

## 13. Advanced Microservice Concepts

- Introduction to API Gateway Filters (`GlobalFilter`, `AbstractGatewayFilterFactory`, pre/post)
- Authentication in API Gateway using Custom `GatewayFilter`s (JWT, `X-User-Id`, per-route `enabled`)
- Centralized Configuration Server (`@EnableConfigServer`, Git-backed, profile precedence)
- Refresh Configuration without Restart (`@RefreshScope`, `/actuator/refresh`)
- Distributed Tracing using Zipkin & Micrometer (Trace ID, Span ID, sampling)
- Centralized Logging with ELK Stack (Elasticsearch, Logstash, Kibana, search by Trace ID)

---

## 14. Apache Kafka

- Introduction to Kafka
- Kafka Architecture (cluster/broker/node, partitions, replication, ISR, consumer groups, offsets, KRaft)
- Installing Kafka & Kafbat UI
- Kafka Configuration with Spring Boot (producer, consumer, `KafkaTemplate`, `@KafkaListener`)
- Advanced Kafka Configuration with Spring Boot (JSON serializers, trusted packages, error handling)
- Kafka Schema Registry with Confluent (Avro, schema evolution, compatibility modes)

---

## Further Reading

General references useful across the whole handbook:

- [Baeldung — Spring Boot](https://www.baeldung.com/spring-boot) — canonical reference for most Spring Boot topics
- [Marco Behler — Spring Framework Guide](https://www.marcobehler.com/guides/spring-framework) — deep dive on Spring Framework fundamentals including IoC/DI
- [Marco Behler — Spring Boot Autoconfiguration](https://www.marcobehler.com/guides/spring-boot-autoconfiguration) — in-depth auto-configuration walkthrough
lkthrough
