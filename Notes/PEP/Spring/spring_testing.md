# Spring Testing Notes

## Unit Testing Service Layer Methods with JUnit and Mockito

Unit testing the service layer in a Spring application ensures that the business logic behaves as expected. Using **JUnit** and **Mockito**, you can test the service layer by mocking dependencies such as repositories or other services.

---

### **Setup for Unit Testing**

1. **Add Dependencies**
Include JUnit 5 (or JUnit 4) and Mockito in your project.
    
    **Maven:**
    
    ```xml
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.10.0</version> <!-- Use the latest version -->
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>5.5.0</version>
        <scope>test</scope>
    </dependency>
    
    ```
    
    **Gradle:**
    
    ```
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.0'
    testImplementation 'org.mockito:mockito-core:5.5.0'
    
    ```
    
2. **Annotate with Testing Frameworks**
    - Use `@ExtendWith(MockitoExtension.class)` to integrate Mockito with JUnit 5.
    - For JUnit 4, use `MockitoAnnotations.initMocks()`.

---

### **Example Service Layer**

**Service Class:**

```java
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class ProductService {
    private final ProductRepository productRepository;

    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    public Product findById(Long id) {
        return productRepository.findById(id)
                .orElseThrow(() -> new IllegalArgumentException("Product not found"));
    }

    public List<Product> findAll() {
        return productRepository.findAll();
    }

    public Product save(Product product) {
        return productRepository.save(product);
    }
}

```

**Repository Interface:**

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
}

```

---

### **Unit Testing with JUnit and Mockito**

**Test Class:**

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.junit.jupiter.api.extension.ExtendWith;

import java.util.Arrays;
import java.util.Optional;

@ExtendWith(MockitoExtension.class)
public class ProductServiceTest {

    @Mock
    private ProductRepository productRepository;

    @InjectMocks
    private ProductService productService;

    private Product product;

    @BeforeEach
    void setUp() {
        product = new Product();
        product.setId(1L);
        product.setName("Test Product");
    }

    @Test
    void testFindById() {
        // Arrange
        when(productRepository.findById(1L)).thenReturn(Optional.of(product));

        // Act
        Product foundProduct = productService.findById(1L);

        // Assert
        assertNotNull(foundProduct);
        assertEquals("Test Product", foundProduct.getName());
        verify(productRepository, times(1)).findById(1L);
    }

    @Test
    void testFindById_NotFound() {
        // Arrange
        when(productRepository.findById(1L)).thenReturn(Optional.empty());

        // Act & Assert
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            productService.findById(1L);
        });
        assertEquals("Product not found", exception.getMessage());
        verify(productRepository, times(1)).findById(1L);
    }

    @Test
    void testFindAll() {
        // Arrange
        when(productRepository.findAll()).thenReturn(Arrays.asList(product));

        // Act
        var products = productService.findAll();

        // Assert
        assertNotNull(products);
        assertEquals(1, products.size());
        verify(productRepository, times(1)).findAll();
    }

    @Test
    void testSave() {
        // Arrange
        when(productRepository.save(product)).thenReturn(product);

        // Act
        Product savedProduct = productService.save(product);

        // Assert
        assertNotNull(savedProduct);
        assertEquals("Test Product", savedProduct.getName());
        verify(productRepository, times(1)).save(product);
    }
}

```

---

### **Key Concepts in Testing**

1. **Annotations:**
    - `@Mock`: Creates a mock instance of the dependency.
    - `@InjectMocks`: Automatically injects mocked dependencies into the class under test.
    - `@BeforeEach`: Runs setup code before each test.
2. **Mockito Methods:**
    - `when(...)`: Specifies the behavior of a mock for a given method call.
    - `verify(...)`: Ensures a specific method was called with expected arguments.
    - `times(...)`: Specifies how many times a method should have been invoked.
3. **JUnit Assertions:**
    - `assertEquals`: Verifies the expected and actual values are equal.
    - `assertNotNull`: Ensures an object is not `null`.
    - `assertThrows`: Asserts that a specific exception is thrown.

---

### **Best Practices**

1. **Test Edge Cases**
    - Test scenarios like null inputs, empty lists, and exceptions.
2. **Mock Only External Dependencies**
    - Avoid mocking the class under test itself.
3. **Isolate the Service Layer**
    - Ensure tests focus only on the service layer without involving the database or other external systems.
4. **Use Meaningful Assertions**
    - Ensure tests validate the actual business logic and not just method calls.

---

## Testing RESTful APIs with MockMvc and RestTemplate

Spring Boot provides tools like **MockMvc** and **RestTemplate** to test RESTful APIs effectively. These tools allow you to test the behavior of controllers, endpoints, and service interactions in isolation or as part of an integration test.

---

### **1. MockMvc**

**MockMvc** is a Spring testing utility for testing Spring MVC controllers. It provides a way to test API endpoints without starting the full server, focusing on the controller logic and request/response behavior.

### **Setup**

