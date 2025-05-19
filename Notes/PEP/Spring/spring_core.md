# Spring Core Notes

### **Module: Introduction to Spring**

---

### **Introduction to Spring Framework**

The **Spring Framework** is a powerful, open-source framework for Java development that provides comprehensive infrastructure support for building Java applications. It is widely used for creating enterprise-level applications due to its focus on productivity, flexibility, and loose coupling.

### **1. Key Features of Spring Framework**

### **1.1 Dependency Injection (DI)**:

- Core feature that promotes loose coupling.
- Allows objects to define their dependencies and let the framework inject them automatically.

### **1.2 Inversion of Control (IoC)**:

- Central concept where control of object creation and lifecycle is handed over to the Spring IoC container.

### **1.3 Modular Design**:

- Spring is divided into modules that can be used independently, such as:
    - **Spring Core**: Core container for DI and IoC.
    - **Spring AOP**: Aspect-oriented programming.
    - **Spring MVC**: Web development framework.
    - **Spring Data**: Data access and persistence.

### **1.4 Integration with Other Frameworks**:

- Supports seamless integration with frameworks like Hibernate, JPA, and JMS.

### **1.5 Simplified Testing**:

- Provides utilities for testing, including integration with JUnit and TestNG.

### **1.6 Annotation-Based Configuration**:

- Reduces the need for XML configuration by using annotations like `@Component`, `@Service`, and `@Repository`.

### **2. Benefits of Spring Framework**

| **Benefit** | **Description** |
| --- | --- |
| **Productivity** | Simplifies development with reusable modules and extensive tools. |
| **Loose Coupling** | Dependency Injection and IoC promote modular, testable, and flexible code. |
| **Portability** | Applications built with Spring are platform-independent. |
| **Integration** | Seamlessly integrates with databases, messaging services, and third-party APIs. |
| **Testing Support** | Built-in tools for creating unit and integration tests. |

### **3. Spring Framework Architecture**

The architecture of Spring is built on several layers:

### **3.1 Core Container**

- The foundation of the Spring Framework, responsible for managing beans and their lifecycle.
- Includes modules like:
    - **Beans**: BeanFactory for IoC.
    - **Context**: ApplicationContext for advanced container features.

### **3.2 Data Access/Integration**

- Provides JDBC, ORM, JMS, and transaction management support.
- Modules: Spring JDBC, Spring ORM, Spring Data.

### **3.3 Web**

- Facilitates web development with Spring MVC and WebSocket support.
- Modules: Spring Web, Spring WebFlux.

### **3.4 AOP (Aspect-Oriented Programming)**

- Adds cross-cutting concerns like logging, security, and transaction management.

### **3.5 Test**

- Supports unit and integration testing.

---

### **Overview of Dependency Injection in Spring Framework**

**Dependency Injection (DI)** is a design pattern that helps achieve **loose coupling** in software components by providing a way to supply dependencies to an object instead of the object creating them itself. The Spring Framework uses DI as a core principle for managing the relationships between objects.

### **1. What is Dependency Injection?**

### **Definition**:

Dependency Injection is the process where an object’s dependencies (other objects it requires to function) are provided by an external entity, such as the **Spring IoC Container**, instead of the object creating them itself.

### **Key Concepts**:

1. **Dependency**: Any object that a class needs to perform its function.
    - Example: A `Car` class depends on an `Engine` class.
2. **Injection**: Supplying these dependencies to a class from outside rather than creating them internally.

### **2. Why Use Dependency Injection?**

| **Advantage** | **Description** |
| --- | --- |
| **Loose Coupling** | The dependent class does not need to know the details of its dependency implementation. |
| **Improved Testability** | Dependencies can be mocked or stubbed during testing, making it easier to test individual units. |
| **Code Reusability** | Components can be reused across different contexts without modification. |
| **Separation of Concerns** | Promotes modular code by separating object creation logic from business logic. |

### **3. Types of Dependency Injection in Spring**

| **Type** | **Description** | **Example** |
| --- | --- | --- |
| **Constructor Injection** | Dependencies are provided through the class constructor. | `@Autowired` on constructor. |
| **Setter Injection** | Dependencies are provided through public setter methods. | `@Autowired` on setter. |
| **Field Injection** | Dependencies are injected directly into fields (variables) using annotations like `@Autowired`. | Simplifies code but reduces testability. |

### **4. How Spring Implements Dependency Injection**

Spring uses the **IoC (Inversion of Control) Container** to manage dependencies and inject them into beans. The container is responsible for:

1. Instantiating beans.
2. Managing their lifecycle.
3. Resolving and injecting dependencies.

### **5. Comparison of DI Types**

| **Type** | **Advantages** | **Disadvantages** |
| --- | --- | --- |
| **Constructor Injection** | Ensures all dependencies are provided at the time of object creation. | Not suitable for optional dependencies; verbose for classes with many dependencies. |
| **Setter Injection** | Allows optional dependencies; more readable with many dependencies. | Dependencies can be accidentally omitted during configuration. |
| **Field Injection** | Simplifies code by directly injecting dependencies. | Harder to test due to private fields; violates explicit dependency principle. |

---

### **Types of Dependency Injection in Spring Framework**

Spring Framework supports three main types of **Dependency Injection (DI)**: **Constructor Injection**, **Setter Injection**, and **Field Injection**. Each has its use cases, advantages, and trade-offs.

### **1. Constructor Injection**

### **Overview**:

- Dependencies are provided through the **constructor** of the class.
- Ensures all required dependencies are provided at the time of object creation.

### **Advantages**:

- Promotes **immutability** since dependencies are set at construction and cannot be modified later.
- Ensures that the object is always in a valid state because required dependencies must be provided.
- Well-suited for **mandatory dependencies**.

### **Disadvantages**:

- Can become verbose if there are many dependencies.
- Complex dependencies can make constructors cumbersome.

### **Example**:

1. **Dependency Class**:
    
    ```java
    public class Engine {
        public void start() {
            System.out.println("Engine started.");
        }
    }
    
    ```
    
