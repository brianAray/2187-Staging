# Spring Boot Notes

## Overview of Spring Boot

Spring Boot is a popular Java-based framework designed to simplify the development of stand-alone, production-ready applications. It builds on the Spring Framework by adding powerful features such as auto-configuration and embedded servers, which significantly reduce boilerplate code and setup time. Below is an overview of its core features, advantages, and use cases.

---

### **Core Features of Spring Boot**

1. **Auto-Configuration**
    - Automatically configures Spring applications based on the libraries and dependencies present in the classpath.
    - Reduces the need for manual configuration in XML or Java.
2. **Standalone Applications**
    - Includes an embedded server (e.g., Tomcat, Jetty) to run applications without requiring external deployment.
    - Allows applications to be launched as a simple Java program (`java -jar`).
3. **Opinionated Defaults**
    - Provides sensible default configurations to get applications up and running quickly.
    - Allows customization if defaults don’t fit specific requirements.
4. **Spring Boot Starters**
    - Pre-defined dependency descriptors that bundle commonly used libraries for a particular functionality (e.g., `spring-boot-starter-web`, `spring-boot-starter-data-jpa`).
    - Simplifies dependency management.
5. **Production-Ready Features**
    - Built-in support for metrics, health checks, application monitoring, and externalized configuration.
    - Includes tools like Spring Boot Actuator for monitoring and management.
6. **Externalized Configuration**
    - Supports configuration through property files, YAML, environment variables, and command-line arguments.
    - Enables easy application portability across environments.
7. **Spring Boot CLI**
    - A command-line interface to quickly prototype and run Spring Boot applications using Groovy scripts.

---

### **Key Components of Spring Boot**

1. **Spring Boot Actuator**
    - Adds endpoints for monitoring and managing the application.
    - Example: `/health` for health checks, `/metrics` for application metrics.
2. **Spring Boot DevTools**
    - Enhances developer productivity by enabling features like automatic application restart and live reload during development.
3. **Embedded Servers**
    - Includes embedded Tomcat, Jetty, or Undertow servers, removing the need for a separate application server.
4. **Spring Initializr**
    - A web-based tool for generating Spring Boot projects with the desired dependencies and configurations.

---

### **Advantages of Spring Boot**

1. **Rapid Development**
    - Speeds up application setup with minimal configuration.
2. **Reduced Boilerplate**
    - Eliminates repetitive code and configuration.
3. **Microservices-Friendly**
    - Well-suited for developing microservices architectures.
4. **Seamless Integration**
    - Integrates with popular technologies like Hibernate, JPA, RabbitMQ, Kafka, and others.
5. **Scalability**
    - Provides a robust foundation for building scalable and production-ready applications.

---

### **Common Use Cases**

1. **REST APIs**
    - Create RESTful web services using `spring-boot-starter-web`.
2. **Microservices**
    - Ideal for building and deploying distributed systems.
3. **Data-Driven Applications**
    - Integrates seamlessly with databases via Spring Data JPA, MongoDB, or other persistence technologies.
4. **Enterprise Applications**
    - Develop scalable and secure business applications.
5. **Batch Processing**
    - Support for batch jobs via Spring Batch.

---

## Auto-Configuration

### **Spring Boot Auto-Configuration**

**Auto-Configuration** is one of the most powerful features of Spring Boot. It simplifies the process of configuring an application by automatically setting up the necessary beans and components based on the application's dependencies and classpath. This reduces the need for boilerplate configuration and allows developers to focus on business logic.

---

### **How Auto-Configuration Works**

1. **Classpath Inspection**
    - Spring Boot scans the classpath to detect which libraries and dependencies are available.
    - Based on these findings, it applies relevant configurations automatically.
2. **Conditional Configuration**
    - Uses conditional annotations (e.g., `@ConditionalOnClass`, `@ConditionalOnMissingBean`) to decide whether a particular configuration should be applied.
    - Configuration is only applied if the required classes or beans are present/missing.
3. **Default Bean Creation**
    - Provides default beans for commonly used configurations if no custom beans are defined by the developer.
4. **Customization**
    - Developers can override the defaults by defining their own beans or using properties in `application.properties` or `application.yml`.

---

### **Key Components of Auto-Configuration**

1. **`@EnableAutoConfiguration`**
    - Triggers the auto-configuration process.
    - Automatically applied when using `@SpringBootApplication`, as it includes `@EnableAutoConfiguration`.
2. **Spring Factories**
    - Spring Boot uses the `spring.factories` file (under `META-INF/`) to list all available auto-configuration classes.
    - Example: `org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration` for configuring Spring MVC.
3. **Conditional Annotations**
    - **`@ConditionalOnClass`**: Applies configuration if a specified class is on the classpath.
    - **`@ConditionalOnMissingBean`**: Applies configuration if a specific bean is not defined.
    - **`@ConditionalOnProperty`**: Applies configuration if a specific property is set.

---

### **Customization of Auto-Configuration**

### 1. **Using `application.properties` or `application.yml`**

- Externalize configuration by setting properties to fine-tune defaults.
- Example:
    
    ```
    spring.jpa.hibernate.ddl-auto=update
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
    
    ```
    