1. Add the following dependencies in `pom.xml` or `build.gradle`:
    
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
    
    ```
    
2. Annotate the test class with `@WebMvcTest` to focus on controller testing.

### **Example**

**Controller Class:**

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/products")
public class ProductController {
    @GetMapping("/{id}")
    public Product getProduct(@PathVariable Long id) {
        return new Product(id, "Sample Product");
    }

    @PostMapping
    public Product createProduct(@RequestBody Product product) {
        product.setId(1L);
        return product;
    }
}

```

**Test Class:**

```java
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;
import com.fasterxml.jackson.databind.ObjectMapper;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.web.servlet.MockMvc;

@WebMvcTest(ProductController.class)
public class ProductControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private ObjectMapper objectMapper;

    @Test
    void testGetProduct() throws Exception {
        mockMvc.perform(get("/api/products/1"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.name").value("Sample Product"));
    }

    @Test
    void testCreateProduct() throws Exception {
        Product newProduct = new Product(null, "New Product");
        String json = objectMapper.writeValueAsString(newProduct);

        mockMvc.perform(post("/api/products")
                        .contentType("application/json")
                        .content(json))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.name").value("New Product"));
    }
}

```

**Key Points:**

- `MockMvc` is used to simulate HTTP requests to the controller.
- `jsonPath` is used to validate JSON responses.
- `ObjectMapper` helps convert objects to JSON.

---

### **2. RestTemplate**

**RestTemplate** is a Spring class for making HTTP requests programmatically. It is often used in integration tests to test endpoints by sending real HTTP requests to the application.

### **Setup**

1. Ensure the application starts in a test environment. Use `@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)` to start the application on a random port.
2. Use `TestRestTemplate` for easier testing.

### **Example**

**Controller Class:**

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/products")
public class ProductController {
    @GetMapping("/{id}")
    public Product getProduct(@PathVariable Long id) {
        return new Product(id, "Sample Product");
    }

    @PostMapping
    public Product createProduct(@RequestBody Product product) {
        product.setId(1L);
        return product;
    }
}

```

**Test Class:**

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.boot.web.server.LocalServerPort;

import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class ProductControllerIntegrationTest {

    @LocalServerPort
    private int port;

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    void testGetProduct() {
        String url = "http://localhost:" + port + "/api/products/1";

        Product response = restTemplate.getForObject(url, Product.class);

        assertNotNull(response);
        assertEquals(1L, response.getId());
        assertEquals("Sample Product", response.getName());
    }

    @Test
    void testCreateProduct() {
        String url = "http://localhost:" + port + "/api/products";

        Product newProduct = new Product(null, "New Product");

        Product response = restTemplate.postForObject(url, newProduct, Product.class);

        assertNotNull(response);
        assertEquals(1L, response.getId());
        assertEquals("New Product", response.getName());
    }
}

```

**Key Points:**

- `TestRestTemplate` simplifies HTTP requests in integration tests.
- The `@LocalServerPort` annotation injects the random port the application is running on.

---

### **MockMvc vs. RestTemplate**

| **Feature** | **MockMvc** | **RestTemplate** |
| --- | --- | --- |
| **Purpose** | Tests controller logic in isolation. | Tests end-to-end API functionality. |
| **Server** | Does not start a server. | Starts the server. |
| **Test Scope** | Focuses on the controller. | Covers the full application stack. |
| **Performance** | Faster (no server startup). | Slower (due to server startup). |
| **Ideal For** | Unit tests. | Integration tests. |

---

## Testing Database Interactions

### **Approaches to Testing Database Interactions**

1. **Unit Testing (with Mocks):**
    - Mock the repository layer using **Mockito**.
    - Focuses on service logic without interacting with an actual database.
2. **Integration Testing (with an In-Memory Database):**
    - Use an in-memory database (e.g., H2) to test repository methods.
    - Ensures the correctness of queries, mappings, and transactions.
3. **End-to-End Testing (with Testcontainers or Real Database):**
    - Use a containerized database like **PostgreSQL** or **MySQL** to test real interactions.
    - Validates the application against the same database used in production.

---

### **Setting Up for Database Testing**

### **1. Add Dependencies**

**Maven:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>

```

**Gradle:**

```
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
testImplementation 'com.h2database:h2'
testImplementation 'org.springframework.boot:spring-boot-starter-test'

```

### **2. Configure an In-Memory Database**

**In `application-test.properties`:**

```
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=create-drop

```

---

### **Example: Testing a Repository**

### **Entity Class**

```java
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;

@Entity
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private double price;

    // Getters and Setters
}

```

### **Repository Interface**

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
    Product findByName(String name);
}

```

### **Test Class**

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
public class ProductRepositoryTest {

    @Autowired
    private ProductRepository productRepository;

    @Test
    void testSaveAndFind() {
        // Arrange
        Product product = new Product();
        product.setName("Test Product");
        product.setPrice(100.0);

        // Act
        Product savedProduct = productRepository.save(product);
        Product foundProduct = productRepository.findByName("Test Product");

        // Assert
        assertNotNull(savedProduct);
        assertNotNull(foundProduct);
        assertEquals("Test Product", foundProduct.getName());
        assertEquals(100.0, foundProduct.getPrice());
    }

