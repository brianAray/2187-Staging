# **System Design Basics**

When designing software systems, it’s essential to apply object-oriented programming (OOP) principles to structure your code effectively. This ensures scalability, maintainability, and reusability.

---

## **Basics of System Design**

---

### **1. Designing Classes**

Designing a class involves identifying the properties and behaviors of an entity and modeling them as fields and methods, respectively.

#### **Example: Designing a `User` Class**
```java
public class User {
    // Fields (attributes)
    private int id;
    private String name;
    private String email;

    // Constructor
    public User(int id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }

    // Getter and Setter methods
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    // Behavior (methods)
    public void sendEmail(String message) {
        System.out.println("Email sent to " + email + ": " + message);
    }
}
```

---

#### **2. Relationships**

Relationships define how different classes interact with one another. Common relationships in OOP are:

- **Association**: A "uses" relationship.
- **Aggregation**: A "has-a" relationship where one class contains another as part of its state.
- **Composition**: A stronger form of aggregation where the contained object cannot exist independently of its parent.
- **Inheritance**: An "is-a" relationship.

---

#### **Example: Association**
```java
public class Order {
    private User user; // Association (uses a User object)

    public Order(User user) {
        this.user = user;
    }

    public void placeOrder() {
        System.out.println("Order placed by " + user.getName());
    }
}

public class AssociationExample {
    public static void main(String[] args) {
        User user = new User(1, "Alice", "alice@example.com");
        Order order = new Order(user);
        order.placeOrder();
    }
}
```

---

#### **Example: Aggregation**
```java
import java.util.List;

public class Department {
    private List<User> employees; // Aggregation (has-a relationship)

    public Department(List<User> employees) {
        this.employees = employees;
    }

    public void printEmployeeDetails() {
        for (User user : employees) {
            System.out.println("Employee: " + user.getName());
        }
    }
}
```

---

#### **Example: Composition**
```java
public class Engine {
    public void start() {
        System.out.println("Engine started.");
    }
}

public class Car {
    private Engine engine; // Composition (engine cannot exist without car)

    public Car() {
        this.engine = new Engine();
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving.");
    }
}

public class CompositionExample {
    public static void main(String[] args) {
        Car car = new Car();
        car.drive();
    }
}
```

---

#### **Example: Inheritance**
```java
public class Animal {
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

public class Dog extends Animal { // Inheritance (Dog is an Animal)
    public void bark() {
        System.out.println("The dog barks.");
    }
}

public class InheritanceExample {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // Inherited behavior
        dog.bark(); // Specific behavior
    }
}
```

---

### **3. Common OOP Principles**

---

#### **Encapsulation**
- **Definition**: Bundling data and methods that operate on the data within a single unit (class).
- **Key Idea**: Protect internal states by making fields private and providing controlled access via getters/setters.
  
**Example**:
```java
public class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
}
```

---

#### **Abstraction**
- **Definition**: Hiding implementation details and exposing only the functionality.
- **Key Idea**: Use abstract classes and interfaces to define common behavior.

**Example**:
```java
public abstract class Shape {
    public abstract double getArea(); // Abstract method
}

public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}

public class AbstractionExample {
    public static void main(String[] args) {
        Shape circle = new Circle(5);
        System.out.println("Circle Area: " + circle.getArea());
    }
}
```

---

#### **Polymorphism**
- **Definition**: The ability to process objects differently based on their data type or class.
- **Key Idea**: Achieved through method overriding and method overloading.

**Example**:
```java
public class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Animal myAnimal = new Cat(); // Polymorphism: Animal reference, Cat object
        myAnimal.makeSound(); // Output: Meow
    }
}
```

---

#### **Inheritance**
- **Definition**: Enables new classes to derive from existing ones.
- **Key Idea**: Reuse functionality and establish a natural hierarchy.

**Example**:
See the inheritance example above.

---

#### **SOLID Principles**
1. **S**ingle Responsibility Principle: Each class should have only one responsibility.
2. **O**pen/Closed Principle: Classes should be open for extension but closed for modification.
3. **L**iskov Substitution Principle: Subtypes must be substitutable for their base types.
4. **I**nterface Segregation Principle: Prefer small, specific interfaces over large, general ones.
5. **D**ependency Inversion Principle: Depend on abstractions, not concrete implementations.

---