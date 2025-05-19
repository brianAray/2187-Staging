# Project 1 - Backend Fundamentals

This staging project will be focused on just the backend aspects of what you have learned in training and PEP. This goal is to familiarize yourself with the fundamentals of Spring, Java, SQL, and Testing.

## Technologies
- Java
- Spring Boot
- Spring Data JPA
- PostgreSQL
- JUnit
- Mockito

## Requirements

1. Simple CRUD API
    - Create and API for a single entity (e.g. Book or Product)
        - `GET /book` (list all)
        - `POST / books` (create)
        - `PUT /books/{id}` (update)
        - `DELETE /books/{id}` delete
    - Use Spring Data JPA for persistence
2. Testing
    - Write unit tests for the service layer using Mockito to mock the repository
3. Conceptual focus
    - While working on these technologies, be sure to revise and focus on the core ideas of them all
    - Focus on understanding them, this will help for your interviews when you can explain the technical aspects of the technologies and how you have implemented it yourself

### 1. Spring Framework

#### Key Concepts:
- Dependency Injection (DI):  
  - Objects receive dependencies (e.g., services, repositories) from an external source (e.g., Spring container) instead of creating them internally.  
  - Enables loose coupling and easier testing.  
  - Annotations: `@Autowired`, `@Component`, `@Service`, `@Repository`.

- Inversion of Control (IoC):  
  - The framework controls the application flow (e.g., creating/managing beans).  
  - Developers focus on business logic, not infrastructure.

- Spring MVC:  
  - Model-View-Controller architecture for web applications.  
  - Annotations: `@Controller`, `@RequestMapping`, `@GetMapping`.

### 2. Spring Boot

#### Key Concepts:
- Auto-Configuration:  
  - Automatically configures beans based on dependencies (e.g., `spring-boot-starter-data-jpa` sets up JPA/Hibernate).  
  - Override defaults via `application.properties` or `application.yml`.

- Embedded Servers:  
  - Runs as a standalone JAR with embedded Tomcat, Jetty, or Undertow.  
  - No need for external server deployment.

- Starter Dependencies:  
  - Predefined dependency bundles (e.g., `spring-boot-starter-web` for MVC).  
  - Reduces dependency conflicts and boilerplate.

- Spring Boot Actuator:  
  - Adds production-ready endpoints (e.g., `/health`, `/metrics`) for monitoring.

- Annotation: `@SpringBootApplication` (combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`).

### 3. Spring Data JPA  
Simplifies database access by abstracting JPA (Java Persistence API) boilerplate.

#### Key Concepts:
- Repository Abstraction:  
  - Interfaces like `CrudRepository` and `JpaRepository` provide built-in CRUD methods.  
  - Example:  
    ```java
    public interface UserRepository extends JpaRepository<User, Long> { 
        List<User> findByLastName(String lastName); // Auto-implemented query
    }
    ```

- Query Methods:  
  - Derive SQL queries from method names (e.g., `findByEmailAndAge` → `WHERE email = ? AND age = ?`).  
  - Custom queries via `@Query` annotation.

- JPA Entity Mapping:  
  - Map Java objects to database tables using annotations:  
    - `@Entity`, `@Table`, `@Id`, `@GeneratedValue`.  
    - Relationships: `@OneToMany`, `@ManyToOne`, `@JoinColumn`.

- Transaction Management:  
  - Use `@Transactional` to define ACID-compliant transactions.  
  - Spring Data JPA integrates with Spring’s declarative transaction management.
