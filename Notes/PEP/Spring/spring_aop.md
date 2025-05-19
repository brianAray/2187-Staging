# Spring AOP Notes

### **Spring AOP (Aspect-Oriented Programming)**

**Aspect-Oriented Programming (AOP)** is a programming paradigm that allows you to modularize cross-cutting concerns, such as logging, security, transaction management, and exception handling, into separate units called **aspects**. Spring AOP is an implementation of AOP based on the **proxy pattern**.

---

### **Key Concepts in Spring AOP**

1. **Aspect:**
    - A module that encapsulates cross-cutting concerns.
    - Defined using the `@Aspect` annotation.
2. **Join Point:**
    - A specific point in the execution of the application, such as method execution or object initialization, where an aspect can be applied.
3. **Advice:**
    - The action taken by an aspect at a particular join point.
    - Types of advice:
        - **Before Advice**: Executes before the join point.
        - **After Advice**: Executes after the join point (success or failure).
        - **After Returning Advice**: Executes after the join point successfully completes.
        - **After Throwing Advice**: Executes if the join point throws an exception.
        - **Around Advice**: Wraps the join point, allowing custom behavior before and after its execution.
4. **Pointcut:**
    - A predicate that matches join points, determining where advice should be applied.
5. **Weaving:**
    - The process of applying aspects to the target objects.

---

### **Why Use Spring AOP?**

- **Centralized Logic:**
    - Write reusable logic (e.g., logging, security) in one place.
- **Separation of Concerns:**
    - Keep business logic separate from cross-cutting concerns.
- **Improved Maintainability:**
    - Reduce code duplication and improve clarity.

---

### **Setting Up Spring AOP**

### **1. Add Dependencies**

**Maven:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>

```

**Gradle:**

```
implementation 'org.springframework.boot:spring-boot-starter-aop'

```

### **2. Enable AspectJ Auto Proxying**

Add the `@EnableAspectJAutoProxy` annotation to the configuration class or main application class to enable AOP.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@SpringBootApplication
@EnableAspectJAutoProxy
public class SpringAopApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringAopApplication.class, args);
    }
}

```

---

### **Creating Aspects**

### **Example Aspect**

```java
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore() {
        System.out.println("Logging before method execution...");
    }

    @AfterReturning("execution(* com.example.service.*.*(..))")
    public void logAfterReturning() {
        System.out.println("Logging after successful method execution...");
    }

    @AfterThrowing("execution(* com.example.service.*.*(..))")
    public void logAfterThrowing() {
        System.out.println("Logging after an exception...");
    }

    @Around("execution(* com.example.service.*.*(..))")
    public Object logAround(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("Logging before method execution (around)...");
        Object result = joinPoint.proceed();
        System.out.println("Logging after method execution (around)...");
        return result;
    }
}

```

---

### **Pointcut Expressions**

Pointcut expressions determine where advice should be applied. They use patterns to match methods or classes.

1. **Match All Methods in a Package:**
    
    ```java
    @Before("execution(* com.example.service.*.*(..))")
    
    ```
    
2. **Match Specific Method by Name:**
    
    ```java
    @Before("execution(* com.example.service.MyService.myMethod(..))")
    
    ```
    
3. **Match Methods with Specific Arguments:**
    
    ```java
    @Before("execution(* com.example.service.*.*(String))")
    
    ```
    
4. **Match Methods with Annotations:**
    
    ```java
    @Before("@annotation(com.example.annotations.MyCustomAnnotation)")
    
    ```
    

---

### **Using `@Around` for Custom Logic**

`@Around` advice is the most powerful and versatile advice type. It allows custom behavior before and after method execution.

```java
@Around("execution(* com.example.service.*.*(..))")
public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    Object result = joinPoint.proceed(); // Proceed with the method execution
    long elapsedTime = System.currentTimeMillis() - start;
    System.out.println("Execution time: " + elapsedTime + "ms");
    return result;
}

```

---

### **Real-World Use Cases**

1. **Logging:**
    - Automatically log method calls, parameters, and execution times.
2. **Security:**
    - Apply security checks before accessing sensitive methods.
3. **Transaction Management:**
    - Start, commit, or rollback transactions around methods.
4. **Performance Monitoring:**
    - Measure method execution time.
5. **Exception Handling:**
    - Log or handle exceptions consistently across the application.

---

### **Complete Example**

### **Service Class**

```java
import org.springframework.stereotype.Service;

@Service
public class ProductService {
    public String getProductById(Long id) {
        System.out.println("Executing getProductById...");
        return "Product-" + id;
    }

    public void deleteProduct(Long id) {
        System.out.println("Executing deleteProduct...");
        throw new RuntimeException("Exception while deleting product");
    }
}

```

### **Aspect Class**

```java
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class ProductAspect {

    @Before("execution(* com.example.service.ProductService.*(..))")
    public void logBefore() {
        System.out.println("Logging before ProductService method...");
    }

    @AfterReturning("execution(* com.example.service.ProductService.*(..))")
    public void logAfterReturning() {
        System.out.println("Logging after returning from ProductService method...");
    }

    @AfterThrowing("execution(* com.example.service.ProductService.*(..))")
    public void logAfterThrowing() {
        System.out.println("Logging exception in ProductService method...");
    }
}

```

### **Test the Application**

Run the application and call the methods:

```java
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

@Component
public class AppRunner implements CommandLineRunner {

    private final ProductService productService;

    public AppRunner(ProductService productService) {
        this.productService = productService;
    }

    @Override
    public void run(String... args) throws Exception {
        productService.getProductById(1L);
        try {
            productService.deleteProduct(2L);
        } catch (Exception ignored) {}
    }
}

```

**Output:**

```
Logging before ProductService method...
Executing getProductById...
Logging after returning from ProductService method...
Logging before ProductService method...
Executing deleteProduct...
Logging exception in ProductService method...

```

---

### **Best Practices for Spring AOP**

1. **Keep Aspects Focused:**
    - Each aspect should address a single concern (e.g., logging or security).
2. **Avoid Overusing AOP:**
    - Use AOP sparingly to avoid making the application difficult to debug.
3. **Log Exceptions Separately:**
    - Use `@AfterThrowing` for exception logging instead of mixing it with other advice.
4. **Combine Pointcuts for Clarity:**
    - Use reusable pointcut definitions for better maintainability.
    
    ```java
    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceLayer() {}
    
    @Before("serviceLayer()")
    public void logServiceLayer() {
        System.out.println("Service layer logging...");
    }
    
    ```
    

---