2. **Dependent Class**:
    
    ```java
    public class Car {
        private final Engine engine;
    
        // Constructor Injection
        public Car(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    
3. **XML Configuration**:
    
    ```xml
    <beans>
        <bean id="engine" class="com.example.Engine" />
        <bean id="car" class="com.example.Car">
            <constructor-arg ref="engine" />
        </bean>
    </beans>
    
    ```
    
4. **Annotation-Based**:
    
    ```java
    @Component
    public class Car {
        private final Engine engine;
    
        @Autowired
        public Car(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    

### **2. Setter Injection**

### **Overview**:

- Dependencies are provided through **setter methods** after the object is created.
- Ideal for **optional dependencies** that can be modified after object construction.

### **Advantages**:

- Suitable for **optional dependencies** or dependencies that might change during the object's lifecycle.
- Allows flexibility in testing by setting mock dependencies.

### **Disadvantages**:

- Object may remain in an invalid state if required dependencies are not set.
- Can make the code harder to maintain when misused for required dependencies.

### **Example**:

1. **Dependency Class**:
    
    ```java
    public class Engine {
        public void start() {
            System.out.println("Engine started.");
        }
    }
    
    ```
    
2. **Dependent Class**:
    
    ```java
    public class Car {
        private Engine engine;
    
        // Setter Injection
        public void setEngine(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            if (engine != null) {
                engine.start();
                System.out.println("Car is driving.");
            } else {
                System.out.println("No engine found!");
            }
        }
    }
    
    ```
    
3. **XML Configuration**:
    
    ```xml
    <beans>
        <bean id="engine" class="com.example.Engine" />
        <bean id="car" class="com.example.Car">
            <property name="engine" ref="engine" />
        </bean>
    </beans>
    
    ```
    
4. **Annotation-Based**:
    
    ```java
    @Component
    public class Car {
        private Engine engine;
    
        @Autowired
        public void setEngine(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    

### **3. Field Injection**

### **Overview**:

- Dependencies are injected directly into **fields** using the `@Autowired` annotation.
- Simplifies code by eliminating the need for setter or constructor methods.

### **Advantages**:

- Compact and concise.
- Easy to configure in simple applications.

### **Disadvantages**:

- Harder to test since dependencies are private and cannot be mocked easily.
- Reduces clarity about required dependencies and their lifecycle.

### **Example**:

1. **Dependency Class**:
    
    ```java
    public class Engine {
        public void start() {
            System.out.println("Engine started.");
        }
    }
    
    ```
    
2. **Dependent Class**:
    
    ```java
    @Component
    public class Car {
        @Autowired
        private Engine engine;
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    
3. **Configuration with Component Scanning**:
    
    ```java
    @Configuration
    @ComponentScan("com.example")
    public class AppConfig {}
    
    ```
    

### **4. Comparison of DI Types**

| **Type** | **Use Case** | **Advantages** | **Disadvantages** |
| --- | --- | --- | --- |
| **Constructor Injection** | Mandatory dependencies | Promotes immutability and ensures valid state | Verbose for many dependencies |
| **Setter Injection** | Optional or configurable dependencies | Flexible for optional dependencies; testable | Object can be in an invalid state without proper setup |
| **Field Injection** | Simple, concise configurations | Compact and eliminates boilerplate code | Difficult to test and reduces clarity |

### **5. Which Type to Use?**

- **Constructor Injection**:
    - Use when dependencies are **mandatory**.
    - Promotes immutability and clear dependency relationships.
- **Setter Injection**:
    - Use for **optional** dependencies or when values might change during the object's lifecycle.
- **Field Injection**:
    - Use for simple scenarios, but avoid for highly testable or complex components.

---

### **Injection Using XML-Based Configuration in Spring Framework**

In XML-based configuration, dependencies are defined in an XML file, and the Spring IoC container manages injecting those dependencies into beans. This approach was widely used in earlier versions of Spring and provides a declarative way to configure dependencies.

### **1. Steps for XML-Based Dependency Injection**

### **1.1 Create the Dependency Class**

```java
public class Engine {
    public void start() {
        System.out.println("Engine started.");
    }
}

```

### **1.2 Create the Dependent Class**

```java
public class Car {
    private Engine engine;

    // Constructor for Constructor Injection
    public Car(Engine engine) {
        this.engine = engine;
    }

    // Setter for Setter Injection
    public void setEngine(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving.");
    }
}

```

### **2. XML-Based Configurations**

### **2.1 Constructor Injection**

**XML Configuration**:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Define the Engine bean -->
    <bean id="engine" class="com.example.Engine" />

    <!-- Define the Car bean and inject dependency using constructor -->
    <bean id="car" class="com.example.Car">
        <constructor-arg ref="engine" />
    </bean>

</beans>

```

**Main Application**:

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Car car = context.getBean("car", Car.class);
        car.drive();
    }
}

```

### **2.2 Setter Injection**

**XML Configuration**:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Define the Engine bean -->
    <bean id="engine" class="com.example.Engine" />

    <!-- Define the Car bean and inject dependency using setter -->
    <bean id="car" class="com.example.Car">
        <property name="engine" ref="engine" />
    </bean>

</beans>

```

**Main Application**:

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Car car = context.getBean("car", Car.class);
        car.drive();
    }
}

```

### **3. Advantages of XML-Based Configuration**

| **Advantage** | **Description** |
| --- | --- |
| **Centralized Configuration** | All dependencies are defined in a single XML file. |
| **Non-Intrusive** | No need to modify Java code to define dependencies. |
| **Flexibility** | Can configure beans and dependencies at runtime. |
| **Legacy Support** | Works with older versions of Spring and non-annotation setups. |

### **4. Disadvantages of XML-Based Configuration**

| **Disadvantage** | **Description** |
| --- | --- |
| **Verbosity** | XML configurations can become lengthy and hard to maintain. |
| **Error-Prone** | Misspelled bean IDs or tags can lead to runtime errors. |
| **Less Modern** | Annotation-based and Java-based configurations are now preferred. |

---

### **Injection Using Java-Based Configuration in Spring Framework**

Java-based configuration in Spring uses **Java classes** and the `@Configuration` annotation to define beans and manage dependency injection. This approach is type-safe, concise, and easier to maintain compared to XML-based configuration.

### **1. Steps for Java-Based Dependency Injection**

### **1.1 Create the Dependency Class**

```java
public class Engine {
    public void start() {
        System.out.println("Engine started.");
    }
}

```

### **1.2 Create the Dependent Class**

```java
public class Car {
    private Engine engine;

    // Constructor Injection
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving.");
    }
}

```

### **1.3 Create the Configuration Class**

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine(); // Define Engine bean
    }

    @Bean
    public Car car() {
        return new Car(engine()); // Inject Engine bean into Car
    }
}

```

### **2. Running the Application**

1. **Main Application**:
    
    ```java
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.annotation.AnnotationConfigApplicationContext;
    
    public class Main {
        public static void main(String[] args) {
            ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            Car car = context.getBean(Car.class);
            car.drive();
        }
    }
    
    ```
    
2. **Output**:
    
    ```
    Engine started.
    Car is driving.
    
    ```
    

### **3. Types of Injection with Java-Based Configuration**

### **3.1 Constructor Injection**

This is achieved by invoking the constructor of the dependent class in the configuration class.

**Example**:

```java
@Bean
public Car car() {
    return new Car(engine()); // Inject Engine via constructor
}

```

### **3.2 Setter Injection**

This is achieved by calling a setter method of the dependent class in the configuration class.

1. **Update the Dependent Class**:
    
    ```java
    public class Car {
        private Engine engine;
    
        public void setEngine(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    
2. **Configuration Class**:
    
    ```java
    @Bean
    public Car car() {
        Car car = new Car();
        car.setEngine(engine()); // Inject Engine via setter
        return car;
    }
    
    ```
    

### **3.3 Field Injection (Using `@Autowired`)**

Field injection can be achieved using the `@Autowired` annotation.

1. **Update the Dependent Class**:
    
    ```java
    import org.springframework.beans.factory.annotation.Autowired;
    
    public class Car {
        @Autowired
        private Engine engine;
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    
2. **Configuration Class**:
    
    ```java
    @Configuration
    @ComponentScan("com.example")
    public class AppConfig {}
    
    ```
    
3. **Dependency Class with `@Component`**:
    
    ```java
    @Component
    public class Engine {
        public void start() {
            System.out.println("Engine started.");
        }
    }
    
    ```
    

### **4. Advantages of Java-Based Configuration**

| **Advantage** | **Description** |
| --- | --- |
| **Type-Safe** | Compile-time checks for bean dependencies. |
| **Readable and Maintainable** | Easier to understand compared to verbose XML configuration. |
| **Refactor-Friendly** | Changes to class names or package structures are automatically reflected. |
| **Custom Logic** | Enables the use of custom logic during bean creation. |
| **Integration** | Supports annotation-based and programmatic configurations. |

### **5. Disadvantages of Java-Based Configuration**

| **Disadvantage** | **Description** |
| --- | --- |
| **Code Overhead** | Increases the size of configuration classes for large projects. |
| **Complex for Large Configurations** | Manual bean definitions can become cumbersome for applications with many beans. |

---

### **Module: Inversion of Control**

---

### **Overview of Inversion of Control (IoC) in Spring Framework**

**Inversion of Control (IoC)** is a principle in software development where the control of object creation, configuration, and lifecycle management is transferred from the application to a container or framework. In the context of the **Spring Framework**, the IoC Container manages these responsibilities.

### **1. What is Inversion of Control?**

### **Definition**:

IoC is a design principle where the responsibility for managing the lifecycle and dependencies of objects is delegated to an external container, rather than being handled manually by the application.

### **Key Idea**:

- Instead of a class instantiating its dependencies, the **IoC Container** supplies them at runtime.

### **2. Why Use IoC?**

| **Benefit** | **Description** |
| --- | --- |
| **Loose Coupling** | Classes are not tightly coupled to their dependencies, improving code flexibility. |
| **Reusability** | Components can be reused in different contexts without changes. |
| **Separation of Concerns** | Business logic is decoupled from object creation and dependency management. |
| **Improved Testability** | Dependencies can be mocked or replaced during testing. |

### **3. IoC in the Spring Framework**

### **3.1 IoC Container**

The **IoC Container** is a core part of Spring that manages the lifecycle and configuration of beans. It:

1. **Creates** objects (beans).
2. **Configures** objects (injects dependencies).
3. **Manages** the lifecycle of objects.

### **3.2 Types of IoC Containers**:

| **IoC Container** | **Description** |
| --- | --- |
| **BeanFactory** | Basic container, lazy initializes beans (only when requested). |
| **ApplicationContext** | Advanced container, eagerly initializes beans and provides additional features. |

### **4. How IoC Works in Spring**

1. **Define Dependencies**:
    - Specify dependencies of a class either via **XML**, **annotations**, or **Java-based configuration**.
2. **Register Beans**:
    - Register beans (components) with the IoC container.
3. **IoC Container Handles Dependencies**:
    - The container injects the required dependencies into beans at runtime.

### **5. Dependency Injection and IoC**

**Dependency Injection (DI)** is a specific implementation of IoC where the container provides an object's dependencies instead of the object instantiating them itself.

---

### **Spring IoC (Inversion of Control) Container**

The **Spring IoC Container** is at the core of the Spring Framework and is responsible for managing the lifecycle, configuration, and dependencies of objects (beans). It implements the **Inversion of Control (IoC)** principle, where the control of object creation and dependency management is transferred from the application to the container.

### **1. What is the Spring IoC Container?**

### **Definition**:

The **Spring IoC Container** is a framework that creates and manages the lifecycle of application objects, known as **beans**, and resolves their dependencies based on configuration metadata.

### **Responsibilities**:

1. **Bean Instantiation**: Creates and manages objects defined as beans.
2. **Dependency Injection**: Supplies beans with their required dependencies.
3. **Lifecycle Management**: Handles initialization, configuration, and destruction of beans.

### **2. Types of IoC Containers in Spring**

| **Container Type** | **Description** | **Usage** |
| --- | --- | --- |
| **BeanFactory** | - Basic IoC container. |  |
|  | - Provides lazy initialization (beans are created only when requested). |  |
|  | - Lightweight and suitable for simple applications. | Rarely used today. |
| **ApplicationContext** | - Advanced IoC container. |  |
|  | - Provides additional features like event propagation, AOP, and declarative transactions. |  |
|  | - Beans are eagerly initialized by default (created at startup). | Widely used in Spring. |

### **3. Common Implementations of IoC Container**

| **Implementation** | **Description** |
| --- | --- |
| **`ClassPathXmlApplicationContext`** | Loads configuration from an XML file located in the classpath. |
| **`FileSystemXmlApplicationContext`** | Loads configuration from an XML file located in the file system. |
| **`AnnotationConfigApplicationContext`** | Loads configuration from Java-based configuration using annotations like `@Configuration`. |
| **`WebApplicationContext`** | Specialized version of `ApplicationContext` for web applications. |

---

### **4. Key Components of Spring IoC Container**

### **4.1 Bean**

- A **bean** is an object managed by the IoC container.
- Defined in configuration files (XML or Java) or annotated with stereotypes like `@Component`.

### **4.2 Configuration Metadata**

- Metadata that tells the IoC container how to configure and manage beans.

### **Supported Formats**:

1. **XML-Based Configuration**:
    
    ```xml
    <beans>
        <bean id="car" class="com.example.Car" />
    </beans>
    
    ```
    
2. **Java-Based Configuration**:
    
    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public Car car() {
            return new Car();
        }
    }
    
    ```
    
3. **Annotation-Based Configuration**:
    
    ```java
    @Component
    public class Car {}
    
    ```
    

### **4.3 Dependency Injection (DI)**

- The process of injecting dependencies into beans, supported via:
    1. **Constructor Injection**
    2. **Setter Injection**
    3. **Field Injection**

### **5. Lifecycle of a Bean in IoC Container**

1. **Instantiation**:
    - The container instantiates the bean.
2. **Dependency Injection**:
    - Dependencies are injected into the bean.
3. **Initialization**:
    - Initialization methods (e.g., `@PostConstruct` or custom init methods) are invoked.
4. **Usage**:
    - Bean is used in the application.
5. **Destruction**:
    - Cleanup methods (e.g., `@PreDestroy` or custom destroy methods) are invoked before the container shuts down.

### **6. Example: Using Spring IoC Container**

### **6.1 XML-Based Configuration**

1. **Dependency Class**:
    
    ```java
    public class Engine {
        public void start() {
            System.out.println("Engine started.");
        }
    }
    
    ```
    
2. **Dependent Class**:
    
    ```java
    public class Car {
        private Engine engine;
    
        public void setEngine(Engine engine) {
            this.engine = engine;
        }
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    
3. **XML Configuration**:
    
    ```xml
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
                               http://www.springframework.org/schema/beans/spring-beans.xsd">
        <bean id="engine" class="com.example.Engine" />
        <bean id="car" class="com.example.Car">
            <property name="engine" ref="engine" />
        </bean>
    </beans>
    
    ```
    
4. **Main Application**:
    
    ```java
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;
    
    public class Main {
        public static void main(String[] args) {
            ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
            Car car = context.getBean("car", Car.class);
            car.drive();
        }
    }
    
    ```
    

**Output**:

```
Engine started.
Car is driving.

```

### **6.2 Annotation-Based Configuration**

1. **Dependency Class**:
    
    ```java
    @Component
    public class Engine {
        public void start() {
            System.out.println("Engine started.");
        }
    }
    
    ```
    
2. **Dependent Class**:
    
    ```java
    @Component
    public class Car {
        @Autowired
        private Engine engine;
    
        public void drive() {
            engine.start();
            System.out.println("Car is driving.");
        }
    }
    
    ```
    
3. **Configuration Class**:
    
    ```java
    @Configuration
    @ComponentScan("com.example")
    public class AppConfig {}
    
    ```
    
4. **Main Application**:
    
    ```java
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.annotation.AnnotationConfigApplicationContext;
    
    public class Main {
        public static void main(String[] args) {
            ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            Car car = context.getBean(Car.class);
            car.drive();
        }
    }
    
    ```
    

**Output**:

```
Engine started.
Car is driving.

```

### **7. Features of IoC Container**

| **Feature** | **Description** |
| --- | --- |
| **Bean Lifecycle Management** | Handles the complete lifecycle of beans, from creation to destruction. |
| **Dependency Injection** | Supplies required dependencies to beans. |
| **Event Handling** | Supports event propagation within the container (e.g., `ApplicationEvent`). |
| **Resource Management** | Manages external resources like files or databases. |
| **Integration Support** | Works seamlessly with Spring AOP, transactions, and data access. |

### **8. Summary**

| **Aspect** | **Details** |
| --- | --- |
| **IoC Principle** | Transfers object creation and dependency management to the container. |
| **IoC Container** | Manages beans, their dependencies, and their lifecycle. |
| **Implementations** | BeanFactory (basic) and ApplicationContext (advanced). |
| **Configuration Options** | XML-based, Annotation-based, and Java-based configuration. |
| **Core Benefits** | Loose coupling, enhanced testability, reusability, and modularity. |

---

### **Bean Lifecycle in Spring IoC Container**

The **Bean Lifecycle** in the Spring Framework refers to the series of steps a bean goes through from its creation to its destruction within the Spring IoC container. The lifecycle includes bean instantiation, dependency injection, initialization, and cleanup.

### **1. Steps in the Spring Bean Lifecycle**

| **Step** | **Description** |
| --- | --- |
| **1. Instantiation** | The IoC container instantiates the bean. |
| **2. Dependency Injection** | The container injects dependencies into the bean based on the configuration. |
| **3. Pre-Initialization (`BeanPostProcessor`)** | Custom processing before the bean's initialization phase. |
| **4. Initialization** | Initialization logic is executed (e.g., `@PostConstruct` or custom init method). |
| **5. Post-Initialization (`BeanPostProcessor`)** | Custom processing after the bean's initialization phase. |
| **6. Bean Usage** | The bean is ready to be used by the application. |
| **7. Destruction** | Cleanup logic is executed before the container destroys the bean (e.g., `@PreDestroy` or custom destroy method). |

### **2. Lifecycle Flow**

### **Step-by-Step Explanation**

1. **Instantiation**:
    - The IoC container creates an instance of the bean using its constructor.
2. **Dependency Injection**:
    - Dependencies are injected into the bean (via constructor, setter, or field injection).
3. **BeanPostProcessor - Before Initialization**:
    - If any `BeanPostProcessor` implementations are registered, their `postProcessBeforeInitialization` method is called.
4. **Initialization**:
    - Executes any custom initialization logic, such as methods annotated with `@PostConstruct` or specified in XML/Java configuration.
5. **BeanPostProcessor - After Initialization**:
    - Calls the `postProcessAfterInitialization` method of registered `BeanPostProcessor` implementations.
6. **Bean Usage**:
    - The bean is now ready to be used in the application.
7. **Destruction**:
    - When the container is shutting down, the bean’s cleanup methods are called (e.g., methods annotated with `@PreDestroy` or custom destroy methods).

### **3. Customizing the Bean Lifecycle**

You can customize the lifecycle by implementing specific interfaces or using annotations.

### **3.1 Using `InitializingBean` and `DisposableBean`**

1. **`InitializingBean`**:
    - Implement the `afterPropertiesSet()` method to define initialization logic.
2. **`DisposableBean`**:
    - Implement the `destroy()` method to define cleanup logic.

**Example**:

```java
public class Car implements InitializingBean, DisposableBean {
    @Override
    public void afterPropertiesSet() {
        System.out.println("Car initialized.");
    }

    @Override
    public void destroy() {
        System.out.println("Car destroyed.");
    }
}

```

### **3.2 Using Custom Init and Destroy Methods**

Specify custom methods for initialization and destruction in the configuration.

1. **XML Configuration**:
    
    ```xml
    <bean id="car" class="com.example.Car" init-method="init" destroy-method="cleanup" />
    
    ```
    
2. **Java-Based Configuration**:
    
    ```java
    @Bean(initMethod = "init", destroyMethod = "cleanup")
    public Car car() {
        return new Car();
    }
    
    ```
    
3. **Dependent Class**:
    
    ```java
    public class Car {
        public void init() {
            System.out.println("Car is ready to drive.");
        }
    
        public void cleanup() {
            System.out.println("Car is being destroyed.");
        }
    }
    
    ```
    

### **3.3 Using `@PostConstruct` and `@PreDestroy` Annotations**

1. **Add Annotations**:
    
    ```java
    import javax.annotation.PostConstruct;
    import javax.annotation.PreDestroy;
    
    public class Car {
        @PostConstruct
        public void init() {
            System.out.println("Car is ready to drive.");
        }
    
        @PreDestroy
        public void cleanup() {
            System.out.println("Car is being destroyed.");
        }
    }
    
    ```
    
2. **Configuration Class**:
    
    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public Car car() {
            return new Car();
        }
    }
    
    ```
    

### **3.4 Using `BeanPostProcessor`**

The `BeanPostProcessor` interface allows custom logic before and after the initialization of a bean.

1. **Implementing `BeanPostProcessor`**:
    
    ```java
    import org.springframework.beans.factory.config.BeanPostProcessor;
    
    public class CustomBeanPostProcessor implements BeanPostProcessor {
        @Override
        public Object postProcessBeforeInitialization(Object bean, String beanName) {
            System.out.println("Before Initialization: " + beanName);
            return bean;
        }
    
        @Override
        public Object postProcessAfterInitialization(Object bean, String beanName) {
            System.out.println("After Initialization: " + beanName);
            return bean;
        }
    }
    
    ```
    
2. **Registering the Post Processor**:
    
    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public CustomBeanPostProcessor beanPostProcessor() {
            return new CustomBeanPostProcessor();
        }
    }
    
    ```
    

### **4. Example: Full Bean Lifecycle**

1. **Dependent Class**:
    
    ```java
    public class Car {
        public void init() {
            System.out.println("Car initialized.");
        }
    
        public void cleanup() {
            System.out.println("Car destroyed.");
        }
    }
    
    ```
    
2. **Configuration Class**:
    
    ```java
    @Configuration
    public class AppConfig {
        @Bean(initMethod = "init", destroyMethod = "cleanup")
        public Car car() {
            return new Car();
        }
    }
    
    ```
    
3. **Main Application**:
    
    ```java
    import org.springframework.context.annotation.AnnotationConfigApplicationContext;
    
    public class Main {
        public static void main(String[] args) {
            AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
            Car car = context.getBean(Car.class);
            context.close();
        }
    }
    
    ```
    
4. **Output**:
    
    ```
    Car initialized.
    Car destroyed.
    
    ```
    

### **5. Summary of Bean Lifecycle Customization Methods**

| **Customization Method** | **Initialization** | **Destruction** |
| --- | --- | --- |
| **`InitializingBean`/`DisposableBean`** | `afterPropertiesSet()` | `destroy()` |
| **Custom Methods** | `init-method` | `destroy-method` |
| **Annotations** | `@PostConstruct` | `@PreDestroy` |
| **BeanPostProcessor** | `postProcessBeforeInitialization()` | `postProcessAfterInitialization()` |

### **Key Takeaways**

- The Spring IoC Container fully manages the lifecycle of beans.
- The lifecycle includes instantiation, dependency injection, initialization, usage, and destruction.
- Developers can customize the lifecycle using interfaces, custom methods, annotations, or `BeanPostProcessor`.
- **Modern Approach**: Use `@PostConstruct` and `@PreDestroy` for simplicity.

---

### **Scopes of a Bean in Spring Framework**

The **scope** of a bean in Spring defines the lifecycle and visibility of the bean instances within the application. It determines:

1. How many instances of the bean will be created.
2. How the instances are shared.

### **1. Default Bean Scope**

The default scope in Spring is **`singleton`**, meaning one instance of the bean will be created and shared throughout the application.

### **2. Types of Bean Scopes**

Spring provides five primary bean scopes:

| **Scope** | **Description** | **Usage** |
| --- | --- | --- |
| **`singleton`** | A single instance of the bean is created and shared across the entire application context. | Default and most common. |
| **`prototype`** | A new instance of the bean is created each time it is requested. | For stateful beans. |
| **`request`** | A single instance is created for each HTTP request (Web applications only). | Web-specific. |
| **`session`** | A single instance is created for each HTTP session (Web applications only). | Web-specific. |
| **`application`** | A single instance is created for the entire lifecycle of a web application (shared across sessions). | Web-specific. |

### **3. Setting Bean Scope**

### **3.1 Annotation-Based Configuration**

Use the `@Scope` annotation along with `@Component` or `@Bean`.

1. **For Singleton Scope (Default)**:
    
    ```java
    @Component
    public class SingletonBean {}
    
    ```
    
2. **For Prototype Scope**:
    
    ```java
    @Component
    @Scope("prototype")
    public class PrototypeBean {}
    
    ```
    
3. **Java Configuration with `@Bean`**:
    
    ```java
    @Configuration
    public class AppConfig {
        @Bean
        @Scope("prototype")
        public PrototypeBean prototypeBean() {
            return new PrototypeBean();
        }
    }
    
    ```
    

### **4. Scope Details**

### **4.1 Singleton Scope**

- **Behavior**:
    - Only one instance is created and shared for all requests.
- **Use Case**:
    - Stateless beans or services shared across the application.

**Example**:

```java
@Component
public class SingletonBean {
    public SingletonBean() {
        System.out.println("SingletonBean instance created");
    }
}

```

**Output** (on multiple requests):

```
SingletonBean instance created

```

### **4.2 Prototype Scope**

- **Behavior**:
    - A new instance is created every time the bean is requested.
- **Use Case**:
    - Stateful beans or objects requiring unique instances.

**Example**:

```java
@Component
@Scope("prototype")
public class PrototypeBean {
    public PrototypeBean() {
        System.out.println("PrototypeBean instance created");
    }
}

```

**Output** (on multiple requests):

```
PrototypeBean instance created
PrototypeBean instance created
PrototypeBean instance created

```

### **4.3 Request Scope**

- **Behavior**:
    - A new instance is created for each HTTP request.
- **Use Case**:
    - Web applications, where the bean is tied to the request lifecycle.

**Example**:

```java
@Component
@Scope("request")
public class RequestBean {
    public RequestBean() {
        System.out.println("RequestBean instance created");
    }
}

```

**Output** (on multiple requests):

```
RequestBean instance created (for each HTTP request)

```

### **4.4 Session Scope**

- **Behavior**:
    - A new instance is created for each HTTP session.
- **Use Case**:
    - Storing user-specific data for the duration of a session.

**Example**:

```java
@Component
@Scope("session")
public class SessionBean {
    public SessionBean() {
        System.out.println("SessionBean instance created");
    }
}

```

### **4.5 Application Scope**

- **Behavior**:
    - A single instance is created and shared across the entire web application.
- **Use Case**:
    - Application-wide shared resources.

**Example**:

```java
@Component
@Scope("application")
public class ApplicationBean {
    public ApplicationBean() {
        System.out.println("ApplicationBean instance created");
    }
}

```

### **5. Accessing Scoped Beans**

1. **For Prototype Scope**:
    - `@Scope("prototype")` beans are not managed after creation; their lifecycle is manual.
    - Use `ObjectFactory` or `Provider` for prototype beans in singleton beans.

**Example with `ObjectFactory`**:

```java
@Component
public class SingletonService {
    @Autowired
    private ObjectFactory<PrototypeBean> prototypeBeanFactory;

    public PrototypeBean getPrototypeBean() {
        return prototypeBeanFactory.getObject();
    }
}

```

### **6. Summary of Scopes**

| **Scope** | **Lifecycle** | **Visibility** | **Use Case** |
| --- | --- | --- | --- |
| **Singleton** | Entire application context | Shared across all requests | Stateless, shared beans |
| **Prototype** | Each request | Unique per request | Stateful, non-shared objects |
| **Request** | Each HTTP request | Unique per request | Web applications |
| **Session** | Each HTTP session | Unique per session | User-specific data |
| **Application** | Entire web application | Shared across all sessions | Application-wide shared beans |

### **7. Choosing the Right Scope**

| **Requirement** | **Recommended Scope** |
| --- | --- |
| Shared service, stateless | `singleton` |
| Unique instance per request or use | `prototype` |
| Tied to an HTTP request | `request` |
| Tied to a user session | `session` |
| Shared across the entire application lifecycle | `application` |

---

### **Bean Definition and Instantiation in Spring Framework**

In the Spring Framework, **bean definition** refers to how you define the configuration and properties of a bean in the IoC container, while **bean instantiation** refers to how the container creates and initializes those beans.

### **1. What is a Bean?**

A **bean** is an object managed by the Spring IoC container. It is a central concept in Spring and represents any object that is instantiated, configured, and managed by the container.

### **2. Bean Definition**

The configuration metadata (XML, Java, or annotations) defines the following:

1. **Bean ID/Name**: A unique identifier for the bean in the container.
2. **Class**: The fully qualified class name of the bean.
3. **Scope**: Defines the lifecycle of the bean (`singleton`, `prototype`, etc.).
4. **Dependencies**: Specifies the dependencies for the bean.
5. **Custom Initialization and Destruction**: Defines methods for custom initialization and cleanup.

### **3. Defining Beans in Spring**

### **3.1 XML-Based Configuration**

In **XML**, beans are defined using the `<bean>` tag.

**Example**:

```xml
<beans>
    <bean id="car" class="com.example.Car">
        <property name="engine" ref="engine" />
    </bean>

    <bean id="engine" class="com.example.Engine" />
</beans>

```

### **3.2 Java-Based Configuration**

In **Java**, beans are defined using `@Configuration` and `@Bean` annotations.

**Example**:

```java
@Configuration
public class AppConfig {
    @Bean
    public Engine engine() {
        return new Engine();
    }

    @Bean
    public Car car() {
        return new Car(engine());
    }
}

```

### **3.3 Annotation-Based Configuration**

In **Annotation-Based** configuration, beans are defined using stereotype annotations like `@Component`.

**Example**:

```java
@Component
public class Engine {}

@Component
public class Car {
    @Autowired
    private Engine engine;
}

```

**Enable Component Scanning**:

```java
@Configuration
@ComponentScan("com.example")
public class AppConfig {}

```

### **4. Bean Instantiation**

Bean instantiation refers to how the Spring IoC container creates the bean instance. Spring provides several methods for instantiation:

### **4.1 Default Constructor**

Spring uses the default constructor to instantiate the bean.

**Class**:

```java
public class Engine {
    public Engine() {
        System.out.println("Engine instance created.");
    }
}

```

**Configuration**:

```xml
<bean id="engine" class="com.example.Engine" />

```

**Output**:

```
Engine instance created.

```

### **4.2 Constructor with Arguments**

Spring can call a parameterized constructor and inject dependencies during instantiation.

**Class**:

```java
public class Car {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }
}

```

**XML Configuration**:

```xml
<bean id="car" class="com.example.Car">
    <constructor-arg ref="engine" />
</bean>
<bean id="engine" class="com.example.Engine" />

```

**Java Configuration**:

```java
@Bean
public Car car() {
    return new Car(engine());
}

```

### **4.3 Setter Injection**

Spring uses setter methods to inject dependencies.

**Class**:

```java
public class Car {
    private Engine engine;

    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}

```

**XML Configuration**:

```xml
<bean id="car" class="com.example.Car">
    <property name="engine" ref="engine" />
</bean>
<bean id="engine" class="com.example.Engine" />

```

### **4.4 Factory Method**

A factory method can be used to create beans.

**Static Factory Method**:

```java
public class EngineFactory {
    public static Engine createEngine() {
        return new Engine();
    }
}

```

**XML Configuration**:

```xml
<bean id="engine" class="com.example.EngineFactory" factory-method="createEngine" />

```

### **4.5 Factory Bean**

A custom factory bean can create complex beans.

**Factory Bean Implementation**:

```java
public class CustomFactoryBean implements FactoryBean<Engine> {
    @Override
    public Engine getObject() throws Exception {
        return new Engine();
    }

    @Override
    public Class<?> getObjectType() {
        return Engine.class;
    }
}

```

**Configuration**:

```xml
<bean id="engine" class="com.example.CustomFactoryBean" />

```

### **5. Bean Lifecycle During Instantiation**

1. **Bean Definition Loading**:
    - The container reads the bean definitions from the configuration metadata.
2. **Bean Instantiation**:
    - The container creates instances of beans using the defined methods.
3. **Dependency Injection**:
    - Dependencies are injected into the bean (via constructor, setter, or field).
4. **Initialization**:
    - Custom initialization methods are called if defined.
5. **Ready for Use**:
    - The bean is now fully initialized and ready to be used.

### **7. Summary of Bean Definition and Instantiation**

| **Aspect** | **Description** |
| --- | --- |
| **Definition Methods** | XML, Java-based (`@Configuration`), and annotation-based (`@Component`). |
| **Instantiation Methods** | Default constructor, parameterized constructor, setter methods, factory methods. |
| **Dependency Injection** | Inject dependencies using constructor, setter, or field injection. |
| **Customization** | Use factory beans or custom factory methods for complex object creation. |

---

### **Module: Annotation-Based Configuration**

---

### **Annotation-Based Configuration in Spring Framework**

**Annotation-Based Configuration** in Spring uses Java annotations to define and manage beans, eliminating the need for verbose XML configurations. This approach simplifies development by leveraging annotations directly in the codebase for dependency injection, bean management, and configuration.

### **1. Key Annotations for Configuration**

| **Annotation** | **Purpose** |
| --- | --- |
| `@Configuration` | Indicates a class contains bean definitions. |
| `@Bean` | Declares a bean definition in a `@Configuration` class. |
| `@Component` | Marks a class as a Spring-managed bean. |
| `@Service` | Specialized `@Component` for service-layer beans. |
| `@Repository` | Specialized `@Component` for persistence-layer beans. |
| `@Controller` | Specialized `@Component` for Spring MVC controllers. |
| `@Autowired` | Injects a bean into a dependent bean. |
| `@Qualifier` | Specifies which bean to inject when multiple candidates are available. |
| `@ComponentScan` | Configures component scanning to detect `@Component`-annotated classes automatically. |

### **2. Enabling Annotation-Based Configuration**

Annotation-based configuration requires enabling **component scanning** in the Spring IoC container.

### **2.1 Enabling in XML Configuration**

```xml
<context:component-scan base-package="com.example" />

```

### **2.2 Enabling in Java Configuration**

```java
@Configuration
@ComponentScan("com.example")
public class AppConfig {}

```

### **3. Defining Beans with Annotations**

### **3.1 Using `@Component`**

The `@Component` annotation marks a class as a Spring-managed bean. It can be used for any general-purpose bean.

**Example**:

```java
@Component
public class Engine {
    public void start() {
        System.out.println("Engine started.");
    }
}

```

### **3.2 Using `@Configuration` and `@Bean`**

The `@Configuration` annotation indicates a class that declares one or more `@Bean`-annotated methods to define beans.

**Example**:

```java
@Configuration
public class AppConfig {
    @Bean
    public Engine engine() {
        return new Engine();
    }

    @Bean
    public Car car() {
        return new Car(engine());
    }
}

```

### **4. Dependency Injection with Annotations**

### **4.1 Using `@Autowired`**

The `@Autowired` annotation injects a dependency automatically.

**Example**:

```java
@Component
public class Car {
    @Autowired
    private Engine engine;

    public void drive() {
        engine.start();
        System.out.println("Car is driving.");
    }
}

```

### **5. Advantages of Annotation-Based Configuration**

| **Advantage** | **Description** |
| --- | --- |
| **Reduced Boilerplate Code** | Eliminates verbose XML configurations. |
| **Type-Safety** | Refactoring is easier as annotations are tied to code. |
| **Improved Readability** | Configurations are colocated with the code they affect. |
| **Fine-Grained Control** | Annotations allow fine control over bean creation and dependency injection. |

### **6. Disadvantages of Annotation-Based Configuration**

| **Disadvantage** | **Description** |
| --- | --- |
| **Harder to Modify** | Changing configurations requires modifying the source code. |
| **Limited Flexibility** | XML-based configuration is more flexible in some dynamic scenarios. |
| **Mixed Configurations** | Large projects often require a mix of annotation-based and XML-based configurations. |

---

### **Component Scanning in Spring Framework**

**Component Scanning** is a mechanism in Spring Framework that automatically detects and registers beans (classes annotated with stereotype annotations) in the **Spring IoC Container**. This eliminates the need for explicit bean definitions in XML or Java-based configurations.

### **1. How Component Scanning Works**

Spring scans specified packages for classes annotated with **stereotype annotations** like `@Component`, `@Service`, `@Repository`, and `@Controller`. These classes are automatically registered as beans in the IoC container.

### **2. Enabling Component Scanning**

You enable component scanning using the following approaches:

### **2.1 XML-Based Configuration**

Use the `<context:component-scan>` tag in the XML configuration.

```xml
<context:component-scan base-package="com.example" />

```

### **2.2 Java-Based Configuration**

Use the `@ComponentScan` annotation in a `@Configuration` class.

```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {}

```

### **2.3 Annotation-Based Configuration**

Annotations like `@SpringBootApplication` or `@EnableWebMvc` include implicit `@ComponentScan`, scanning the current package and its sub-packages.

**Example in Spring Boot**:

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}

```

- This scans the package where `Application` resides and all its sub-packages.

### **3. Stereotype Annotations for Component Scanning**

Spring provides the following annotations to mark classes for component scanning:

| **Annotation** | **Purpose** |
| --- | --- |
| `@Component` | General-purpose annotation to mark a class as a Spring-managed bean. |
| `@Service` | Specialized for service-layer classes. |
| `@Repository` | Specialized for persistence-layer classes, typically interacting with the database. |
| `@Controller` | Specialized for Spring MVC controller classes that handle HTTP requests. |

### **4. Customizing Component Scanning**

### **4.1 Specifying Base Packages**

You can specify multiple packages for scanning.

```java
@ComponentScan(basePackages = {"com.example.services", "com.example.repositories"})

```

### **4.2 Excluding Classes**

Use the `excludeFilters` attribute to exclude specific classes or annotations.

```java
@ComponentScan(
    basePackages = "com.example",
    excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = {Deprecated.class})
)

```

### **4.3 Including Specific Classes**

Use the `includeFilters` attribute to include specific classes.

```java
@ComponentScan(
    basePackages = "com.example",
    includeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = {MyCustomAnnotation.class})
)

```

### **4.4 Custom Filters**

You can customize scanning using `FilterType` options:

- **`ANNOTATION`**: Filter by annotations.
- **`ASSIGNABLE_TYPE`**: Filter by class type.
- **`ASPECTJ`**: Filter by AspectJ expressions.
- **`REGEX`**: Filter by regular expressions.
- **`CUSTOM`**: Use a custom filter implementation.

**Example**:

```java
@ComponentScan(
    basePackages = "com.example",
    includeFilters = @ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, classes = MySpecificClass.class)
)

```

### **5. Example: Component Scanning in Action**

### **5.1 Annotated Classes**

```java
@Component
public class Engine {
    public void start() {
        System.out.println("Engine started.");
    }
}

@Service
public class CarService {
    @Autowired
    private Engine engine;

    public void drive() {
        engine.start();
        System.out.println("Car is driving.");
    }
}

```

### **5.2 Configuration Class**

```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {}

```

### **5.3 Main Application**

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        CarService carService = context.getBean(CarService.class);
        carService.drive();
    }
}

