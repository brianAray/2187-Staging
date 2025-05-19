# Spring Data Notes

### **Spring Data**

Spring Data is a module of the Spring Framework that simplifies data access and persistence in applications. It provides a consistent and simplified programming model for interacting with various data sources, including relational databases, NoSQL databases, and distributed data systems.

The most widely used sub-project of Spring Data is **Spring Data JPA**, which is designed for working with JPA-based repositories.

---

### **Core Features of Spring Data**

1. **Repository Abstraction:**
    - Provides a high-level repository interface (`CrudRepository`, `JpaRepository`) for data access.
    - Eliminates the need for boilerplate code like `SELECT` or `INSERT` statements.
2. **Query Methods:**
    - Supports derived query methods based on method names (e.g., `findByName`).
3. **Pagination and Sorting:**
    - Built-in support for paginated and sorted data retrieval.
4. **Custom Queries:**
    - Allows writing custom JPQL or SQL queries.
5. **Auditing:**
    - Automatically captures metadata like created/modified dates and users.
6. **Support for Multiple Databases:**
    - Supports relational databases (e.g., MySQL, PostgreSQL) and NoSQL databases (e.g., MongoDB, Cassandra).

---

### **Key Components**

1. **Repository Interfaces**
    - Predefined interfaces like `JpaRepository` and `CrudRepository` provide methods for CRUD operations.
2. **Annotations**
    - Annotations like `@Query` for custom queries, `@Modifying` for update/delete queries, and `@Entity` for mapping Java objects to database tables.
3. **Transactional Support**
    - Ensures data integrity with the help of Spring’s `@Transactional` annotation.

---

### **Spring Data JPA Overview**

Spring Data JPA is a subproject of Spring Data that provides an abstraction layer over JPA (Java Persistence API) for working with relational databases. It integrates seamlessly with Hibernate, EclipseLink, and other JPA providers.

### **1. Add Spring Data JPA Dependency**

**Maven:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.h2</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>

```

**Gradle:**

```
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
runtimeOnly 'com.h2database:h2'

```

---

### **Example of Spring Data JPA**

### **1. Entity Class**

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

---

### **2. Repository Interface**

Spring Data JPA eliminates the need to implement the repository manually. The repository interface provides CRUD operations out of the box.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface ProductRepository extends JpaRepository<Product, Long> {
    Product findByName(String name);
}

```

---

### **3. Service Layer**

Use the repository in the service layer to manage business logic.

```java
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class ProductService {

    private final ProductRepository productRepository;

    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    public List<Product> findAllProducts() {
        return productRepository.findAll();
    }

    public Product findProductByName(String name) {
        return productRepository.findByName(name);
    }

    public Product saveProduct(Product product) {
        return productRepository.save(product);
    }
}

```

---

### **4. Controller Layer**

```java
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/products")
public class ProductController {

    private final ProductService productService;

    public ProductController(ProductService productService) {
        this.productService = productService;
    }

    @GetMapping
    public List<Product> getAllProducts() {
        return productService.findAllProducts();
    }

    @GetMapping("/{name}")
    public Product getProductByName(@PathVariable String name) {
        return productService.findProductByName(name);
    }

    @PostMapping
    public Product createProduct(@RequestBody Product product) {
        return productService.saveProduct(product);
    }
}

```

---

### **Custom Queries with `@Query`**

If derived query methods are insufficient, use `@Query` for custom JPQL or native SQL queries.

### Example of JPQL Query:

```java
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

public interface ProductRepository extends JpaRepository<Product, Long> {

    @Query("SELECT p FROM Product p WHERE p.price > :price")
    List<Product> findProductsByPriceGreaterThan(@Param("price") double price);
}

```

### Example of Native Query:

```java
import org.springframework.data.jpa.repository.Query;

public interface ProductRepository extends JpaRepository<Product, Long> {

    @Query(value = "SELECT * FROM Product WHERE price > :price", nativeQuery = true)
    List<Product> findProductsByPriceGreaterThanNative(@Param("price") double price);
}

```

---

### **Pagination and Sorting**

Spring Data JPA supports pagination and sorting via the `Pageable` interface.

### Example:

```java
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;

public interface ProductRepository extends JpaRepository<Product, Long> {
    Page<Product> findAll(Pageable pageable);
}

```

### Usage:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.domain.PageRequest;
import org.springframework.data.domain.Sort;
import org.springframework.stereotype.Service;

@Service
public class ProductService {

    @Autowired
    private ProductRepository productRepository;

    public List<Product> getProductsPaginated(int page, int size) {
        return productRepository.findAll(PageRequest.of(page, size, Sort.by("name"))).getContent();
    }
}

```

---