    @Test
    void testFindById() {
        // Arrange
        Product product = new Product();
        product.setName("Another Product");
        product.setPrice(200.0);
        Product savedProduct = productRepository.save(product);

        // Act
        Product foundProduct = productRepository.findById(savedProduct.getId()).orElse(null);

        // Assert
        assertNotNull(foundProduct);
        assertEquals("Another Product", foundProduct.getName());
    }
}

```

---

## Spring Profiles for Test Environments

Spring profiles are a feature of the Spring Framework that allow developers to define environment-specific configurations. They are particularly useful for managing different configurations for **test environments** (e.g., unit testing, integration testing, or QA testing).

By using profiles, you can easily switch between configurations for development, testing, and production environments without changing the core application code.

---

### **Setting Up Spring Profiles for Testing**

1. **Default Profile Files**
    - **`application.properties` or `application.yml`**: Contains default properties for all environments.
    - **Profile-Specific Files**: Named as `application-{profile}.properties` or `application-{profile}.yml`, where `{profile}` is the profile name (e.g., `test`, `dev`, `prod`).
2. **Activating Profiles**
    - Set the active profile to `test` to load test-specific configurations.

---

### **Steps to Configure Test Profiles**

### **1. Create a Test Configuration File**

**`application-test.properties`**

```
# Database configuration for testing
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=create-drop

# Logging level
logging.level.root=WARN

```

---

### **2. Activate the Test Profile**

**a. Programmatically in Tests**
You can set the active profile programmatically using the `@ActiveProfiles` annotation.

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ActiveProfiles;

@SpringBootTest
@ActiveProfiles("test")
public class ProductServiceTest {
    @Test
    void testServiceMethod() {
        // Test logic here
    }
}

```

**b. In `application.properties`**
Set the active profile globally (useful for local testing):

```
spring.profiles.active=test

```

**c. Command-Line Arguments**
Activate the profile when running the application:

```bash
java -jar myapp.jar --spring.profiles.active=test

```

**d. Environment Variable**
Set the profile using the `SPRING_PROFILES_ACTIVE` environment variable:

```bash
export SPRING_PROFILES_ACTIVE=test

```

---

### **3. Test Profile in Action**

Suppose your application has a service that interacts with a database.

**Service Class:**

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

@Service
public class ConfigService {
    @Value("${spring.datasource.url}")
    private String dataSourceUrl;

    public String getDataSourceUrl() {
        return dataSourceUrl;
    }
}

```

**Test Class:**

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ActiveProfiles;

import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest
@ActiveProfiles("test")
public class ConfigServiceTest {

    @Autowired
    private ConfigService configService;

    @Test
    void testDataSourceUrl() {
        String expectedUrl = "jdbc:h2:mem:testdb";
        assertEquals(expectedUrl, configService.getDataSourceUrl());
    }
}

```

---

### **Using Multiple Profiles**

Sometimes, you may want to load a combination of profiles. Spring allows you to activate multiple profiles by separating them with commas:

```
spring.profiles.active=dev,test

```

In this case:

- Properties from `application-dev.properties` and `application-test.properties` will be loaded.
- If a property exists in both files, the profile listed last (e.g., `test`) takes precedence.

---

### **Best Practices for Test Profiles**

1. **Use an In-Memory Database for Testing**
    - Use H2 or another lightweight database for fast, isolated tests.
2. **Separate Test-Specific Configurations**
    - Keep test-related properties in `application-test.properties` to avoid affecting other environments.
3. **Rollback Transactions in Tests**
    - Use Spring’s `@Transactional` annotation to roll back database changes after each test.
4. **Mock External Dependencies**
    - Use mocks or stubs for external systems like third-party APIs to isolate tests.
5. **Parameterize Profiles**
    - Use environment variables or command-line arguments to activate profiles dynamically in CI/CD pipelines.
6. **Test All Profiles**
    - Regularly test all profiles (e.g., `dev`, `test`, `prod`) to ensure configuration integrity across environments.

---

### **Example Folder Structure**

```
src/main/resources/
├── application.properties
├── application-dev.properties
├── application-test.properties
├── application-prod.properties

src/test/java/
├── com.example.myapp/
│   ├── ConfigServiceTest.java
│   ├── ProductServiceTest.java

```

---

### **Testing Scenarios with Profiles**

| **Scenario** | **Profile** | **Purpose** |
| --- | --- | --- |
| Unit Tests | `test` | Fast and isolated tests with in-memory databases. |
| Integration Tests with Testcontainers | `test` | Tests with a containerized database (e.g., PostgreSQL). |
| Development Environment Testing | `dev` | Verify functionality against a dev database or staging APIs. |
| Production Configuration Validation | `prod` | Ensure all production settings are correctly applied. |

---