### 2. **Excluding Specific Auto-Configuration**

- Use `@SpringBootApplication(exclude = {AutoConfigClass.class})` to disable specific configurations.
- Example:
    
    ```java
    @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
    public class MyApplication {
    }
    
    ```
    

---

### **Advantages of Auto-Configuration**

1. **Reduces Boilerplate Code**
    - Eliminates the need to write extensive configuration files manually.
2. **Faster Development**
    - Speeds up the development process by providing ready-to-use setups.
3. **Flexible Customization**
    - Allows developers to override or exclude configurations when needed.
4. **Seamless Integration**
    - Automatically configures components based on popular libraries like Hibernate, Thymeleaf, RabbitMQ, and others.

---

## Overview of Common Spring Boot Starters (Web, Data JPA)

Spring Boot Starters are pre-configured dependency bundles that simplify the setup and configuration of commonly used features in Spring applications. Each starter is designed to bring together all the necessary dependencies for a specific functionality.

Two of the most commonly used starters are **Spring Boot Starter Web** and **Spring Boot Starter Data JPA**.

---

### **1. Spring Boot Starter Web**

**Purpose**: To simplify the development of web applications, including RESTful APIs.

### **Dependencies Added**

- **Spring MVC**: For building web applications and RESTful APIs.
- **Tomcat**: Embedded web server (can be replaced with Jetty or Undertow).
- **Jackson**: For JSON serialization and deserialization.
- **Validation API**: For validating input data.

### **Key Features**

- **RESTful Web Services**: Simplifies the creation of REST endpoints.
- **Embedded Web Server**: Eliminates the need for an external web server.
- **View Layer Support**: Provides integration with view technologies like Thymeleaf and FreeMarker.
- **Exception Handling**: Default support for exception handling using `@ControllerAdvice`.

### **Example Usage**

**Dependencies in `pom.xml`:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

```

**Controller Example:**

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot Web!";
    }
}

```

**Configuration Example (`application.properties`):**

```
server.port=8080

```

---

### **2. Spring Boot Starter Data JPA**

**Purpose**: To simplify data access and persistence using Java Persistence API (JPA) and Hibernate.

### **Dependencies Added**

- **Spring Data JPA**: Simplifies data access by providing a repository abstraction.
- **Hibernate**: Default JPA implementation.
- **Database Driver**: Requires manual addition of a database driver (e.g., MySQL, PostgreSQL).

### **Key Features**

- **Repository Abstraction**: Auto-generates implementations for repositories (e.g., `JpaRepository`).
- **Transaction Management**: Built-in support for managing transactions.
- **Database Schema Initialization**: Automatically creates or updates database schema based on JPA entities.
- **Query Methods**: Allows custom queries using method names (e.g., `findByName`).

### **Example Usage**

**Dependencies in `pom.xml`:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

```

**Entity Example:**

```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class Product {
    @Id
    private Long id;
    private String name;
    private double price;

    // Getters and setters
}

```

**Repository Example:**

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
    Product findByName(String name);
}

```

**Configuration Example (`application.properties`):**

```
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=myuser
spring.datasource.password=mypassword
spring.jpa.hibernate.ddl-auto=update

```

---

### **Comparison of Spring Boot Starter Web and Data JPA**

| Feature | Spring Boot Starter Web | Spring Boot Starter Data JPA |
| --- | --- | --- |
| **Primary Use Case** | Build web applications and RESTful APIs | Access and manage relational databases |
| **Key Components** | Spring MVC, Tomcat, Jackson | Spring Data JPA, Hibernate, Database Driver |
| **Focus** | Web layer | Data persistence layer |
| **Example Endpoint** | `/hello` (REST API) | `findByName` (Database query) |

---

## DevTools

**Spring Boot DevTools** is a module designed to enhance developer productivity by providing features like automatic application restart, live reload, and property defaults. These features make the development process more efficient and reduce the time spent on repetitive tasks.

---

### **Key Features of Spring Boot DevTools**

1. **Automatic Restart**
    - Automatically restarts the application whenever changes are detected in the classpath (e.g., `.java` or `.properties` files).
    - This uses Spring Boot's classloader to reload only the modified parts, making it faster than a full restart.
2. **Live Reload**
    - Works with **LiveReload** to automatically refresh the browser when static files (like HTML, CSS, or JavaScript) are updated.
    - Requires a LiveReload browser plugin or a compatible IDE setup.
3. **Property Defaults**
    - Includes sensible defaults for development environments:
        - `cache` is disabled for templates.
        - HTTP caching headers are disabled.
4. **Remote Debugging**
    - Enables remote updates and restarts by allowing connections to a running application from a remote machine.
5. **Environment-Specific Behavior**
    - DevTools is only active in the development environment. It is excluded in production by default to avoid unnecessary overhead.

---

### **How to Enable DevTools**

### **Add Dependency**

**Maven:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope> <!-- Ensures DevTools is not included in the production build -->
</dependency>