```

### **Output**:

```
Engine started.
Car is driving.

```

### **6. Advantages of Component Scanning**

| **Advantage** | **Description** |
| --- | --- |
| **Reduces Boilerplate Code** | No need to explicitly define beans in XML or Java configuration. |
| **Improves Maintainability** | Scans and registers beans automatically when new classes are added. |
| **Promotes Convention Over Configuration** | Encourages structured and consistent package organization. |

### **7. Best Practices**

1. **Organize Packages by Layers**:
    - Use separate packages for controllers, services, and repositories:
        
        ```
        com.example.controller
        com.example.service
        com.example.repository
        
        ```
        
2. **Use Specific Base Packages**:
    - Limit component scanning to specific packages to avoid scanning irrelevant classes.
3. **Avoid Over-Scanning**:
    - Exclude unnecessary classes or annotations using filters.
4. **Use Stereotype Annotations**:
    - Prefer `@Service`, `@Repository`, and `@Controller` over `@Component` for better clarity.

### **8. Component Scanning vs. Explicit Bean Definition**

| **Aspect** | **Component Scanning** | **Explicit Bean Definition** |
| --- | --- | --- |
| **Configuration Overhead** | Minimal (uses annotations). | Requires explicit bean definitions in XML/Java. |
| **Flexibility** | Automatically registers classes marked with annotations. | Offers fine-grained control over bean creation. |
| **Readability** | Annotations colocated with the code enhance readability. | Configuration may be separated from the codebase. |

---

### **Stereotype Annotations in Spring Framework**

Spring provides several **stereotype annotations** to define and classify different types of components in a Spring application. These annotations help organize the application structure into layers such as presentation, business, and persistence.

### **1. Common Stereotype Annotations**

| **Annotation** | **Purpose** |
| --- | --- |
| `@Component` | General-purpose annotation for any Spring-managed component. |
| `@Service` | Specialized annotation for service-layer components. |
| `@Repository` | Specialized annotation for persistence-layer components, such as DAOs. |
| `@Controller` | Specialized annotation for presentation-layer components, typically in Spring MVC. |

### **2. Stereotype Annotations Explained**

### **2.1 `@Component`**

- **Purpose**: Marks a class as a generic Spring-managed component.
- **Usage**: Suitable for classes that don’t fit into a specific layer (business logic, utility classes, etc.).

**Example**:

```java
@Component
public class NotificationService {
    public void sendNotification(String message) {
        System.out.println("Notification sent: " + message);
    }
}

