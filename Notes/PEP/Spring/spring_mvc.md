# **Spring MVC Notes**

Spring MVC is a component of the **Spring Framework** designed to simplify the development of web applications by using the **Model-View-Controller (MVC)** design pattern. It separates the application's concerns into three components: **Model**, **View**, and **Controller**, which promotes a clean and modular architecture.

---

### **Core Concepts of Spring MVC**

1. **Model:**
    - Represents the application's data and business logic.
    - Typically consists of objects (POJOs) and services.
2. **View:**
    - Defines how the data (model) is presented to the user.
    - Can use JSP, Thymeleaf, or other template engines for rendering.
3. **Controller:**
    - Handles HTTP requests, processes data (via the model), and returns the appropriate view.

---

### **Features of Spring MVC**

1. **Annotation-Based Configuration:**
    - Uses annotations like `@Controller`, `@RequestMapping`, and `@RestController` to define endpoints.
2. **RESTful APIs:**
    - Easily create RESTful web services with `@RestController`.
3. **Flexible View Resolution:**
    - Supports multiple view technologies (e.g., JSP, Thymeleaf, and PDF/Excel views).
4. **Data Binding:**
    - Maps HTTP request parameters to Java objects using annotations like `@ModelAttribute` and `@RequestBody`.
5. **Validation:**
    - Built-in validation with `javax.validation` and `@Valid`.
6. **Exception Handling:**
    - Custom exception handling with `@ExceptionHandler` or `@ControllerAdvice`.

---

### **Setting Up a Spring MVC Application**

### **1. Add Dependencies**

**Maven:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

```

**Gradle:**

```
implementation 'org.springframework.boot:spring-boot-starter-web'

```

---

### **2. Create a Controller**

**Controller Example:**

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/")
    public String home(Model model) {
        model.addAttribute("message", "Welcome to Spring MVC!");
        return "home"; // View name (resolved as home.html or home.jsp)
    }
}

```

---

### **3. Create a View**

**Thymeleaf View (`home.html`):**

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Home</title>
</head>
<body>
    <h1 th:text="${message}">Welcome</h1>
</body>
</html>

```

---

### **4. Run the Application**

Use `SpringApplication.run()` in the main class to start the application.

**Main Class:**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringMvcApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringMvcApplication.class, args);
    }
}

```

---

### **Common Spring MVC Annotations**

| **Annotation** | **Description** |
| --- | --- |
| `@Controller` | Indicates a class is a Spring MVC controller. |
| `@RestController` | Combines `@Controller` and `@ResponseBody` for RESTful APIs. |
| `@RequestMapping` | Maps HTTP requests to controller methods. |
| `@GetMapping` | Shortcut for `@RequestMapping(method = RequestMethod.GET)`. |
| `@PostMapping` | Shortcut for `@RequestMapping(method = RequestMethod.POST)`. |
| `@RequestParam` | Maps request parameters to method arguments. |
| `@PathVariable` | Maps URI path variables to method arguments. |
| `@ModelAttribute` | Binds request parameters to model attributes. |
| `@RequestBody` | Maps the request body to a Java object (e.g., JSON to POJO). |
| `@ResponseBody` | Maps the return value of a method directly to the HTTP response body. |
| `@ExceptionHandler` | Handles exceptions raised in the controller. |

---

### **Spring MVC Workflow**

1. **HTTP Request:**
    - The client sends an HTTP request to a specific URL.
2. **DispatcherServlet:**
    - The **front controller** of Spring MVC that intercepts requests and delegates them to appropriate handlers.
3. **Handler Mapping:**
    - Determines which controller method should handle the request based on URL mappings.
4. **Controller:**
    - Executes business logic, interacts with the model, and prepares the data.
5. **View Resolver:**
    - Determines which view (HTML, JSP, etc.) should be rendered.
6. **View:**
    - The view is rendered and returned as an HTTP response.

---