```

---

### **Features in Detail**

### **1. Automatic Restart**

- Monitors classpath changes and restarts the application when changes are detected.
- Useful for quick testing of changes without manually restarting the server.

**How It Works:**

- DevTools uses two classloaders:
    - **Base ClassLoader**: For classes that are unlikely to change (e.g., third-party libraries).
    - **Restart ClassLoader**: For classes under development.

### **2. Live Reload**

- Automatically refreshes the browser when static files are updated.
- Requires a **LiveReload browser extension** for seamless integration.

### **3. Property Defaults**

- Disables certain optimizations to favor development speed:
    
    ```
    spring.thymeleaf.cache=false
    spring.freemarker.cache=false
    spring.groovy.template.cache=false
    spring.mustache.cache=false
    
    ```
    
- Disables HTTP caching to ensure the browser always fetches updated resources.

### **4. Remote Debugging**

- Enables debugging of a remotely deployed application.
- Requires setting up remote restart via the property:
    
    ```
    spring.devtools.remote.secret=mySecret
    
    ```
    
- You can use the `spring-boot-devtools` module in a remote environment for quick restarts and updates.

---

### **Configuration Properties**

- **Disabling Restart**
To disable the automatic restart feature:
    
    ```
    spring.devtools.restart.enabled=false
    
    ```
    
- **Exclude Specific Paths**
To prevent specific directories or files from triggering a restart:
    
    ```
    spring.devtools.restart.exclude=static/**,public/**
    
    ```
    
- **Watching Additional Paths**
To monitor additional paths for changes:
    
    ```
    spring.devtools.restart.additional-paths=/path/to/watch
    
    ```
    

---

## Spring Environments

### **Spring Environments**

In Spring, **environments** allow developers to define and manage different configurations for various deployment stages, such as **development**, **testing**, and **production**. By organizing configurations into environments, you can ensure the application behaves appropriately for the context in which it is running.

---

### **Key Concepts in Spring Environments**

1. **Profiles**
    - A profile represents a specific environment (e.g., `dev`, `test`, `prod`).
    - Profiles enable selective activation of beans, properties, and other configurations.
2. **Property Sources**
    - Externalized configurations (e.g., `application.properties`, `application.yml`, environment variables) that can vary across environments.
3. **Environment Abstraction**
    - The `Environment` interface provides access to active profiles, default profiles, and property values.

---

### **Setting Up Spring Environments**

### **1. Using Profiles**

Spring profiles enable environment-specific configurations.

- **Activate Profiles**:
    - Use the `spring.profiles.active` property to specify the active profile.
    - Example in `application.properties`:
        
        ```
        spring.profiles.active=dev
        
        ```
        
- **Profile-Specific Files**:
    - Use `application-{profile}.properties` or `application-{profile}.yml` for environment-specific configurations.
    - Example:
        - `application-dev.properties`:
            
            ```
            server.port=8081
            spring.datasource.url=jdbc:mysql://localhost:3306/devdb
            
            ```
            
        - `application-prod.properties`:
            
            ```
            server.port=8080
            spring.datasource.url=jdbc:mysql://prod-server:3306/proddb
            
            ```
            

### **2. Bean Scoping with Profiles**

Use the `@Profile` annotation to load beans conditionally based on the active profile.

```java
import org.springframework.context.annotation.Profile;
import org.springframework.stereotype.Service;

@Service
@Profile("dev")
public class DevDataService implements DataService {
    @Override
    public String getData() {
        return "Development Data";
    }
}

```

```java
@Service
@Profile("prod")
public class ProdDataService implements DataService {
    @Override
    public String getData() {
        return "Production Data";
    }
}

```

### **3. Environment-Specific Configuration**

Retrieve environment-specific properties programmatically using the `Environment` interface.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class MyAppConfig {
    @Autowired
    private Environment environment;

    public void printActiveProfiles() {
        for (String profile : environment.getActiveProfiles()) {
            System.out.println("Active Profile: " + profile);
        }
    }
}

```

---

### **Ways to Set Active Profiles**

1. **In `application.properties` or `application.yml`**
    
    ```
    spring.profiles.active=dev
    
    ```
    
2. **As Command-Line Arguments**
    
    ```bash
    java -jar myapp.jar --spring.profiles.active=prod
    
    ```
    
3. **As Environment Variables**
    
    ```bash
    export SPRING_PROFILES_ACTIVE=prod
    
    ```
    
4. **In IDE Run Configurations**
    - Pass `-spring.profiles.active=dev` as a program argument in your IDE's run configuration.

---

### **Default Profiles**

If no profile is explicitly activated, Spring uses the **default profile**. Beans and properties without a `@Profile` annotation or profile-specific files are always loaded unless another profile is explicitly activated.

---

### **Property Sources in Environments**

1. **Hierarchical Order of Property Resolution**:
Spring resolves properties in the following order (from highest to lowest precedence):
    1. Command-line arguments
    2. `application-{profile}.properties` or `application-{profile}.yml`
    3. `application.properties` or `application.yml`
    4. Environment variables
    5. System properties (`D` arguments)
    6. Default properties
2. **Example of Property Resolution**:
    - If both `application.properties` and `application-dev.properties` specify `server.port`:
        - `application-dev.properties` takes precedence when `dev` is the active profile.

---