```

### **2.2 `@Service`**

- **Purpose**: A specialization of `@Component`, indicating that the class contains **business logic** or service-layer logic.
- **Usage**: Use for service-layer components where business operations or orchestration occurs.

**Example**:

```java
@Service
public class OrderService {
    public void processOrder(String orderId) {
        System.out.println("Processing order: " + orderId);
    }
}

```

### **2.3 `@Repository`**

- **Purpose**: A specialization of `@Component`, indicating that the class interacts with the **persistence layer** (e.g., DAOs or database repositories).
- **Additional Functionality**:
    - Translates database exceptions (e.g., `SQLException`) into Spring's `DataAccessException`.
- **Usage**: Use for database access logic (CRUD operations).

**Example**:

```java
@Repository
public class ProductRepository {
    public void saveProduct(String productName) {
        System.out.println("Product saved: " + productName);
    }
}

```

### **2.4 `@Controller`**

- **Purpose**: A specialization of `@Component`, marking a class as a **controller** in Spring MVC for handling HTTP requests.
- **Usage**: Use for presentation-layer components that process web requests and return responses.

**Example**:

```java
@Controller
public class ProductController {
    @Autowired
    private ProductRepository productRepository;

    public void createProduct(String productName) {
        productRepository.saveProduct(productName);
        System.out.println("Product created: " + productName);
    }
}

