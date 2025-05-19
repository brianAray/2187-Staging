# Spring Transactions Notes

### **Spring Transactions**

Spring provides a robust transaction management framework to ensure data consistency and integrity when performing operations on a database. Transactions group a series of actions so that they either all succeed or all fail, ensuring the database remains in a consistent state.

---

### **Key Concepts of Transactions**

1. **ACID Properties:**
    - **Atomicity:** All operations in a transaction succeed or none do.
    - **Consistency:** Transactions leave the database in a consistent state.
    - **Isolation:** Transactions are isolated from each other.
    - **Durability:** Committed transactions persist even after a system failure.
2. **Transactional Boundary:**
    - Defines the start and end of a transaction.
3. **Rollback:**
    - Ensures that all database changes are undone if a transaction fails.
4. **Propagation:**
    - Determines how a method's transaction participates in existing transactions.

---

### **Spring Transaction Management**

1. **Declarative Transactions:**
    - Use `@Transactional` annotation to define transaction boundaries.
2. **Programmatic Transactions:**
    - Use Spring’s `TransactionTemplate` or `PlatformTransactionManager`.
3. **Transaction Propagation:**
    - Defines how transactions behave across multiple methods.
4. **Transaction Isolation:**
    - Controls how concurrent transactions interact with each other.

---

### **Setting Up Spring Transactions**

### **1. Add Dependencies**

**Maven:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.transaction</groupId>
    <artifactId>spring-tx</artifactId>
</dependency>

```

### **2. Enable Transaction Management**

Add the `@EnableTransactionManagement` annotation to a configuration class or the main application class.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.transaction.annotation.EnableTransactionManagement;

@SpringBootApplication
@EnableTransactionManagement
public class TransactionDemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(TransactionDemoApplication.class, args);
    }
}

```

---

### **Using `@Transactional`**

The `@Transactional` annotation is used to define transactional boundaries declaratively.

### **Example Service with Transactions**

```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class ProductService {

    private final ProductRepository productRepository;

    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Transactional
    public void saveProduct(Product product) {
        productRepository.save(product);

        // Simulating an exception to trigger a rollback
        if (product.getPrice() < 0) {
            throw new IllegalArgumentException("Price cannot be negative!");
        }
    }
}

```

---

### **Propagation and Isolation**

### **Transaction Propagation**

Propagation determines how transactions behave when multiple transactional methods are called.

| **Propagation Type** | **Description** |
| --- | --- |
| `REQUIRED` (default) | Joins an existing transaction or creates a new one if none exists. |
| `REQUIRES_NEW` | Suspends the existing transaction and creates a new one. |
| `NESTED` | Creates a nested transaction within an existing one. |
| `MANDATORY` | Requires an existing transaction; throws an exception if none exists. |
| `SUPPORTS` | Runs within a transaction if one exists; otherwise runs non-transactionally. |
| `NOT_SUPPORTED` | Suspends the current transaction and runs non-transactionally. |
| `NEVER` | Runs non-transactionally; throws an exception if a transaction exists. |

**Example:**

```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void saveWithNewTransaction(Product product) {
    productRepository.save(product);
}

```

### **Transaction Isolation**

Isolation defines how transactions interact with each other when accessing shared data.

| **Isolation Level** | **Description** |
| --- | --- |
| `DEFAULT` | Uses the database's default isolation level. |
| `READ_UNCOMMITTED` | Allows dirty reads (reading uncommitted changes). |
| `READ_COMMITTED` | Prevents dirty reads; allows non-repeatable reads. |
| `REPEATABLE_READ` | Prevents dirty and non-repeatable reads; allows phantom reads. |
| `SERIALIZABLE` | Prevents dirty, non-repeatable, and phantom reads; the highest isolation level. |

**Example:**

```java
@Transactional(isolation = Isolation.SERIALIZABLE)
public void saveWithSerializableIsolation(Product product) {
    productRepository.save(product);
}

```

---

### **Rollback in Transactions**

Spring rolls back transactions automatically for **unchecked exceptions** (subclasses of `RuntimeException`) but **not for checked exceptions** by default.

### **Forcing Rollback on Checked Exceptions:**

```java
@Transactional(rollbackFor = Exception.class)
public void saveProductWithRollback(Product product) throws Exception {
    productRepository.save(product);
    throw new Exception("Simulating an exception!");
}

```

### **Prevent Rollback on Specific Exceptions:**

```java
@Transactional(noRollbackFor = IllegalArgumentException.class)
public void saveProductWithoutRollback(Product product) {
    productRepository.save(product);
    throw new IllegalArgumentException("Simulating a non-rollback exception!");
}

```

---

### **Programmatic Transactions**

You can also manage transactions programmatically using `TransactionTemplate`.

**Example:**

```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.support.TransactionTemplate;

@Service
public class ProductService {

    private final ProductRepository productRepository;
    private final TransactionTemplate transactionTemplate;

    public ProductService(ProductRepository productRepository, TransactionTemplate transactionTemplate) {
        this.productRepository = productRepository;
        this.transactionTemplate = transactionTemplate;
    }

    public void saveProduct(Product product) {
        transactionTemplate.execute(status -> {
            productRepository.save(product);
            if (product.getPrice() < 0) {
                status.setRollbackOnly();
            }
            return null;
        });
    }
}

```

---

### **Testing Transactions**

### **Using `@Transactional` in Tests**

The `@Transactional` annotation ensures that changes made during tests are rolled back after the test completes.

**Example:**

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.transaction.annotation.Transactional;

@SpringBootTest
public class ProductServiceTest {

    @Autowired
    private ProductService productService;

    @Autowired
    private ProductRepository productRepository;

    @Test
    @Transactional
    void testSaveProduct() {
        Product product = new Product();
        product.setName("Test Product");
        product.setPrice(100.0);

        productService.saveProduct(product);

        assertEquals(1, productRepository.findAll().size());
    }
}

```

---

### **Best Practices for Transactions**

1. **Keep Transactions Short:**
    - Avoid long-running transactions to reduce database locks and improve performance.
2. **Use Propagation Wisely:**
    - Understand when to create new transactions (`REQUIRES_NEW`) and when to join existing ones (`REQUIRED`).
3. **Rollback Intentionally:**
    - Use `rollbackFor` or `noRollbackFor` for specific exception handling.
4. **Log and Monitor Transactions:**
    - Use logs or AOP to track transaction start, commit, and rollback events.
5. **Avoid Transactions in Controllers:**
    - Controllers should delegate transactional logic to the service layer.
6. **Test Transactional Behavior:**
    - Write tests to validate rollback and commit scenarios.

---