```

### **3. Lifecycle of Components with Stereotype Annotations**

1. **Scanning**:
    - Classes annotated with `@Component`, `@Service`, `@Repository`, or `@Controller` are detected during **component scanning**.
2. **Registration**:
    - The Spring IoC container registers these classes as beans.
3. **Dependency Injection**:
    - The container resolves and injects dependencies into these beans.

### **4. Enabling Stereotype Annotations**

To enable the detection of stereotype annotations, you must enable **component scanning**.

### **4.1 XML-Based Configuration**

```xml
<context:component-scan base-package="com.example" />

```

### **4.2 Java-Based Configuration**

```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {}

```

### **5. Dependency Injection in Stereotype Components**

### **Using `@Autowired`**:

You can inject dependencies into classes annotated with stereotype annotations using `@Autowired`.

**Example**:

```java
@Service
public class OrderService {
    @Autowired
    private NotificationService notificationService;

    public void processOrder(String orderId) {
        notificationService.sendNotification("Order processed: " + orderId);
    }
}

```

### **6. Differences Between Stereotype Annotations**

| **Annotation** | **Purpose** | **Primary Use Case** |
| --- | --- | --- |
| `@Component` | General-purpose bean annotation. | Utility classes or generic components. |
| `@Service` | Represents the service layer. | Business logic or service orchestration. |
| `@Repository` | Represents the persistence layer. | Database access and data persistence. |
| `@Controller` | Represents the presentation layer. | Web controllers for handling HTTP requests. |

---

### **7. Advantages of Using Stereotype Annotations**

| **Advantage** | **Description** |
| --- | --- |
| **Clear Separation of Layers** | Defines specific layers of the application (e.g., service, persistence). |
| **Component Scanning** | Automatically detects and registers beans, reducing boilerplate code. |
| **Improved Readability** | Improves code readability by categorizing classes based on their purpose. |

---

### **8. Best Practices**

1. **Use Stereotype Annotations Judiciously**:
    - Apply annotations that match the role of the class (`@Service` for services, `@Repository` for DAOs, etc.).
2. **Avoid Overuse of `@Component`**:
    - Use specialized annotations (`@Service`, `@Repository`, `@Controller`) for better clarity and structure.
3. **Organize by Layers**:
    - Keep components in separate packages based on their layer (e.g., `controller`, `service`, `repository`).

---