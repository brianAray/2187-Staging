# **Java Fullstack Development Review Guide**

### **Java Orientation**

1. **What is Java?**
    
    Java is a versatile, object-oriented, and platform-independent programming language designed for building robust, secure, and high-performance applications. Developed by **Sun Microsystems** (now owned by Oracle Corporation) in 1995, Java has become one of the most popular programming languages, widely used in various domains, including web development, mobile apps, enterprise systems, embedded systems, and more.
    
    ### Key Features of Java:
    
    1. **Platform-Independent (Write Once, Run Anywhere)**:
        
        Java applications are compiled into bytecode, which can run on any device with a Java Virtual Machine (JVM).
        
    2. **Object-Oriented**:
        
        Java follows the object-oriented programming (OOP) paradigm, which promotes modularity and reusability through classes and objects.
        
    3. **Robust**:
        
        Java has strong memory management, exception handling, and type-checking features, making it less prone to crashes.
        
    4. **Secure**:
        
        Java provides a secure runtime environment with features like a security manager, classloader, and runtime checks to prevent unauthorized code execution.
        
    5. **Multithreaded**:
        
        Java supports multithreading, allowing concurrent execution of multiple threads to enhance application performance.
        
    6. **High Performance**:
        
        Java uses Just-In-Time (JIT) compilers to optimize bytecode into native machine code during runtime for faster execution.
        
    7. **Distributed**:
        
        Java has built-in support for developing distributed applications through technologies like RMI (Remote Method Invocation) and CORBA.
        
    8. **Dynamic and Extensible**:
        
        Java supports dynamic linking and loading of classes, allowing applications to adapt and extend functionality.
        
2. **JVM, JRE, JDK**
    
    ### 1. **Java Virtual Machine (JVM)**
    
    The **JVM** is the engine that runs Java bytecode. It is platform-specific and provides an environment for Java programs to execute.
    
    ### Key Responsibilities:
    
    - **Bytecode Execution**: The JVM interprets or compiles Java bytecode into machine code for the host operating system.
    - **Memory Management**: Handles allocation and deallocation of memory through Garbage Collection (GC).
    - **Platform Independence**: Allows Java programs to run on any machine with a JVM installed.
    
    ### Components of JVM:
    
    - **Classloader**: Loads class files into memory.
    - **Bytecode Verifier**: Ensures bytecode integrity and security.
    - **Execution Engine**: Converts bytecode to native code using an interpreter or Just-In-Time (JIT) compiler.
    - **Java Native Interface (JNI)**: Enables interaction with native libraries.
    
    ---
    
    ### 2. **Java Runtime Environment (JRE)**
    
    The **JRE** is a software package that provides the necessary libraries and components to run Java applications. It includes the JVM, but not development tools like a compiler.
    
    ### Key Responsibilities:
    
    - Provides the **runtime libraries** (like Java APIs) required for running Java programs.
    - Contains the **JVM** to execute bytecode.
    - Does **not include tools for development**, such as `javac`.
    
    ### Usage:
    
    - Ideal for end-users who only want to run Java applications and do not need to develop them.
    
    ---
    
    ### 3. **Java Development Kit (JDK)**
    
    The **JDK** is a full-fledged software development environment for Java. It includes the JRE along with tools necessary for Java development.
    
    ### Key Components:
    
    - **JRE**: To run Java applications.
    - **Compiler (`javac`)**: Translates Java source code into bytecode.
    - **Debugger (`jdb`)**: Helps in debugging Java programs.
    - **JavaDoc**: Generates documentation from source code comments.
    - **Additional Tools**: Tools like `jconsole`, `jstack`, and `jps` for performance and debugging.
    
    ### Usage:
    
    - Required for Java developers to write, compile, debug, and test Java programs.
    
    ---
    
    ### Comparison Table
    
    | Feature | **JVM** | **JRE** | **JDK** |
    | --- | --- | --- | --- |
    | **Purpose** | Executes bytecode | Runs Java programs | Develops and runs Java programs |
    | **Includes** | Execution engine, GC, etc. | JVM + Libraries | JRE + Compiler + Tools |
    | **Used By** | End-users and developers | End-users and developers | Developers |
    | **Tools Included** | None | None | Compiler, Debugger, JavaDoc |
    
    ---
    
    ### Analogy:
    
    - **JVM**: The engine of a car that makes it move.
    - **JRE**: The car itself, ready to drive but not customizable.
    - **JDK**: The car factory, enabling you to build and modify cars.

---

### **Java Basics**

1. **Primitive Data Types**
    
    Java provides **8 primitive data types** that serve as the building blocks for data manipulation. These types are not objects and are stored directly in memory for high performance.
    
    ---
    
    ### **List of Primitive Data Types**
    
    | **Type** | **Size** | **Default Value** | **Range** | **Description** |
    | --- | --- | --- | --- | --- |
    | **byte** | 1 byte (8 bits) | `0` | -128 to 127 | Smallest integer type, useful for memory saving. |
    | **short** | 2 bytes (16 bits) | `0` | -32,768 to 32,767 | Larger integer, used for compact storage. |
    | **int** | 4 bytes (32 bits) | `0` | -2³¹ to 2³¹-1 | Default type for integers. |
    | **long** | 8 bytes (64 bits) | `0L` | -2⁶³ to 2⁶³-1 | Large integer values, appended with `L`. |
    | **float** | 4 bytes (32 bits) | `0.0f` | ~±3.40282347E+38F | Single-precision floating-point numbers. |
    | **double** | 8 bytes (64 bits) | `0.0d` | ~±1.79769313486231570E+308 | Double-precision floating-point numbers. |
    | **char** | 2 bytes (16 bits) | `'\u0000'` | 0 to 65,535 (unsigned) | Represents a single 16-bit Unicode character. |
    | **boolean** | 1 bit (not precise) | `false` | `true` or `false` | Represents logical values. |
    
    ---
    
2. **Mathematical Operators**
    
    ### **1. Arithmetic Operators**
    
    Used for basic mathematical operations.
    
    | **Operator** | **Description** | **Example** | **Result** |
    | --- | --- | --- | --- |
    | `+` | Addition | `5 + 3` | `8` |
    | `-` | Subtraction | `5 - 3` | `2` |
    | `*` | Multiplication | `5 * 3` | `15` |
    | `/` | Division | `5 / 2` | `2` (integer division) |
    | `%` | Modulus (Remainder) | `5 % 2` | `1` |
    
    **Note**: For division, if both operands are integers, the result will also be an integer. Use floating-point numbers for precise division.
    
    Example:
    
    ```java
    int a = 10, b = 3;
    System.out.println(a / b); // Output: 3
    System.out.println(a / (double)b); // Output: 3.333...
    
    ```
    
    ---
    
    ### **2. Assignment Operators**
    
    Used to assign values to variables.
    
    | **Operator** | **Description** | **Example** | **Result** |
    | --- | --- | --- | --- |
    | `=` | Assign | `x = 5` | `x = 5` |
    | `+=` | Add and Assign | `x += 3` | `x = x + 3` |
    | `-=` | Subtract and Assign | `x -= 3` | `x = x - 3` |
    | `*=` | Multiply and Assign | `x *= 3` | `x = x * 3` |
    | `/=` | Divide and Assign | `x /= 3` | `x = x / 3` |
    | `%=` | Modulus and Assign | `x %= 3` | `x = x % 3` |
    
    ---
    
    ### **3. Comparison (Relational) Operators**
    
    Used to compare two values and return a boolean result (`true` or `false`).
    
    | **Operator** | **Description** | **Example** | **Result** |
    | --- | --- | --- | --- |
    | `==` | Equal to | `5 == 3` | `false` |
    | `!=` | Not equal to | `5 != 3` | `true` |
    | `>` | Greater than | `5 > 3` | `true` |
    | `<` | Less than | `5 < 3` | `false` |
    | `>=` | Greater than or equal to | `5 >= 3` | `true` |
    | `<=` | Less than or equal to | `5 <= 3` | `false` |
    
    ---
    
    ### **4. Increment and Decrement Operators**
    
    Used to increase or decrease a value by 1.
    
    | **Operator** | **Description** | **Example** | **Result** |
    | --- | --- | --- | --- |
    | `++` | Increment by 1 | `x++` | Post-increment |
    | `--` | Decrement by 1 | `x--` | Post-decrement |
    
    **Note**:
    
    - **Postfix (`x++`)**: Returns the value first, then increments.
    - **Prefix (`++x`)**: Increments first, then returns the value.
    
    Example:
    
    ```java
    int x = 5;
    System.out.println(x++); // Output: 5
    System.out.println(x);   // Output: 6
    System.out.println(++x); // Output: 7
    
    ```
    
    ---
    
    ### **5. Bitwise Operators**
    
    Operate directly on bits (binary representations).
    
    | **Operator** | **Description** | **Example** | **Result** |
    | --- | --- | --- | --- |
    | `&` | Bitwise AND | `5 & 3` | `1` |
    | ` | ` | Bitwise OR | `5 |
    | `^` | Bitwise XOR | `5 ^ 3` | `6` |
    | `~` | Bitwise Complement | `~5` | `-6` |
    | `<<` | Left Shift | `5 << 2` | `20` |
    | `>>` | Right Shift | `5 >> 2` | `1` |
    | `>>>` | Unsigned Right Shift | `-5 >>> 2` | A large number |
    
    ---
    
    ### **6. Logical Operators**
    
    Used for combining boolean expressions.
    
    | **Operator** | **Description** | **Example** | **Result** |
    | --- | --- | --- | --- |
    | `&&` | Logical AND | `true && false` | `false` |
    | ` |  | ` | Logical OR |
    | `!` | Logical NOT | `!true` | `false` |
    
    ---
    
3. **Using Scanner**
    
    ### **Steps to Use Scanner**
    
    1. **Import the Scanner Class**:
        
        ```java
        import java.util.Scanner;
        
        ```
        
    2. **Create a Scanner Object**:
        
        ```java
        Scanner scanner = new Scanner(System.in);
        
        ```
        
    3. **Read Input**:
    Use the appropriate method to read input depending on the data type (e.g., `nextInt()`, `nextDouble()`, `nextLine()`).
    4. **Close the Scanner**:
    Always close the Scanner to release the resources:
        
        ```java
        scanner.close();
        
        ```
        
    
    ---
    
    ### **Common Methods in Scanner**
    
    | **Method** | **Description** | **Example** |
    | --- | --- | --- |
    | `nextLine()` | Reads an entire line of input (including spaces). | `String line = scanner.nextLine();` |
    | `next()` | Reads a single word (up to whitespace). | `String word = scanner.next();` |
    | `nextInt()` | Reads an integer. | `int number = scanner.nextInt();` |
    | `nextDouble()` | Reads a double. | `double value = scanner.nextDouble();` |
    | `nextBoolean()` | Reads a boolean (`true` or `false`). | `boolean flag = scanner.nextBoolean();` |
    | `hasNext()` | Checks if there is more input (any type). | `if (scanner.hasNext())` |
    | `hasNextInt()` | Checks if the next input is an integer. | `if (scanner.hasNextInt())` |
    
    ---
    
4. **Reference Variables**
    
    In Java, **reference variables** are variables that store the memory address (or reference) of an object instead of storing the actual data like primitive variables do. Reference variables are essential for working with objects in Java.
    
    ---
    
    ### **Understanding Reference Variables**
    
    1. **Declaration and Instantiation**:
    A reference variable is declared with a specific data type, typically a class or an interface, and it refers to an object of that type.
        
        Example:
        
        ```java
        String str = "Hello"; // str is a reference variable pointing to a String object
        
        ```
        
    2. **Storage**:
        - Primitive variables directly hold the value (e.g., `int num = 5;`).
        - Reference variables hold the memory address of the object in the heap.
    3. **Default Value**:
    If a reference variable is not explicitly initialized, its default value is `null`.
        
        Example:
        
        ```java
        String uninitializedStr; // Default value: null
        
        ```
        
    
    ---
    
    ### **How Reference Variables Work**
    
    When you create an object, the actual object is stored in the **heap memory**, and the reference variable holds the **address** of the object.
    
    ```java
    class Person {
        String name;
    }
    
    public class ReferenceExample {
        public static void main(String[] args) {
            // Create a new Person object
            Person person = new Person();
            person.name = "John";
    
            // Another reference variable points to the same object
            Person anotherPerson = person;
            anotherPerson.name = "Jane";
    
            // Both references point to the same object
            System.out.println(person.name); // Output: Jane
        }
    }
    
    ```
    
    **Explanation**:
    
    - Both `person` and `anotherPerson` refer to the same memory location. Changing the object's data using one reference affects the other.
    
    ---
    
    ### **Key Features of Reference Variables**
    
    1. **Pass-by-Reference**:
    In Java, when reference variables are passed to methods, the actual object's reference is passed (not a copy of the object). This allows the method to modify the object's data.
        
        Example:
        
        ```java
        class Box {
            int size;
        }
        
        public class ReferenceDemo {
            static void modify(Box b) {
                b.size = 20; // Modifies the original object
            }
        
            public static void main(String[] args) {
                Box box = new Box();
                box.size = 10;
        
                modify(box);
                System.out.println(box.size); // Output: 20
            }
        }
        
        ```
        
    2. **Null References**:
    If a reference variable is `null`, it does not point to any object. Accessing it results in a **NullPointerException**.
        
        Example:
        
        ```java
        String str = null;
        System.out.println(str.length()); // Throws NullPointerException
        
        ```
        
    3. **Changing References**:
    You can change a reference variable to point to a different object, but the original object remains unaffected.
        
        Example:
        
        ```java
        String s1 = "Hello";
        String s2 = s1;
        
        s2 = "World"; // s1 remains "Hello"
        System.out.println(s1); // Output: Hello
        System.out.println(s2); // Output: World
        
        ```
        
    
    ---
    
    ### **Reference vs Object**
    
    - The **object** resides in the heap memory.
    - The **reference variable** is stored in the stack and points to the object in the heap.

---

### **Methods**

In Java, a **method** is a block of code that performs a specific task. Methods are used to define behaviors for objects and encapsulate code for reusability and modularity.

---

### **What is a Method?**

- A method is a function defined within a class.
- It can accept input (parameters), perform operations, and optionally return a result.
- Methods provide **modularity** by dividing tasks into smaller, reusable chunks.

---

### **1. Method Declaration and Syntax**

A method declaration specifies the method's name, return type, and parameters. It defines the structure of the method.

**Syntax**:

```java
modifier returnType methodName(parameterList) {
    // Method body
}

```

**Explanation**:

1. **modifier**: Determines access (e.g., `public`, `private`).
2. **returnType**: Data type of the value the method returns (use `void` for no return).
3. **methodName**: Identifier used to call the method.
4. **parameterList**: Input values the method accepts (optional).
5. **Method body**: Contains the code the method executes.

---

**Example**:

```java
public int addNumbers(int a, int b) {
    return a + b; // Returns the sum of a and b
}

```

---

### **2. Method Return Types**

The **return type** of a method determines the type of value it produces and returns to the caller. Use `void` if the method does not return any value.

### **Common Return Types**:

- **Primitive Types**: `int`, `double`, `char`, etc.
- **Reference Types**: Objects like `String`, `ArrayList`, etc.
- **Void**: No value returned.

**Examples**:

1. **Returning a value**:
    
    ```java
    public double calculateArea(double radius) {
        return 3.14 * radius * radius; // Returns a double
    }
    
    ```
    
2. **Void (no return)**:
    
    ```java
    public void printMessage() {
        System.out.println("Hello, World!");
    }
    
    ```
    

---

### **3. Method Parameters**

Parameters allow methods to accept input values. They are defined in the parentheses during method declaration.

### **Types of Parameters**:

- **Primitive Parameters**: Pass values directly.
- **Reference Parameters**: Pass object references.

**Syntax**:

```java
public returnType methodName(parameterType parameterName) {
    // Use parameter in the method
}

```

**Examples**:

1. **Single Parameter**:
    
    ```java
    public void greet(String name) {
        System.out.println("Hello, " + name);
    }
    
    ```
    
2. **Multiple Parameters**:
    
    ```java
    public int multiply(int x, int y) {
        return x * y;
    }
    
    ```
    
3. **No Parameters**:
    
    ```java
    public void displayTime() {
        System.out.println(System.currentTimeMillis());
    }
    
    ```
    

---

### **4. Method Invocation**

Methods are invoked using their name, followed by parentheses. If the method is not `static`, you need to call it on an instance of the class.

**Syntax**:

```java
objectName.methodName(arguments);

```

**Static Methods** (called using the class name):

```java
ClassName.methodName(arguments);

```

**Examples**:

1. **Non-static Method**:
    
    ```java
    class Calculator {
        public int add(int a, int b) {
            return a + b;
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Calculator calc = new Calculator(); // Create an object
            int sum = calc.add(5, 10); // Call the method
            System.out.println("Sum: " + sum);
        }
    }
    
    ```
    
2. **Static Method**:
    
    ```java
    public class MathUtils {
        public static int square(int num) {
            return num * num;
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            int result = MathUtils.square(4); // Call static method
            System.out.println("Square: " + result);
        }
    }
    
    ```
    

---

### **Example: Complete Program**

```java
public class Example {
    // Method with no return value (void)
    public void printMessage(String message) {
        System.out.println(message);
    }

    // Method with a return value
    public int addNumbers(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Example example = new Example();

        // Calling a void method
        example.printMessage("Hello, Java!");

        // Calling a method with a return value
        int sum = example.addNumbers(10, 20);
        System.out.println("Sum: " + sum);
    }
}

```

**Output**:

```
Hello, Java!
Sum: 30

```

---

### **Key Points**

- A method must be **declared** in a class but can be invoked multiple times.
- The **parameters** are passed to the method during the call.
- The **return type** determines what, if anything, the method gives back to the caller.

Let me know if you'd like detailed examples or have specific scenarios to explore!

---

### **Project Development**

### **1. Commenting**

Comments are annotations in the code meant for explanation or documentation. They are ignored by the compiler and help make code more readable and maintainable.

### Types of Comments:

1. **Single-line Comments**:
Use `//` for brief, inline explanations.
    
    ```java
    // This is a single-line comment
    int age = 25; // Variable to store age
    
    ```
    
2. **Multi-line Comments**:
Use `/* */` for longer descriptions.
    
    ```java
    /*
     This is a multi-line comment.
     It can span multiple lines.
    */
    int sum = a + b;
    
    ```
    
3. **Documentation Comments**:
Use `/** */` to generate API documentation with tools like **Javadoc**.
    
    ```java
    /**
     * Adds two integers.
     * @param a the first integer
     * @param b the second integer
     * @return the sum of a and b
     */
    public int add(int a, int b) {
        return a + b;
    }
    
    ```
    

---

### **2. Packages and Imports**

### Packages:

- A **package** is a namespace for organizing classes and interfaces.
- Helps avoid name conflicts and makes code easier to manage.

**Declaring a Package**:

```java
package com.example.myapp;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Packages!");
    }
}

```

### Imports:

- Use `import` to include classes from other packages.

**Default Package**:

- The `java.lang` package is automatically imported (e.g., `String`, `Math`).

**Manually Importing**:

```java
import java.util.Scanner;

public class Example {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
    }
}

```

**Wildcard Import**:

```java
import java.util.*; // Imports all classes from java.util

```

---

### **3. Stubs**

A **stub** is a placeholder or skeletal code for a method, class, or module. It is used during development as a temporary implementation for testing or prototyping.

**Example Stub**:

```java
public class Calculator {
    // Stub method: Placeholder for future implementation
    public int add(int a, int b) {
        // TODO: Implement this method
        return 0; // Temporary return value
    }
}

```

**Use Cases**:

- To allow other parts of the program to compile and run.
- To plan and outline code structure during development.

---

### **4. Reading the Stack Trace**

A **stack trace** is a detailed report of the error that caused an exception in your program. It helps identify where and why the error occurred.

**Structure of a Stack Trace**:

- Starts with the exception type and message.
- Lists the method calls in reverse order of execution.

**Example Stack Trace**:

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at Example.divide(Example.java:10)
    at Example.main(Example.java:20)

```

**How to Read**:

1. **Exception Type**: `java.lang.ArithmeticException`.
2. **Message**: `/ by zero`.
3. **Trace**:
    - `at Example.divide(Example.java:10)` → Error in `divide` method at line 10.
    - `at Example.main(Example.java:20)` → Called from `main` method at line 20.

**Steps to Debug**:

- Locate the error line in the stack trace.
- Check variables and logic leading to the error.

---

### **5. Using the Debugger**

A **debugger** is a tool that allows you to pause program execution and inspect its behavior step-by-step.

### Steps to Use a Debugger:

1. **Set Breakpoints**:
    - Identify where to pause execution.
    - Example: Set a breakpoint on the method you want to inspect.
2. **Run in Debug Mode**:
    - Use your IDE (e.g., IntelliJ IDEA, Eclipse) to start the program in debug mode.
3. **Inspect Variables**:
    - Check variable values at the current execution point.
4. **Step Through Code**:
    - **Step Into**: Dive into the method being called.
    - **Step Over**: Execute the current line and move to the next.
    - **Step Out**: Exit the current method and return to the caller.
5. **Watch Expressions**:
    - Add specific variables or expressions to a watch list for real-time updates.

---

---

### **Maven**

1. **Introduction to Maven**
    
    ### **Introduction to Maven**
    
    **Maven** is a powerful **build automation and project management tool** used primarily for Java projects. It simplifies the process of managing dependencies, building projects, and creating consistent development environments.
    
    ---
    
    ### **Key Features of Maven**
    
    1. **Dependency Management**:
        - Automatically downloads libraries and dependencies from a central repository.
        - Handles versioning and transitive dependencies.
    2. **Build Automation**:
        - Builds projects, compiles code, runs tests, and packages applications using a single command (`mvn package`).
    3. **Project Standardization**:
        - Follows a standardized directory structure for all projects, ensuring consistency.
    4. **Plugins and Lifecycle**:
        - Provides plugins for a wide variety of tasks (e.g., testing, deployment).
        - Built-in lifecycle phases (e.g., `compile`, `test`, `package`, `install`).
    5. **Portable and Scalable**:
        - Ensures consistency across environments with configuration in a single `pom.xml` file.
    
    ---
    
    ### **How Maven Works**
    
    Maven operates on the concept of:
    
    1. **Project Object Model (POM)**:
        - Central configuration file (`pom.xml`) that defines project settings, dependencies, plugins, and build instructions.
    2. **Repositories**:
        - **Local Repository**: A cache on your machine where Maven stores downloaded dependencies.
        - **Central Repository**: A public repository (like Maven Central) where Maven fetches dependencies.
        - **Remote Repositories**: Additional repositories specified in the `pom.xml`.
    3. **Build Lifecycle**:
    Maven builds projects in defined stages such as:
        - **validate**: Validates the project structure.
        - **compile**: Compiles the source code.
        - **test**: Runs unit tests.
        - **package**: Packages the code into a deployable format (e.g., `.jar`, `.war`).
        - **install**: Installs the package in the local repository.
        - **deploy**: Deploys the package to a remote repository.
    
    ---
    
    ### **Maven Directory Structure**
    
    Maven uses a standard directory layout:
    
    ```
    project/
    ├── src/
    │   ├── main/
    │   │   ├── java/         # Application source code
    │   │   ├── resources/    # Configuration files
    │   └── test/
    │       ├── java/         # Test source code
    │       ├── resources/    # Test resources
    ├── target/               # Compiled files and artifacts
    ├── pom.xml               # Project configuration file
    
    ```
    
    ---
    
2. **Maven lifecycle**
    
    ### **Maven Build Lifecycle**
    
    The **Maven Build Lifecycle** is a sequence of phases that define the steps to build and deploy a Maven project. These phases are executed in a specific order, ensuring all necessary steps are performed during the build process.
    
    ---
    
    ### **1. Key Concepts of Maven Lifecycle**
    
    1. **Phases**:
        - A **phase** represents a step in the build process (e.g., `compile`, `test`, `package`).
        - Executing a phase automatically executes all preceding phases.
    2. **Goals**:
        - A **goal** is a specific task bound to a phase (e.g., compiling code or packaging an application).
        - Goals can be executed independently of the lifecycle.
    3. **Plugins**:
        - Maven relies on plugins to execute goals during each phase.
    
    ---
    
    ### **2. Maven Default Lifecycle**
    
    Maven has three built-in lifecycles:
    
    1. **Default Lifecycle** (Most common):
        - Handles project build and deployment.
    2. **Clean Lifecycle**:
        - Cleans the project directory (removes temporary files and compiled artifacts).
    3. **Site Lifecycle**:
        - Generates project documentation.
    
    ---
    
    ### **3. Phases in the Default Lifecycle**
    
    The default lifecycle consists of the following **phases**:
    
    | **Phase** | **Description** |
    | --- | --- |
    | **validate** | Validates the project structure and configuration files (e.g., `pom.xml`). |
    | **compile** | Compiles the project’s source code into bytecode (`.class` files). |
    | **test** | Runs unit tests using a testing framework like JUnit or TestNG. |
    | **package** | Packages the compiled code into a distributable format (e.g., `.jar`, `.war`). |
    | **verify** | Runs checks to ensure the package is valid and meets quality standards. |
    | **install** | Installs the package into the local repository for use as a dependency. |
    | **deploy** | Copies the package to a remote repository for sharing with other developers. |
    
    ---
    
    ### **4. Clean Lifecycle**
    
    The **clean lifecycle** focuses on removing temporary files generated during the build process.
    
    | **Phase** | **Description** |
    | --- | --- |
    | **pre-clean** | Tasks performed before cleaning. |
    | **clean** | Deletes files generated during the build (e.g., `/target`). |
    | **post-clean** | Tasks performed after cleaning. |
    
    ---
    
    ### **5. Site Lifecycle**
    
    The **site lifecycle** generates project documentation.
    
    | **Phase** | **Description** |
    | --- | --- |
    | **pre-site** | Tasks performed before generating the site. |
    | **site** | Generates project documentation. |
    | **post-site** | Tasks performed after generating the site. |
    | **site-deploy** | Deploys the generated documentation to a server. |
    
    ---
    
3. **Central Repository**
    
    ### **Maven Central Repository**
    
    The **Maven Central Repository** is the primary public repository for Maven artifacts, such as libraries, frameworks, and plugins. It is managed by the Apache Software Foundation and is widely used by developers to access and share open-source software components.
    
    ---
    
    ### **Key Features of Maven Central Repository**
    
    1. **Public Accessibility**:
        - Maven Central is a globally accessible repository available at https://repo.maven.apache.org/maven2.
        - It hosts a vast collection of Java libraries and frameworks.
    2. **Standardized Structure**:
        - Artifacts in the repository follow a standardized naming convention based on `groupId`, `artifactId`, and `version`.
    3. **Automatic Dependency Management**:
        - Maven automatically downloads dependencies from Central when they are declared in the `pom.xml`.
    4. **Reliable and Secure**:
        - Artifacts are verified and vetted for reliability before inclusion in the repository.
    
    ---
    
    ### **How Maven Central Repository Works**
    
    When you build a Maven project:
    
    1. Maven checks the **local repository** on your machine for the required dependency.
    2. If the dependency is not found locally, Maven queries the Central Repository to download it.
    3. The downloaded artifact is cached in the local repository for future use.
    
    ---
    
    ### **Declaring Dependencies from Central Repository**
    
    Dependencies in Maven are added to the `pom.xml` file. Maven uses these dependencies to download the corresponding artifacts from Central.
    
    **Example**:
    
    ```xml
    <dependencies>
        <!-- Example: Adding the Gson library -->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.10</version>
        </dependency>
    </dependencies>
    
    ```
    
    **Explanation**:
    
    - **`groupId`**: Identifies the organization or project (e.g., `com.google.code.gson`).
    - **`artifactId`**: Identifies the library or module (e.g., `gson`).
    - **`version`**: Specifies the version to use (e.g., `2.10`).
    
    When Maven runs, it fetches the Gson library from the Central Repository if it is not already present in your local repository.
    
    ---
    
4. **Project Object Model**
    
    ### **Project Object Model (POM) in Maven**
    
    The **Project Object Model (POM)** is the core configuration file for a Maven project. It is an XML file named `pom.xml` located in the project's root directory. The POM file defines the project's dependencies, plugins, build configurations, and other settings, enabling Maven to manage the build lifecycle efficiently.
    
    ---
    
    ### **Key Components of a POM File**
    
    Here are the essential elements of a `pom.xml`:
    
    ### **1. Project Coordinates**
    
    - Defines the unique identifiers for the project.
    
    ```xml
    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <groupId>com.example</groupId>
        <artifactId>my-app</artifactId>
        <version>1.0.0</version>
    </project>
    
    ```
    
    - **`modelVersion`**: The version of the POM model (always `4.0.0` for Maven 2+).
    - **`groupId`**: A unique identifier for the organization or project (e.g., `com.example`).
    - **`artifactId`**: The project's name or module identifier (e.g., `my-app`).
    - **`version`**: The current version of the project (e.g., `1.0.0`).
    
    ---
    
    ### **2. Dependencies**
    
    - Specifies libraries or frameworks required for the project.
    
    ```xml
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.1.1</version>
        </dependency>
    </dependencies>
    
    ```
    
    - Dependencies include `groupId`, `artifactId`, and `version`.
    - Maven resolves dependencies from the Central Repository or other configured repositories.
    
    ---
    
    ### **3. Build Section**
    
    - Configures build settings, such as plugins and directories.
    
    ```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    
    ```
    
    - **Plugins**: Add functionality to the build process (e.g., compiling Java code).
    
    ---
    
    ### **4. Properties**
    
    - Defines reusable variables for project configuration.
    
    ```xml
    <properties>
        <java.version>11</java.version>
    </properties>
    
    ```
    
    - Use `${propertyName}` to reference properties in the POM.
    
    ---
    
    ### **5. Repositories**
    
    - Specifies custom repositories for dependencies.
    
    ```xml
    <repositories>
        <repository>
            <id>custom-repo</id>
            <url>https://example.com/maven-repo</url>
        </repository>
    </repositories>
    
    ```
    
    - The `id` identifies the repository, and `url` specifies its location.
    
    ---
    
    ### **6. Parent POM**
    
    - Enables inheritance from a parent POM for shared configuration.
    
    ```xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.1.1</version>
    </parent>
    
    ```
    
    ---
    
    ### **7. Modules**
    
    - Used in multi-module projects to group related projects.
    
    ```xml
    <modules>
        <module>module-a</module>
        <module>module-b</module>
    </modules>
    
    ```
    
    ---
    
    ### **Example POM File**
    
    Below is a complete example of a basic `pom.xml`:
    
    ```xml
    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <groupId>com.example</groupId>
        <artifactId>my-app</artifactId>
        <version>1.0.0</version>
    
        <!-- Dependencies -->
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
                <version>3.1.1</version>
            </dependency>
        </dependencies>
    
        <!-- Build configuration -->
        <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.8.1</version>
                    <configuration>
                        <source>11</source>
                        <target>11</target>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    
        <!-- Properties -->
        <properties>
            <java.version>11</java.version>
        </properties>
    </project>
    
    ```
    
    ---
    
    ### **Advantages of POM**
    
    1. **Centralized Configuration**:
        - All project settings, dependencies, and plugins are in a single file.
    2. **Dependency Management**:
        - Maven automatically resolves, downloads, and manages dependencies.
    3. **Build Automation**:
        - Simplifies the build process with pre-configured lifecycle phases.
    4. **Inheritance and Modularity**:
        - Parent POMs and modules promote reusability and consistent configuration.

---

### **Control Flow**

### **1. If Statements and Switch Statements**

### **If Statements**

Used to execute code based on a condition.

**Syntax**:

```java
if (condition) {
    // Code to execute if condition is true
} else if (anotherCondition) {
    // Code to execute if anotherCondition is true
} else {
    // Code to execute if none of the conditions are true
}

```

**Example**:

```java
int age = 18;
if (age >= 18) {
    System.out.println("You are eligible to vote.");
} else {
    System.out.println("You are not eligible to vote.");
}

```

### **Switch Statements**

Used to execute code based on a single variable's value.

**Syntax**:

```java
switch (variable) {
    case value1:
        // Code for value1
        break;
    case value2:
        // Code for value2
        break;
    default:
        // Default code
}

```

**Example**:

```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Other day");
}

```

---

### **2. Comparison and Logical Operators**

### **Comparison Operators**:

| Operator | Description | Example |
| --- | --- | --- |
| `==` | Equal to | `a == b` |
| `!=` | Not equal to | `a != b` |
| `>` | Greater than | `a > b` |
| `<` | Less than | `a < b` |
| `>=` | Greater than or equal | `a >= b` |
| `<=` | Less than or equal | `a <= b` |

### **Logical Operators**:

| Operator | Description | Example |
| --- | --- | --- |
| `&&` | Logical AND | `a > 0 && b > 0` |
| ` |  | ` |
| `!` | Logical NOT | `!(a > 0)` |

---

### **3. Loops**

### **While Loop**

Executes as long as the condition is true.

**Syntax**:

```java
while (condition) {
    // Code to execute
}

```

**Example**:

```java
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}

```

### **For Loop**

Executes a block of code for a specified number of iterations.

**Syntax**:

```java
for (initialization; condition; increment) {
    // Code to execute
}

```

**Example**:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}

```

---

### **4. Variable Scopes**

### **Local Variables**:

- Declared within a method or block.
- Accessible only within the method or block.

**Example**:

```java
public void printNumber() {
    int number = 10; // Local variable
    System.out.println(number);
}

```

### **Instance Variables**:

- Declared inside a class but outside any method.
- Unique to each object.

**Example**:

```java
class Example {
    int count; // Instance variable
}

```

### **Class (Static) Variables**:

- Declared using the `static` keyword.
- Shared across all instances of the class.

**Example**:

```java
class Example {
    static int sharedCount; // Class variable
}

```

---

### **5. Arrays**

An **array** is a data structure in Java that stores a fixed-size sequential collection of elements of the same type. Arrays are zero-indexed, meaning the first element is accessed at index `0`.

---

### **1. Characteristics of Arrays**

- **Fixed Size**: The size of the array is defined when it is created and cannot be changed.
- **Homogeneous**: All elements must be of the same data type.
- **Zero-based Indexing**: Elements are accessed using indices starting from `0`.

---

### **2. Declaring and Initializing Arrays**

### **Declaration**:

```java
dataType[] arrayName;

```

or

```java
dataType arrayName[];

```

### **Initialization**:

1. **Specify Size**:
    
    ```java
    int[] numbers = new int[5]; // Creates an array of size 5
    
    ```
    
2. **Initialize with Values**:
    
    ```java
    int[] numbers = {1, 2, 3, 4, 5}; // Creates and initializes
    
    ```
    
3. **Separate Declaration and Initialization**:
    
    ```java
    int[] numbers;
    numbers = new int[] {1, 2, 3};
    
    ```
    

---

### **3. Accessing and Modifying Elements**

### Accessing Elements:

Use the **index** to access an element.

```java
int[] numbers = {10, 20, 30};
System.out.println(numbers[1]); // Output: 20

```

### Modifying Elements:

Assign a new value using the index.

```java
numbers[1] = 50; // Updates the second element
System.out.println(numbers[1]); // Output: 50

```

---

### **4. Iterating Over Arrays**

### **Using a For Loop**:

```java
int[] numbers = {1, 2, 3, 4, 5};
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

```

### **Using a For-Each Loop**:

```java
for (int number : numbers) {
    System.out.println(number);
}

```

---

### **5. Array Length**

The **length** property returns the size of the array.

```java
int[] numbers = {1, 2, 3};
System.out.println(numbers.length); // Output: 3

```

---

### **6. Multi-Dimensional Arrays**

An array containing other arrays (e.g., 2D arrays, 3D arrays).

### Declaration and Initialization:

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

```

### Accessing Elements:

```java
System.out.println(matrix[1][2]); // Output: 6 (second row, third column)

```

### Iterating Through a 2D Array:

```java
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}

```

---

### **7. Common Operations on Arrays**

### **Copying Arrays**:

```java
int[] original = {1, 2, 3};
int[] copy = Arrays.copyOf(original, original.length);
System.out.println(Arrays.toString(copy)); // Output: [1, 2, 3]

```

### **Sorting Arrays**:

```java
int[] numbers = {5, 3, 8, 1};
Arrays.sort(numbers);
System.out.println(Arrays.toString(numbers)); // Output: [1, 3, 5, 8]

```

### **Searching Arrays**:

```java
int index = Arrays.binarySearch(numbers, 3);
System.out.println(index); // Output: 1 (index of element 3)

```

---

### **8. Limitations of Arrays**

- Fixed size: Cannot dynamically grow or shrink.
- Requires manual resizing or using other data structures like **ArrayList** for flexible arrays.

---

### **9. Example Program**

```java
import java.util.Arrays;

public class ArrayExample {
    public static void main(String[] args) {
        // Declare and initialize an array
        int[] numbers = {10, 20, 30, 40, 50};

        // Access and modify elements
        System.out.println("Original value at index 2: " + numbers[2]);
        numbers[2] = 35;
        System.out.println("Modified value at index 2: " + numbers[2]);

        // Iterate using a for loop
        System.out.println("Array elements:");
        for (int i = 0; i < numbers.length; i++) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        // Sort the array
        Arrays.sort(numbers);
        System.out.println("Sorted array: " + Arrays.toString(numbers));
    }
}

```

---

### **10. Arrays vs Other Data Structures**

| Feature | Arrays | ArrayList (from `java.util`) |
| --- | --- | --- |
| **Size** | Fixed | Dynamic |
| **Performance** | Faster | Slightly slower due to overhead |
| **Primitive Types** | Directly stores values | Stores primitives as objects |
| **Usage** | Lightweight and simple | Flexible and easier to manage |

---

If you need further details, advanced examples, or comparisons, let me know!

---

### **6. Advanced Boolean Expressions**

Combines multiple conditions and logical operators.

**Example**:

```java
int age = 25;
boolean isEligible = (age >= 18 && age <= 65) || (age > 70 && age < 80);
System.out.println(isEligible);

```

---

### **7. Method Recursion**

**Recursion** is when a method calls itself.

**Syntax**:

```java
returnType methodName(parameters) {
    if (baseCondition) {
        // Stop recursion
        return result;
    } else {
        // Recursive call
        return methodName(newParameters);
    }
}

```

**Example**: Calculating Factorial

```java
public int factorial(int n) {
    if (n == 0) { // Base case
        return 1;
    } else {
        return n * factorial(n - 1); // Recursive call
    }
}

public static void main(String[] args) {
    System.out.println(new Example().factorial(5)); // Output: 120
}

```

---

### **Types**

1. **Value and reference types**
    
    ### **Value and Reference Types in Java**
    
    Java's data types are divided into **value types** (primitives) and **reference types** (objects). Understanding their behavior is crucial for writing efficient and bug-free programs.
    
    ---
    
    ### **1. Value Types**
    
    **Definition**:
    
    Value types are **primitive data types** in Java. They directly hold the value in memory and do not refer to any object.
    
    ### **Characteristics**:
    
    - Stored in **stack memory**.
    - Variables contain the actual value.
    - Operations on value types create a new value; they do not modify the original.
    - Independent of each other.
    
    ### **Examples**:
    
    | **Primitive Type** | **Size** | **Default Value** | **Examples** |
    | --- | --- | --- | --- |
    | `byte` | 1 byte | `0` | `byte b = 100;` |
    | `short` | 2 bytes | `0` | `short s = 3000;` |
    | `int` | 4 bytes | `0` | `int i = 42;` |
    | `long` | 8 bytes | `0L` | `long l = 123L;` |
    | `float` | 4 bytes | `0.0f` | `float f = 3.14f;` |
    | `double` | 8 bytes | `0.0d` | `double d = 3.14;` |
    | `char` | 2 bytes | `'\u0000'` | `char c = 'A';` |
    | `boolean` | 1 bit | `false` | `boolean b = true;` |
    
    ---
    
    ### **Example: Value Type Behavior**:
    
    ```java
    int a = 10;
    int b = a; // Copies the value of 'a' into 'b'
    
    b = 20; // Modifies 'b', but 'a' remains unchanged
    System.out.println("a: " + a); // Output: a: 10
    System.out.println("b: " + b); // Output: b: 20
    
    ```
    
    ---
    
    ### **2. Reference Types**
    
    **Definition**:
    
    Reference types store the **memory address** (reference) of an object, rather than the actual data. These include classes, arrays, interfaces, and enums.
    
    ### **Characteristics**:
    
    - Stored in **heap memory**.
    - Variables hold a reference (or pointer) to the actual object.
    - Operations on reference types can modify the original object.
    - Multiple references can point to the same object.
    
    ### **Examples**:
    
    - Objects created from classes:
        
        ```java
        String name = "Java";
        
        ```
        
    - Arrays:
        
        ```java
        int[] numbers = {1, 2, 3};
        
        ```
        
    - Custom classes:
        
        ```java
        class Person { String name; }
        Person p = new Person();
        
        ```
        
    
    ---
    
    ### **Example: Reference Type Behavior**:
    
    ```java
    int[] array1 = {1, 2, 3};
    int[] array2 = array1; // Both variables point to the same array
    
    array2[0] = 100; // Modifying 'array2' affects 'array1'
    System.out.println(array1[0]); // Output: 100
    
    ```
    
    ---
    
    ### **3. Key Differences Between Value and Reference Types**
    
    | **Aspect** | **Value Type** | **Reference Type** |
    | --- | --- | --- |
    | **Storage** | Stored in **stack memory** | Stored in **heap memory** |
    | **Holds** | Actual value | Reference (memory address) of object |
    | **Default Value** | Defined defaults (`0`, `false`, etc.) | `null` |
    | **Mutability** | Independent | Can modify the object it refers to |
    | **Example** | `int`, `float`, `boolean` | `String`, `int[]`, `Person` |
    
    ---
    
2. **Introduction to OOP**
    
    ### **Introduction to Object-Oriented Programming (OOP)**
    
    **Object-Oriented Programming (OOP)** is a programming paradigm that organizes software design around **objects**, which represent real-world entities. OOP focuses on **data** (attributes) and **behavior** (methods) and promotes code modularity, reusability, and scalability.
    
    ---
    
    ### **Core Concepts of OOP**
    
    1. **Class**:
        - A blueprint for creating objects.
        - Defines attributes (fields) and behaviors (methods).
        
        **Example**:
        
        ```java
        class Car {
            String brand;
            int speed;
        
            void drive() {
                System.out.println(brand + " is driving at " + speed + " mph.");
            }
        }
        
        ```
        
    2. **Object**:
        - An instance of a class.
        - Represents a real-world entity with state and behavior.
        
        **Example**:
        
        ```java
        Car myCar = new Car(); // Object creation
        myCar.brand = "Toyota";
        myCar.speed = 60;
        myCar.drive(); // Output: Toyota is driving at 60 mph.
        
        ```
        
    3. **Encapsulation**:
        - Bundles data (attributes) and methods that operate on the data into a single unit (class).
        - Protects data by making fields private and exposing access through public methods (getters and setters).
        
        **Example**:
        
        ```java
        class BankAccount {
            private double balance;
        
            public double getBalance() {
                return balance;
            }
        
            public void deposit(double amount) {
                if (amount > 0) {
                    balance += amount;
                }
            }
        }
        
        ```
        
    4. **Inheritance**:
        - Allows a class (subclass) to inherit fields and methods from another class (superclass).
        - Promotes code reuse.
        
        **Example**:
        
        ```java
        class Animal {
            void eat() {
                System.out.println("This animal eats food.");
            }
        }
        
        class Dog extends Animal {
            void bark() {
                System.out.println("The dog barks.");
            }
        }
        
        Dog dog = new Dog();
        dog.eat();  // Inherited method
        dog.bark(); // Subclass-specific method
        
        ```
        
    5. **Polymorphism**:
        - Enables a single entity (method or object) to behave differently based on context.
        - Achieved via method overloading and overriding.
        
        **Example of Overriding**:
        
        ```java
        class Animal {
            void sound() {
                System.out.println("Animal makes a sound.");
            }
        }
        
        class Cat extends Animal {
            @Override
            void sound() {
                System.out.println("Cat meows.");
            }
        }
        
        Animal myAnimal = new Cat();
        myAnimal.sound(); // Output: Cat meows.
        
        ```
        
    6. **Abstraction**:
        - Hides implementation details and exposes only essential features.
        - Achieved using abstract classes and interfaces.
        
        **Example**:
        
        ```java
        abstract class Shape {
            abstract void draw();
        }
        
        class Circle extends Shape {
            void draw() {
                System.out.println("Drawing a circle.");
            }
        }
        
        Shape shape = new Circle();
        shape.draw(); // Output: Drawing a circle.
        
        ```
        
    
    ---
    
    ### **Advantages of OOP**
    
    1. **Modularity**:
        - Classes and objects make code more modular, facilitating debugging and maintenance.
    2. **Code Reusability**:
        - Inheritance allows sharing of functionality across classes.
    3. **Flexibility and Scalability**:
        - Polymorphism makes code flexible to adapt to new requirements.
    4. **Data Security**:
        - Encapsulation restricts direct access to sensitive data.
    5. **Real-World Modeling**:
        - Objects represent real-world entities, making code intuitive.
    
    ---
    
    ### **Key Principles (SOLID)**
    
    1. **Single Responsibility Principle (SRP)**:
        - A class should have one and only one reason to change.
    2. **Open-Closed Principle (OCP)**:
        - Classes should be open for extension but closed for modification.
    3. **Liskov Substitution Principle (LSP)**:
        - Subtypes must be substitutable for their base types.
    4. **Interface Segregation Principle (ISP)**:
        - Interfaces should be client-specific, not one-size-fits-all.
    5. **Dependency Inversion Principle (DIP)**:
        - High-level modules should not depend on low-level modules; both should depend on abstractions.
    
    ---
    
3. **Stack and Garbage Collection**
    
    ### **Stack and Garbage Collection in Java**
    
    Java efficiently manages memory through a combination of **stack memory** and **heap memory**, with automatic memory cleanup performed by the **Garbage Collector**.
    
    ---
    
    ### **1. Stack Memory**
    
    **Stack memory** is used for the execution of a thread, storing:
    
    1. **Method calls** (function frames).
    2. **Local variables**.
    3. **Primitive types** and **references** to objects in heap memory.
    
    ### **Characteristics of Stack Memory**:
    
    - **Fast Access**: Direct access; no complex management like in heap memory.
    - **Thread-Specific**: Each thread has its own stack.
    - **LIFO (Last-In-First-Out)**: Memory is allocated and deallocated in a specific order.
    
    ### **Example**:
    
    ```java
    public class StackExample {
        public static void main(String[] args) {
            int a = 10; // Local variable stored in stack
            int result = multiply(a, 5); // Method call pushed to stack
            System.out.println("Result: " + result);
        }
    
        public static int multiply(int x, int y) {
            int product = x * y; // Local variable
            return product; // Product goes out of scope after method exits
        }
    }
    
    ```
    
    **How Stack Works**:
    
    1. **Method Calls**:
        - Each method call creates a **stack frame** containing its local variables and return address.
        - Frames are destroyed when the method finishes execution.
    2. **Scope Management**:
        - Local variables exist only within their respective stack frames.
    
    ---
    
    ### **2. Heap Memory**
    
    **Heap memory** is used for dynamic allocation of objects and JRE classes. All objects and class variables are stored here.
    
    ### **Characteristics of Heap Memory**:
    
    - **Global Access**: Accessible from anywhere through references.
    - **Garbage Collected**: The Garbage Collector automatically reclaims unused memory.
    - **Slower Access**: Memory management requires more overhead than stack memory.
    
    ### **Example**:
    
    ```java
    class Person {
        String name; // Stored in heap
        int age;     // Stored in heap
    
        Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
    
    public class HeapExample {
        public static void main(String[] args) {
            Person p1 = new Person("Alice", 25); // Object stored in heap, reference in stack
            System.out.println(p1.name);
        }
    }
    
    ```
    
    ---
    
    ### **3. Garbage Collection**
    
    **Garbage Collection (GC)** is Java's process of automatically reclaiming memory occupied by objects no longer accessible in the program.
    
    ### **Key Features**:
    
    1. **Automatic Process**:
        - No need for manual memory management (unlike languages like C++).
    2. **Tracks Object Reachability**:
        - Objects are eligible for garbage collection if they are no longer referenced.
    
    ### **How It Works**:
    
    - The Garbage Collector runs periodically to identify and reclaim memory from unreachable objects.
    
    ### **Example**:
    
    ```java
    public class GCExample {
        public static void main(String[] args) {
            Person p1 = new Person("Alice", 25);
            p1 = null; // p1 is now eligible for garbage collection
            System.gc(); // Suggests the JVM to perform garbage collection
        }
    }
    
    ```
    
    **Note**: Calling `System.gc()` does not guarantee immediate GC execution—it’s a request to the JVM.
    
    ### **4. Stack vs. Heap Memory**
    
    | **Aspect** | **Stack Memory** | **Heap Memory** |
    | --- | --- | --- |
    | **Usage** | Stores method calls and local variables. | Stores objects and class-level variables. |
    | **Allocation/Access** | LIFO (fast and efficient). | Slower due to dynamic allocation. |
    | **Lifetime** | Exists for the lifetime of the method. | Exists until garbage collected. |
    | **Management** | Managed automatically (scope-based). | Managed via garbage collection. |
    | **Thread Specificity** | Thread-specific. | Shared across all threads. |
    
    ---
    
    ### **5. Code Example Illustrating Stack and Heap**
    
    ```java
    class Person {
        String name; // Stored in heap
        int age;     // Stored in heap
    
        Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
    
    public class MemoryDemo {
        public static void main(String[] args) {
            int localVariable = 10; // Stored in stack
            Person p = new Person("John", 30); // Object in heap, reference in stack
    
            // p now points to null, making the Person object eligible for GC
            p = null;
    
            // Request Garbage Collection
            System.gc();
        }
    }
    
    ```
    
    ---
    
    ### **6. Summary**
    
    | **Aspect** | **Stack Memory** | **Heap Memory** |
    | --- | --- | --- |
    | **Purpose** | Stores local variables and method calls. | Stores objects and global variables. |
    | **Lifetime** | Tied to method execution. | Determined by garbage collection. |
    | **Speed** | Faster | Slower due to dynamic allocation. |
    | **Management** | Scope-based (automatic). | Managed via garbage collection. |
    
    ---
    
4. **Classes and Objects**
    
    ### **Classes and Objects in Java**
    
    Java is an object-oriented programming (OOP) language where the primary focus is on creating reusable and modular code through **classes** and **objects**. These are the core building blocks of Java programs.
    
    ---
    
    ### **1. Classes**
    
    A **class** is a blueprint or template for creating objects. It defines:
    
    1. **Attributes (fields)**: Represent the object's properties.
    2. **Methods**: Represent the object's behaviors.
    
    ### **Syntax for a Class**
    
    ```java
    class ClassName {
        // Fields (attributes)
        dataType fieldName;
    
        // Methods (behaviors)
        returnType methodName(parameters) {
            // Method body
        }
    }
    
    ```
    
    ### **Example of a Class**
    
    ```java
    class Car {
        // Attributes
        String brand;
        int speed;
    
        // Constructor
        Car(String brand, int speed) {
            this.brand = brand;
            this.speed = speed;
        }
    
        // Method
        void drive() {
            System.out.println(brand + " is driving at " + speed + " mph.");
        }
    }
    
    ```
    
    ---
    
    ### **2. Objects**
    
    An **object** is an instance of a class. It represents a real-world entity with specific values for the attributes and access to methods defined in the class.
    
    ### **Creating Objects**
    
    Use the `new` keyword to create objects:
    
    ```java
    ClassName objectName = new ClassName(parameters);
    
    ```
    
    ### **Example of an Object**
    
    ```java
    public class Main {
        public static void main(String[] args) {
            // Creating an object of the Car class
            Car myCar = new Car("Toyota", 120);
    
            // Accessing object properties and methods
            System.out.println(myCar.brand); // Output: Toyota
            myCar.drive(); // Output: Toyota is driving at 120 mph.
        }
    }
    
    ```
    
    ---
    
    ### **3. Components of a Class**
    
    ### **a. Fields (Attributes)**
    
    - Represent data or state.
    - Can be of primitive types or reference types.
    
    ### **b. Methods**
    
    - Define behaviors or actions that objects of the class can perform.
    
    ### **c. Constructor**
    
    - A special method used to initialize an object.
    - **No return type**, and its name matches the class name.
    - **Example**:
        
        ```java
        class Car {
            String brand;
        
            // Constructor
            Car(String brand) {
                this.brand = brand;
            }
        }
        
        ```
        
    
    ### **d. Access Modifiers**
    
    - Control access to fields and methods:
        - `public`: Accessible from anywhere.
        - `private`: Accessible only within the class.
        - `protected`: Accessible within the package and by subclasses.
        - Default (no modifier): Accessible within the package.
    
    ---
    
    ### **4. Key Differences Between Classes and Objects**
    
    | **Aspect** | **Class** | **Object** |
    | --- | --- | --- |
    | **Definition** | Blueprint for creating objects. | Instance of a class. |
    | **Storage** | Does not occupy memory directly. | Occupies memory when created. |
    | **Use** | Defines behavior and properties. | Represents an entity with behavior. |
    | **Example** | `class Car {}` | `Car myCar = new Car();` |
    
    ---
    
    ### **5. Class Members: Static vs. Non-Static**
    
    ### **Static Members**:
    
    - Belong to the class, not individual objects.
    - Can be accessed without creating an object.
    - Use the `static` keyword.
    
    **Example**:
    
    ```java
    class MathUtils {
        static int add(int a, int b) {
            return a + b;
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            int sum = MathUtils.add(5, 10); // Accessing static method
            System.out.println(sum); // Output: 15
        }
    }
    
    ```
    
    ### **Non-Static Members**:
    
    - Belong to the object.
    - Require an object to be accessed.
    
    **Example**:
    
    ```java
    class Counter {
        int count = 0;
    
        void increment() {
            count++;
        }
    }
    
    ```
    
    ---
    
5. **String pool and String basics**
    
    ### **String Basics and String Pool in Java**
    
    The **`String`** class in Java is a fundamental and widely used class for handling and manipulating text. Strings in Java are immutable, meaning once a string object is created, it cannot be modified.
    
    ---
    
    ### **1. Strings in Java**
    
    ### **Characteristics of Strings**:
    
    1. **Immutable**:
        - The content of a `String` object cannot be changed after it's created.
        - Any modification results in the creation of a new `String` object.
        
        **Example**:
        
        ```java
        String s1 = "Hello";
        s1.concat(" World"); // Creates a new String but does not modify s1
        System.out.println(s1); // Output: Hello
        
        ```
        
    2. **`String` Class**:
        - The `String` class is part of the `java.lang` package and does not require explicit import.
        - Strings can be created using literals or the `new` keyword.
    3. **Immutable Nature Advantage**:
        - Makes strings thread-safe.
        - Allows safe sharing of `String` objects.
    
    ---
    
    ### **2. Creating Strings**
    
    ### **Using String Literals**:
    
    - When a string is created using double quotes, it is stored in the **String Pool**.
    
    ```java
    String s1 = "Hello";
    
    ```
    
    ### **Using the `new` Keyword**:
    
    - Creates a new object in the heap memory, even if an identical string exists in the String Pool.
    
    ```java
    String s2 = new String("Hello");
    
    ```
    
    **Comparison**:
    
    ```java
    String s1 = "Hello"; // From String Pool
    String s2 = new String("Hello"); // New object in heap
    
    System.out.println(s1 == s2); // Output: false (compares references)
    System.out.println(s1.equals(s2)); // Output: true (compares values)
    
    ```
    
    ---
    
    ### **3. String Pool**
    
    The **String Pool** (or intern pool) is a special memory region in the **heap** where Java stores unique string literals. This improves memory efficiency and performance.
    
    ### **How it Works**:
    
    1. When a string literal is created, the JVM checks the String Pool.
        - If the string already exists, it reuses the reference.
        - If not, it creates a new string in the pool.
    2. Strings created using the `new` keyword do not go into the pool unless explicitly interned.
    
    ### **String Interning**:
    
    - The `intern()` method moves a string to the pool or returns the reference if it already exists.
    
    **Example**:
    
    ```java
    String s1 = new String("Hello");
    String s2 = s1.intern(); // Moves "Hello" to the pool
    String s3 = "Hello";
    
    System.out.println(s2 == s3); // Output: true
    
    ```
    
    ---
    
    ### **4. Common String Methods**
    
    | **Method** | **Description** | **Example** |
    | --- | --- | --- |
    | `charAt(int index)` | Returns the character at a specific index. | `"Hello".charAt(1); // Output: e` |
    | `length()` | Returns the length of the string. | `"Hello".length(); // Output: 5` |
    | `substring(int start)` | Returns a substring from the start index. | `"Hello".substring(2); // Output: llo` |
    | `substring(int start, int end)` | Returns a substring between start and end indices. | `"Hello".substring(1, 4); // Output: ell` |
    | `toLowerCase()` | Converts the string to lowercase. | `"Hello".toLowerCase(); // Output: hello` |
    | `toUpperCase()` | Converts the string to uppercase. | `"Hello".toUpperCase(); // Output: HELLO` |
    | `equals(String s)` | Compares strings for equality. | `"Hello".equals("hello"); // Output: false` |
    | `equalsIgnoreCase(String s)` | Compares strings ignoring case. | `"Hello".equalsIgnoreCase("hello"); // true` |
    | `contains(CharSequence s)` | Checks if the string contains a sequence. | `"Hello".contains("ell"); // Output: true` |
    | `replace(char old, char new)` | Replaces all occurrences of a character. | `"Hello".replace('l', 'x'); // Output: Hexxo` |
    | `split(String regex)` | Splits the string into an array. | `"a,b,c".split(","); // Output: ["a", "b", "c"]` |
    | `trim()` | Removes leading and trailing spaces. | `" Hello ".trim(); // Output: "Hello"` |
    
    ---
    
    ### **5. Comparison of Strings**
    
    ### **`==` vs. `.equals()`**:
    
    - `==` compares references (memory addresses).
    - `.equals()` compares the content.
    
    **Example**:
    
    ```java
    String s1 = "Hello";
    String s2 = new String("Hello");
    
    System.out.println(s1 == s2);       // false (different memory locations)
    System.out.println(s1.equals(s2)); // true (content is the same)
    
    ```
    
    ---
    
    ### **6. String Immutability**
    
    ### **Why Strings are Immutable**:
    
    1. **Security**:
        - Strings are often used as keys, passwords, etc., and immutability ensures they can't be altered.
    2. **Performance**:
        - String Pool optimization relies on immutability.
    3. **Thread-Safety**:
        - Shared strings across threads remain unchanged.
    
    ---
    
    ### **7. Performance with Strings**
    
    ### **StringBuilder and StringBuffer**:
    
    For scenarios where strings are modified frequently (e.g., concatenation in loops), use `StringBuilder` or `StringBuffer`.
    
    - **StringBuilder**: Faster, not thread-safe.
    - **StringBuffer**: Thread-safe but slower.
    
    **Example**:
    
    ```java
    StringBuilder sb = new StringBuilder("Hello");
    sb.append(" World");
    System.out.println(sb.toString()); // Output: Hello World
    
    ```
    
    ---
    
    ### **8. Examples of String Usage**
    
    ### **Reverse a String**:
    
    ```java
    String str = "Hello";
    String reversed = new StringBuilder(str).reverse().toString();
    System.out.println(reversed); // Output: olleH
    
    ```
    
    ### **Count Characters in a String**:
    
    ```java
    String str = "Hello";
    System.out.println("Length: " + str.length()); // Output: Length: 5
    
    ```
    
    ### **Split and Iterate**:
    
    ```java
    String str = "Java,Python,C++";
    String[] languages = str.split(",");
    for (String lang : languages) {
        System.out.println(lang);
    }
    // Output:
    // Java
    // Python
    // C++
    
    ```
    
    ---
    
    ### **Summary**
    
    | **Aspect** | **Details** |
    | --- | --- |
    | **Immutability** | Strings cannot be changed after creation. |
    | **String Pool** | Stores unique string literals to optimize memory. |
    | **Comparison** | Use `.equals()` to compare content, not `==`. |
    | **Performance** | Use `StringBuilder` for frequent string modifications. |
    | **Usage** | Widely used for text manipulation and representation. |
    
    ---
    
6. **Equality, Hashcode, Equals**
    
    ### **Equality, `hashCode()`, and `equals()` in Java**
    
    In Java, **equality** involves comparing objects to determine if they are "equal." This comparison can be based on memory reference (`==`) or the logical equivalence defined by the `equals()` method.
    
    Additionally, the **`hashCode()`** method plays a crucial role in determining the identity of objects in hash-based collections like `HashMap` or `HashSet`.
    
    ---
    
    ### **1. Equality in Java**
    
    ### **Reference Equality (`==`)**:
    
    - Compares the memory addresses of two objects to check if they reference the same object.
    - It is the default behavior of `==` for objects.
    
    **Example**:
    
    ```java
    String s1 = new String("Hello");
    String s2 = new String("Hello");
    System.out.println(s1 == s2); // false (different memory locations)
    
    ```
    
    ### **Value Equality (`equals()`)**:
    
    - Compares the **content** or **logical equivalence** of two objects.
    - The default implementation of `equals()` in the `Object` class behaves like `==` unless overridden.
    
    **Example**:
    
    ```java
    String s1 = new String("Hello");
    String s2 = new String("Hello");
    System.out.println(s1.equals(s2)); // true (same content)
    
    ```
    
    ---
    
    ### **2. `equals()` Method**
    
    ### **Definition**:
    
    The `equals()` method is used to compare the logical equality of objects.
    
    ### **Default Behavior**:
    
    - The `Object` class defines `equals()` as:
        
        ```java
        public boolean equals(Object obj) {
            return (this == obj);
        }
        
        ```
        
    
    ### **Overriding `equals()`**:
    
    - Override `equals()` to provide a meaningful equality comparison.
    
    **Example**:
    
    ```java
    class Person {
        String name;
        int age;
    
        Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null || getClass() != obj.getClass()) return false;
            Person person = (Person) obj;
            return age == person.age && name.equals(person.name);
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Person p1 = new Person("Alice", 30);
            Person p2 = new Person("Alice", 30);
            System.out.println(p1.equals(p2)); // true
        }
    }
    
    ```
    
    ---
    
    ### **3. `hashCode()` Method**
    
    ### **Definition**:
    
    The `hashCode()` method returns an integer (hash code) that represents the object. It is used in hash-based collections like `HashMap` and `HashSet`.
    
    ### **Default Behavior**:
    
    - The `Object` class's `hashCode()` implementation returns a unique integer for each object, derived from its memory address.
    
    ### **Overriding `hashCode()`**:
    
    - If you override `equals()`, you **must override `hashCode()`** to ensure consistency.
    - Equal objects (`equals() == true`) must have the same hash code.
    
    **Example**:
    
    ```java
    class Person {
        String name;
        int age;
    
        Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null || getClass() != obj.getClass()) return false;
            Person person = (Person) obj;
            return age == person.age && name.equals(person.name);
        }
    
        @Override
        public int hashCode() {
            return Objects.hash(name, age); // Combines hash codes of fields
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Person p1 = new Person("Alice", 30);
            Person p2 = new Person("Alice", 30);
    
            System.out.println(p1.hashCode()); // Same hash code
            System.out.println(p2.hashCode()); // Same hash code
        }
    }
    
    ```
    
    ---
    
    ### **4. Relationship Between `equals()` and `hashCode()`**
    
    | **Aspect** | **Requirement** |
    | --- | --- |
    | **Consistency** | If `equals()` is overridden, `hashCode()` must also be overridden. |
    | **Equal Objects** | If `obj1.equals(obj2) == true`, then `obj1.hashCode() == obj2.hashCode()`. |
    | **Unequal Objects** (not mandatory) | If `obj1.equals(obj2) == false`, `hashCode()` values may or may not differ. |
    
    ---
    
7. **Casting primitives and objects**
    
    ### **Casting in Java**
    
    **Casting** is the process of converting a variable from one type to another. Java supports two types of casting:
    
    1. **Primitive Type Casting**: Conversion between primitive data types.
    2. **Object Type Casting**: Conversion between objects of related types.
    
    ---
    
    ### **1. Primitive Type Casting**
    
    ### **Types of Primitive Casting**
    
    1. **Widening (Implicit Casting)**:
        - Automatically performed when converting a smaller type to a larger type.
        - No data loss occurs.
        - **Example**: `byte → short → int → long → float → double`.
        
        **Example**:
        
        ```java
        int num = 100;
        double doubleNum = num; // Implicit casting
        System.out.println(doubleNum); // Output: 100.0
        
        ```
        
    2. **Narrowing (Explicit Casting)**:
        - Must be explicitly performed when converting a larger type to a smaller type.
        - Can result in data loss or truncation.
        - **Example**: `double → float → long → int → short → byte`.
        
        **Example**:
        
        ```java
        double doubleNum = 100.99;
        int intNum = (int) doubleNum; // Explicit casting
        System.out.println(intNum); // Output: 100 (truncated)
        
        ```
        
    
    ### **Examples of Primitive Casting**
    
    ```java
    public class PrimitiveCasting {
        public static void main(String[] args) {
            // Widening
            int a = 10;
            double b = a; // Implicit casting
            System.out.println(b); // Output: 10.0
    
            // Narrowing
            double x = 9.78;
            int y = (int) x; // Explicit casting
            System.out.println(y); // Output: 9
        }
    }
    
    ```
    
    ---
    
    ### **2. Object Type Casting**
    
    In Java, object type casting is used for converting an object of one type to another in an inheritance hierarchy.
    
    ### **Types of Object Casting**
    
    1. **Upcasting**:
        - Casting a subclass object to a superclass type.
        - **Implicit** and always safe.
        - **Example**: `Dog → Animal`.
    2. **Downcasting**:
        - Casting a superclass object to a subclass type.
        - **Explicit** and must be checked for safety using `instanceof`.
        - **Example**: `Animal → Dog`.
    
    ---
    
    ### **Examples of Object Casting**
    
    ### **Upcasting (Implicit)**
    
    ```java
    class Animal {
        void eat() {
            System.out.println("This animal eats food.");
        }
    }
    
    class Dog extends Animal {
        void bark() {
            System.out.println("The dog barks.");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Dog dog = new Dog();
    
            // Upcasting: Dog → Animal
            Animal animal = dog; // Implicit casting
            animal.eat(); // Output: This animal eats food.
        }
    }
    
    ```
    
    ### **Downcasting (Explicit)**
    
    ```java
    public class Main {
        public static void main(String[] args) {
            Animal animal = new Dog(); // Upcasting
    
            // Downcasting: Animal → Dog
            if (animal instanceof Dog) {
                Dog dog = (Dog) animal; // Explicit casting
                dog.bark(); // Output: The dog barks.
            }
        }
    }
    
    ```
    
    ---
    
    ### **3. `instanceof` Operator**
    
    The `instanceof` operator checks if an object is an instance of a specific class or subclass.
    
    **Example**:
    
    ```java
    if (animal instanceof Dog) {
        Dog dog = (Dog) animal;
        dog.bark();
    }
    
    ```
    
    ---
    
    ### **4. Casting Between Wrapper Classes and Primitives**
    
    Java automatically performs casting between **primitive types** and their **corresponding wrapper classes** through **autoboxing** and **unboxing**.
    
    ### **Autoboxing**:
    
    - Converting a primitive to a wrapper class.
    
    **Example**:
    
    ```java
    int num = 100;
    Integer wrappedNum = num; // Autoboxing
    
    ```
    
    ### **Unboxing**:
    
    - Converting a wrapper class back to a primitive.
    
    **Example**:
    
    ```java
    Integer wrappedNum = 100;
    int num = wrappedNum; // Unboxing
    
    ```
    
    ### **Example of Autoboxing and Unboxing**
    
    ```java
    public class WrapperCasting {
        public static void main(String[] args) {
            // Autoboxing
            int num = 10;
            Integer obj = num; // Primitive to wrapper
            System.out.println(obj); // Output: 10
    
            // Unboxing
            Integer wrapped = new Integer(20);
            int primitive = wrapped; // Wrapper to primitive
            System.out.println(primitive); // Output: 20
        }
    }
    
    ```
    
    ---
    
    ### **5. Common Errors with Casting**
    
    ### **ClassCastException**
    
    Occurs when trying to cast an object to a type it does not belong to.
    
    **Example**:
    
    ```java
    Animal animal = new Animal();
    Dog dog = (Dog) animal; // Runtime exception: ClassCastException
    
    ```
    
    **Solution**:
    Use `instanceof` to prevent invalid casting:
    
    ```java
    if (animal instanceof Dog) {
        Dog dog = (Dog) animal;
    }
    
    ```
    
    ---
    
    ### **6. Summary of Casting in Java**
    
    | **Aspect** | **Primitive Casting** | **Object Casting** |
    | --- | --- | --- |
    | **Types** | Widening (implicit), Narrowing (explicit) | Upcasting (implicit), Downcasting (explicit) |
    | **Scope** | Between primitive data types | Between objects in an inheritance hierarchy |
    | **Safety** | Narrowing may lose data | Downcasting must use `instanceof` |
    | **Examples** | `(int) 4.5 → 4`, `10 → 10.0` | `Animal → Dog`, `Dog → Animal` |

---

### **Collections**

1. **Overview of Collections API**
    
    ### **1. Key Features of Collections API**
    
    1. **Unified Framework**:
        - A common interface for all collections (e.g., `List`, `Set`, `Map`).
    2. **Dynamic Data Management**:
        - Collections can dynamically grow or shrink in size.
    3. **Versatile Data Structures**:
        - Supports a variety of structures like lists, sets, queues, and maps.
    4. **Utility Methods**:
        - Offers methods for sorting, searching, shuffling, and more.
    5. **Type Safety with Generics**:
        - Provides compile-time type checking, reducing runtime errors.
    
    ---
    
    ### **2. Core Interfaces in the Collections Framework**
    
    | **Interface** | **Description** |
    | --- | --- |
    | **Collection** | Base interface for all collection types. |
    | **List** | An ordered collection that allows duplicates. |
    | **Set** | A collection that does not allow duplicate elements. |
    | **Queue** | A collection that follows FIFO (First-In-First-Out) or other queuing principles. |
    | **Deque** | A double-ended queue that supports insertion and removal at both ends. |
    | **Map** | A collection that maps keys to values (not part of the `Collection` interface). |
    
    ---
    
    ### **3. Comparing Core Collection Types**
    
    | **Collection** | **Duplicates** | **Order Maintained** | **Implementation** | **Example Use** |
    | --- | --- | --- | --- | --- |
    | `List` | Yes | Yes | `ArrayList`, `LinkedList` | Ordered list of items |
    | `Set` | No | Optional | `HashSet`, `TreeSet` | Unique elements, fast lookups |
    | `Map` | Keys: No | Optional | `HashMap`, `TreeMap` | Key-value pairs |
    | `Queue` | Yes | Yes (FIFO) | `PriorityQueue`, `ArrayDeque` | Processing items in order |
    
    ---
    
    ### **4. Benefits of the Collections Framework**
    
    1. **Performance**:
        - Optimized implementations for different data structures.
    2. **Type Safety**:
        - Generics enforce compile-time checks.
    3. **Reusability**:
        - Standardized implementations reduce boilerplate code.
    4. **Extensibility**:
        - Custom collections can be created by implementing core interfaces.
    
    ---
    
2. **List, Set, Map interfaces**
    
    ### **List, Set, and Map Interfaces in Java**
    
    The **`List`**, **`Set`**, and **`Map`** interfaces are core parts of the **Java Collections Framework**, designed to store and manipulate groups of objects efficiently. Each interface serves a specific purpose and offers unique functionalities.
    
    ---
    
    ### **1. `List` Interface**
    
    The **`List`** interface represents an ordered collection (also known as a sequence) that allows duplicate elements. Elements can be accessed by their **index**.
    
    ### **Key Features**:
    
    - **Order Maintained**: Elements retain their insertion order.
    - **Duplicates Allowed**: Can store multiple instances of the same value.
    - **Indexed Access**: Provides methods to get, add, and remove elements by index.
    
    ### **Common Implementations**:
    
    1. **`ArrayList`**:
        - Backed by a dynamic array.
        - Fast random access; slower insertions/removals in the middle.
        - Best for: Frequent access operations.
    2. **`LinkedList`**:
        - Backed by a doubly linked list.
        - Fast insertions/removals; slower random access.
        - Best for: Frequent additions/deletions.
    3. **`Vector`** (Legacy):
        - Synchronized version of `ArrayList`.
    
    ### **Key Methods**:
    
    | **Method** | **Description** |
    | --- | --- |
    | `add(E element)` | Adds an element to the list. |
    | `add(int index, E element)` | Adds an element at a specific index. |
    | `get(int index)` | Returns the element at a specified index. |
    | `remove(int index)` | Removes the element at a specified index. |
    | `indexOf(Object o)` | Returns the index of the first occurrence of the element. |
    | `size()` | Returns the number of elements in the list. |
    
    ### **Example**:
    
    ```java
    import java.util.ArrayList;
    import java.util.List;
    
    public class ListExample {
        public static void main(String[] args) {
            List<String> list = new ArrayList<>();
            list.add("A");
            list.add("B");
            list.add("A"); // Duplicates allowed
    
            System.out.println(list); // Output: [A, B, A]
            System.out.println(list.get(1)); // Output: B
        }
    }
    
    ```
    
    ---
    
    ### **2. `Set` Interface**
    
    The **`Set`** interface represents a collection that **does not allow duplicate elements**. It is a mathematical set.
    
    ### **Key Features**:
    
    - **No Duplicates**: Ensures unique elements.
    - **No Indexed Access**: Elements cannot be accessed by index.
    - **Order Varies**:
        - **Unordered**: `HashSet`.
        - **Insertion Order**: `LinkedHashSet`.
        - **Sorted**: `TreeSet`.
    
    ### **Common Implementations**:
    
    1. **`HashSet`**:
        - Backed by a hash table.
        - Best for: Fast lookups and unique collections.
        - Unordered.
    2. **`LinkedHashSet`**:
        - Backed by a hash table and a linked list.
        - Best for: Maintaining insertion order.
    3. **`TreeSet`**:
        - Backed by a red-black tree.
        - Best for: Automatically sorted collections.
    
    ### **Key Methods**:
    
    | **Method** | **Description** |
    | --- | --- |
    | `add(E element)` | Adds an element to the set. |
    | `remove(Object o)` | Removes an element from the set. |
    | `contains(Object o)` | Checks if the set contains a specific element. |
    | `size()` | Returns the number of elements in the set. |
    
    ### **Example**:
    
    ```java
    import java.util.HashSet;
    import java.util.Set;
    
    public class SetExample {
        public static void main(String[] args) {
            Set<String> set = new HashSet<>();
            set.add("A");
            set.add("B");
            set.add("A"); // Duplicate, ignored
    
            System.out.println(set); // Output: [A, B] (order may vary)
        }
    }
    
    ```
    
    ---
    
    ### **3. `Map` Interface**
    
    The **`Map`** interface represents a collection of **key-value pairs**, where keys are unique, but values can be duplicated.
    
    ### **Key Features**:
    
    - **Key-Value Pair Storage**: Each key maps to one value.
    - **Keys Must Be Unique**: No duplicate keys allowed.
    - **Values Can Be Duplicated**.
    
    ### **Common Implementations**:
    
    1. **`HashMap`**:
        - Backed by a hash table.
        - Unordered.
        - Best for: Fast lookups and key-value storage.
    2. **`LinkedHashMap`**:
        - Maintains insertion order.
        - Best for: Preserving order with key-value pairs.
    3. **`TreeMap`**:
        - Backed by a red-black tree.
        - Best for: Automatically sorted keys.
    
    ### **Key Methods**:
    
    | **Method** | **Description** |
    | --- | --- |
    | `put(K key, V value)` | Adds a key-value pair to the map. |
    | `get(Object key)` | Returns the value associated with the key. |
    | `remove(Object key)` | Removes the key-value pair for the specified key. |
    | `containsKey(Object key)` | Checks if the map contains the specified key. |
    | `containsValue(Object value)` | Checks if the map contains the specified value. |
    | `size()` | Returns the number of key-value pairs in the map. |
    
    ### **Example**:
    
    ```java
    import java.util.HashMap;
    import java.util.Map;
    
    public class MapExample {
        public static void main(String[] args) {
            Map<String, Integer> map = new HashMap<>();
            map.put("A", 1);
            map.put("B", 2);
            map.put("A", 3); // Overwrites the value for key "A"
    
            System.out.println(map); // Output: {A=3, B=2}
            System.out.println(map.get("A")); // Output: 3
        }
    }
    
    ```
    
    ---
    
    ### **4. Comparison Table**
    
    | **Aspect** | **List** | **Set** | **Map** |
    | --- | --- | --- | --- |
    | **Duplicates** | Allowed | Not Allowed | Keys: Not Allowed, Values: Allowed |
    | **Order** | Maintains insertion order | Unordered (`HashSet`), Ordered (`TreeSet`) | Depends on implementation (`HashMap` unordered, `TreeMap` sorted). |
    | **Indexed Access** | Yes | No | Keys/Values via `get(key)`. |
    | **Implementations** | `ArrayList`, `LinkedList` | `HashSet`, `TreeSet` | `HashMap`, `TreeMap` |
    | **Use Case** | Ordered, allows duplicates. | Unique, fast lookups. | Key-value storage. |
    
    ---
    
    ### **5. When to Use Each**
    
    - **List**:
        - When you need an ordered collection.
        - Use `ArrayList` for frequent reads and `LinkedList` for frequent inserts/deletes.
    - **Set**:
        - When you need a unique collection of elements.
        - Use `HashSet` for fast lookups and `TreeSet` for sorted collections.
    - **Map**:
        - When you need key-value associations.
        - Use `HashMap` for fast access and `TreeMap` for sorted keys.
    
    ---
    
3. **Wrapper classes and Generics**
    
    ### **Wrapper Classes and Generics in Java**
    
    Java's **Wrapper Classes** and **Generics** are integral features that enhance the flexibility, type safety, and performance of the Java programming language.
    
    ---
    
    ## **1. Wrapper Classes**
    
    Wrapper classes are used to wrap primitive data types (`int`, `double`, etc.) into objects. This enables primitives to be used in contexts where objects are required, such as in **collections** or **generics**.
    
    ### **1.1 Wrapper Classes for Primitive Types**
    
    | **Primitive Type** | **Wrapper Class** |
    | --- | --- |
    | `byte` | `Byte` |
    | `short` | `Short` |
    | `int` | `Integer` |
    | `long` | `Long` |
    | `float` | `Float` |
    | `double` | `Double` |
    | `char` | `Character` |
    | `boolean` | `Boolean` |
    
    ### **1.2 Why Use Wrapper Classes?**
    
    1. **Collections**: Collections in Java require objects, not primitives.
        
        ```java
        List<Integer> numbers = new ArrayList<>(); // Cannot use List<int>
        
        ```
        
    2. **Generics**: Generics only work with reference types (e.g., `Integer` instead of `int`).
    3. **Utilities**: Wrapper classes provide utility methods (e.g., `Integer.parseInt()`).
    
    ---
    
    ### **1.3 Autoboxing and Unboxing**
    
    **Autoboxing**: Automatic conversion of a primitive to its corresponding wrapper class.
    
    **Unboxing**: Automatic conversion of a wrapper class to its corresponding primitive.
    
    ### **Example of Autoboxing and Unboxing**:
    
    ```java
    public class WrapperExample {
        public static void main(String[] args) {
            // Autoboxing: Primitive to Wrapper
            Integer num = 10;
    
            // Unboxing: Wrapper to Primitive
            int n = num;
    
            System.out.println(num); // Output: 10
            System.out.println(n);   // Output: 10
        }
    }
    
    ```
    
    ---
    
    ## **2. Generics**
    
    Generics allow you to parameterize types, making code more flexible and type-safe. They were introduced in Java 5 to eliminate the need for casting and to catch type errors at compile time.
    
    ### **2.1 Why Use Generics?**
    
    1. **Type Safety**:
        - Ensures that only compatible types are added to collections or methods.
        - Prevents `ClassCastException` at runtime.
    2. **Eliminates Casting**:
        - Avoids explicit type casting when retrieving objects from collections.
    3. **Reusability**:
        - Allows classes and methods to work with different data types.
    
    ---
    
    ### **2.2 Syntax of Generics**
    
    **Defining a Generic Class**:
    
    ```java
    class Box<T> {
        private T item;
    
        public void setItem(T item) {
            this.item = item;
        }
    
        public T getItem() {
            return item;
        }
    }
    
    ```
    
    **Using a Generic Class**:
    
    ```java
    public class GenericExample {
        public static void main(String[] args) {
            Box<String> stringBox = new Box<>();
            stringBox.setItem("Hello");
            System.out.println(stringBox.getItem()); // Output: Hello
    
            Box<Integer> intBox = new Box<>();
            intBox.setItem(100);
            System.out.println(intBox.getItem()); // Output: 100
        }
    }
    
    ```
    
    ---
    
    ### **2.3 Generics in Collections**
    
    **Before Generics (Java 1.4)**:
    
    ```java
    List list = new ArrayList();
    list.add("Hello");
    String s = (String) list.get(0); // Requires casting
    
    ```
    
    **With Generics (Java 5+)**:
    
    ```java
    List<String> list = new ArrayList<>();
    list.add("Hello");
    // No casting required
    String s = list.get(0);
    
    ```
    
    ---
    
    ### **2.4 Bounded Generics**
    
    Generics can be restricted to a specific range of types using **bounds**.
    
    ### **Upper Bound (`extends`)**:
    
    Allows the generic to accept a type or its subclasses.
    
    ```java
    class Box<T extends Number> {
        private T value;
    }
    
    ```
    
    **Example**:
    
    ```java
    Box<Integer> box1 = new Box<>();
    Box<Double> box2 = new Box<>();
    // Box<String> box3 = new Box<>(); // Compilation error
    
    ```
    
    ### **Lower Bound (`super`)**:
    
    Allows the generic to accept a type or its superclasses.
    
    ```java
    public static void print(List<? super Integer> list) {
        for (Object obj : list) {
            System.out.println(obj);
        }
    }
    
    ```
    
    ---
    
    ### **2.5 Wildcards in Generics**
    
    Wildcards (`?`) are used when you don’t know or want to restrict the type.
    
    | **Wildcard** | **Description** |
    | --- | --- |
    | `<?>` | Accepts any type. |
    | `<? extends Type>` | Accepts `Type` or its subclasses. |
    | `<? super Type>` | Accepts `Type` or its superclasses. |
    
    ### **Example**:
    
    ```java
    public static void printList(List<?> list) {
        for (Object item : list) {
            System.out.println(item);
        }
    }
    
    List<String> strings = Arrays.asList("A", "B", "C");
    printList(strings); // Output: A, B, C
    
    ```
    
    ---
    
    ### **2.6 Generics in Methods**
    
    Generics can also be applied to methods.
    
    **Syntax**:
    
    ```java
    public static <T> void printArray(T[] array) {
        for (T item : array) {
            System.out.println(item);
        }
    }
    
    ```
    
    **Example**:
    
    ```java
    public class GenericMethodExample {
        public static <T> void printArray(T[] array) {
            for (T element : array) {
                System.out.println(element);
            }
        }
    
        public static void main(String[] args) {
            String[] words = {"Java", "Generics"};
            Integer[] numbers = {1, 2, 3};
    
            printArray(words);   // Output: Java, Generics
            printArray(numbers); // Output: 1, 2, 3
        }
    }
    
    ```
    
    ---
    
    ## **3. Comparison: Wrapper Classes vs. Generics**
    
    | **Aspect** | **Wrapper Classes** | **Generics** |
    | --- | --- | --- |
    | **Purpose** | Wraps primitives into objects. | Provides type safety and flexibility. |
    | **Type of Data** | Works with primitive and reference types. | Works with reference types only. |
    | **Autoboxing/Unboxing** | Converts primitives to objects and vice versa. | Not applicable. |
    | **Example Use** | Collections (e.g., `List<Integer>`). | Parameterizing data types in collections. |
    
    ---
    
    ### **4. Key Differences Between Wrapper Classes and Generics**
    
    | **Feature** | **Wrapper Classes** | **Generics** |
    | --- | --- | --- |
    | **Focus** | Enables primitives to act as objects. | Adds type safety to collections and classes. |
    | **Relation to Primitives** | Tightly related (via autoboxing/unboxing). | Unrelated (requires reference types). |
    | **Usage** | `Integer`, `Double`, etc. | `<T>`, `<E>`, `<K, V>` |
    
    ---
    
    ### **Summary**
    
    - **Wrapper Classes**: Allow primitives to behave as objects, making them compatible with Java's object-oriented features.
    - **Generics**: Enable type safety, reusability, and flexibility, especially in collections and custom classes.
    
    ---
    
4. **Queue, Stacks (LIFO vs FIFO)**
    
    ### **Queue and Stack in Java (FIFO vs. LIFO)**
    
    **Queues** and **Stacks** are fundamental data structures in Java, and they follow different principles for organizing and accessing elements:
    
    - **Queue**: Follows the **FIFO** (First In, First Out) principle.
    - **Stack**: Follows the **LIFO** (Last In, First Out) principle.
    
    ---
    
    ## **1. Stack**
    
    A **stack** is a collection where elements are added and removed from the **top**. It follows the **LIFO** principle:
    
    - **Last In**: The last element added is the first one to be removed.
    - **First Out**: The element added most recently is accessed first.
    
    ### **1.1 Common Operations**
    
    | **Operation** | **Description** | **Method in Java** |
    | --- | --- | --- |
    | `push` | Adds an element to the top of the stack. | `stack.push(element)` |
    | `pop` | Removes the top element from the stack. | `stack.pop()` |
    | `peek` | Returns the top element without removing it. | `stack.peek()` |
    | `isEmpty` | Checks if the stack is empty. | `stack.isEmpty()` |
    
    ---
    
    ### **1.2 Implementation in Java**
    
    ### **Using the `Stack` Class**
    
    The `Stack` class is part of the `java.util` package.
    
    **Example**:
    
    ```java
    import java.util.Stack;
    
    public class StackExample {
        public static void main(String[] args) {
            Stack<Integer> stack = new Stack<>();
    
            // Push elements
            stack.push(10);
            stack.push(20);
            stack.push(30);
    
            // Peek the top element
            System.out.println("Top element: " + stack.peek()); // Output: 30
    
            // Pop elements
            System.out.println("Popped: " + stack.pop()); // Output: 30
            System.out.println("Popped: " + stack.pop()); // Output: 20
    
            // Check if stack is empty
            System.out.println("Is stack empty? " + stack.isEmpty()); // Output: false
        }
    }
    
    ```
    
    ---
    
    ## **2. Queue**
    
    A **queue** is a collection where elements are added at the **end** and removed from the **front**. It follows the **FIFO** principle:
    
    - **First In**: The first element added is the first one to be removed.
    - **First Out**: The earliest added element is accessed first.
    
    ### **2.1 Common Operations**
    
    | **Operation** | **Description** | **Method in Java** |
    | --- | --- | --- |
    | `add`/`offer` | Adds an element to the end of the queue. | `queue.add(element)` or `queue.offer(element)` |
    | `remove`/`poll` | Removes the front element from the queue. | `queue.remove()` or `queue.poll()` |
    | `peek` | Returns the front element without removing it. | `queue.peek()` |
    | `isEmpty` | Checks if the queue is empty. | `queue.isEmpty()` |
    
    ---
    
    ### **2.2 Implementation in Java**
    
    ### **Using the `Queue` Interface**
    
    The `Queue` interface is implemented by classes like `LinkedList` and `PriorityQueue`.
    
    **Example**:
    
    ```java
    import java.util.LinkedList;
    import java.util.Queue;
    
    public class QueueExample {
        public static void main(String[] args) {
            Queue<Integer> queue = new LinkedList<>();
    
            // Add elements
            queue.add(10);
            queue.add(20);
            queue.add(30);
    
            // Peek the front element
            System.out.println("Front element: " + queue.peek()); // Output: 10
    
            // Remove elements
            System.out.println("Removed: " + queue.poll()); // Output: 10
            System.out.println("Removed: " + queue.poll()); // Output: 20
    
            // Check if queue is empty
            System.out.println("Is queue empty? " + queue.isEmpty()); // Output: false
        }
    }
    
    ```
    
    ---
    
    ### **3. Key Differences Between Stack and Queue**
    
    | **Aspect** | **Stack** | **Queue** |
    | --- | --- | --- |
    | **Principle** | LIFO (Last In, First Out) | FIFO (First In, First Out) |
    | **Access** | Accesses the most recently added item. | Accesses the earliest added item. |
    | **Implementation** | `Stack` class. | `Queue` interface (e.g., `LinkedList`, `PriorityQueue`). |
    | **Use Cases** | Function calls, undo operations, DFS. | Task scheduling, BFS, message queues. |
    
    ---
    
    ### **4. Variants of Queue**
    
    ### **a. Priority Queue**
    
    - Elements are ordered based on their priority rather than insertion order.
    - Implemented using `PriorityQueue`.
    
    **Example**:
    
    ```java
    import java.util.PriorityQueue;
    
    public class PriorityQueueExample {
        public static void main(String[] args) {
            PriorityQueue<Integer> pq = new PriorityQueue<>();
    
            pq.add(30);
            pq.add(10);
            pq.add(20);
    
            System.out.println(pq.poll()); // Output: 10 (lowest priority first)
        }
    }
    
    ```
    
    ### **b. Deque (Double-Ended Queue)**
    
    - Supports insertion and removal at both ends.
    - Implemented using `ArrayDeque`.
    
    **Example**:
    
    ```java
    import java.util.ArrayDeque;
    
    public class DequeExample {
        public static void main(String[] args) {
            ArrayDeque<Integer> deque = new ArrayDeque<>();
    
            deque.addFirst(10); // Adds to the front
            deque.addLast(20);  // Adds to the end
    
            System.out.println(deque.pollFirst()); // Output: 10
            System.out.println(deque.pollLast());  // Output: 20
        }
    }
    
    ```
    
    ---
    
    ### **5. Use Cases**
    
    | **Data Structure** | **Use Cases** |
    | --- | --- |
    | **Stack** | Function calls, Undo/Redo operations, DFS. |
    | **Queue** | Task scheduling, BFS, Print job management. |
    | **Priority Queue** | Pathfinding algorithms, job/task prioritization. |
    | **Deque** | Palindrome checking, sliding window problems. |
    
    ---
    
5. **Iterators**
    
    ### **Iterators in Java**
    
    An **iterator** is an object in Java that provides a standardized way to traverse elements of a collection (e.g., `List`, `Set`, or `Map`). Iterators are part of the **Java Collections Framework** and are defined in the `java.util` package.
    
    ---
    
    ### **1. Key Features of Iterators**
    
    1. **Unified Traversal**:
        - Provides a consistent way to iterate through elements of different types of collections.
    2. **Fail-Fast Behavior**:
        - Detects concurrent modifications of the collection during iteration and throws a `ConcurrentModificationException`.
    3. **Read and Remove**:
        - Iterators can retrieve elements and optionally remove them during traversal.
    4. **Type Safety with Generics**:
        - Iterator objects can be type-safe by using generics.
    
    ---
    
    ### **2. Iterator Interface**
    
    The `Iterator` interface provides the following key methods:
    
    | **Method** | **Description** |
    | --- | --- |
    | `boolean hasNext()` | Returns `true` if there are more elements to iterate. |
    | `E next()` | Returns the next element in the iteration. |
    | `void remove()` | Removes the last element returned by the iterator. |
    
    ---
    
    ### **3. How to Use an Iterator**
    
    ### **Example with a `List`**
    
    ```java
    import java.util.ArrayList;
    import java.util.Iterator;
    import java.util.List;
    
    public class IteratorExample {
        public static void main(String[] args) {
            List<String> list = new ArrayList<>();
            list.add("A");
            list.add("B");
            list.add("C");
    
            Iterator<String> iterator = list.iterator();
    
            while (iterator.hasNext()) {
                String element = iterator.next();
                System.out.println(element); // Output: A, B, C
            }
        }
    }
    
    ```
    
    ### **Removing Elements with Iterator**
    
    The `remove()` method removes the last element returned by `next()`. It should only be called after a call to `next()`.
    
    ```java
    import java.util.ArrayList;
    import java.util.Iterator;
    import java.util.List;
    
    public class IteratorRemoveExample {
        public static void main(String[] args) {
            List<String> list = new ArrayList<>();
            list.add("A");
            list.add("B");
            list.add("C");
    
            Iterator<String> iterator = list.iterator();
    
            while (iterator.hasNext()) {
                String element = iterator.next();
                if (element.equals("B")) {
                    iterator.remove(); // Removes "B" from the list
                }
            }
    
            System.out.println(list); // Output: [A, C]
        }
    }
    
    ```
    
    ---
    
    ### **4. Enhanced For-Loop vs. Iterator**
    
    The **enhanced for-loop** is a simplified syntax for iteration but does not allow element removal during traversal.
    
    **Example**:
    
    ```java
    for (String element : list) {
        System.out.println(element);
    }
    
    ```
    
    **Comparison**:
    
    | **Aspect** | **Iterator** | **Enhanced For-Loop** |
    | --- | --- | --- |
    | **Control** | Can manually control traversal. | Automatic traversal of all elements. |
    | **Element Removal** | Supports removal using `remove()`. | Does not support element removal. |
    | **Usability** | More verbose. | Concise syntax. |
    
    ---
    
    ### **5. ListIterator**
    
    The **`ListIterator`** is a specialized iterator for `List` collections. It provides additional methods for bi-directional traversal and element modification.
    
    ### **Key Methods of `ListIterator`**
    
    | **Method** | **Description** |
    | --- | --- |
    | `hasPrevious()` | Returns `true` if there are elements before the current one. |
    | `previous()` | Returns the previous element. |
    | `add(E e)` | Inserts an element at the current position. |
    | `set(E e)` | Replaces the last element returned by `next()` or `previous()`. |
    
    ### **Example with `ListIterator`**
    
    ```java
    import java.util.ArrayList;
    import java.util.List;
    import java.util.ListIterator;
    
    public class ListIteratorExample {
        public static void main(String[] args) {
            List<String> list = new ArrayList<>();
            list.add("A");
            list.add("B");
            list.add("C");
    
            ListIterator<String> listIterator = list.listIterator();
    
            while (listIterator.hasNext()) {
                System.out.println(listIterator.next()); // Output: A, B, C
            }
    
            while (listIterator.hasPrevious()) {
                System.out.println(listIterator.previous()); // Output: C, B, A
            }
        }
    }
    
    ```
    
    ---
    
    ### **6. Iterators for `Map`**
    
    Since `Map` does not implement the `Iterable` interface directly, you need to obtain an iterator from its **entry set**, **key set**, or **values** collection.
    
    ### **Example of Iterating a `Map`**
    
    ```java
    import java.util.HashMap;
    import java.util.Iterator;
    import java.util.Map;
    
    public class MapIteratorExample {
        public static void main(String[] args) {
            Map<String, Integer> map = new HashMap<>();
            map.put("A", 1);
            map.put("B", 2);
            map.put("C", 3);
    
            // Using entrySet() iterator
            Iterator<Map.Entry<String, Integer>> iterator = map.entrySet().iterator();
    
            while (iterator.hasNext()) {
                Map.Entry<String, Integer> entry = iterator.next();
                System.out.println(entry.getKey() + ": " + entry.getValue());
            }
        }
    }
    
    ```
    

---

### **OOP Pillars**

1. **Inheritance**
    
    ### **Inheritance in Java**
    
    **Inheritance** is a core feature of object-oriented programming (OOP) that allows one class (called the **subclass**) to inherit fields and methods from another class (called the **superclass**). This enables **code reuse**, **hierarchical classification**, and the extension of existing code.
    
    ---
    
    ### **1. Key Concepts of Inheritance**
    
    1. **Superclass (Parent Class)**:
        - The class whose fields and methods are inherited.
    2. **Subclass (Child Class)**:
        - The class that inherits fields and methods from the superclass.
        - Can override or extend the functionality of the superclass.
    3. **`extends` Keyword**:
        - Used to define a subclass.
        - Example:
            
            ```java
            class Animal {
                void eat() {
                    System.out.println("This animal eats food.");
                }
            }
            
            class Dog extends Animal {
                void bark() {
                    System.out.println("The dog barks.");
                }
            }
            
            ```
            
    
    ---
    
    ### **2. Syntax**
    
    ```java
    class Superclass {
        // Fields and methods
    }
    
    class Subclass extends Superclass {
        // Additional fields and methods
    }
    
    ```
    
    ---
    
    ### **3. Example of Inheritance**
    
    ```java
    class Animal {
        void eat() {
            System.out.println("This animal eats food.");
        }
    }
    
    class Dog extends Animal {
        void bark() {
            System.out.println("The dog barks.");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Dog dog = new Dog();
            dog.eat();  // Inherited from Animal
            dog.bark(); // Defined in Dog
        }
    }
    
    ```
    
    **Output**:
    
    ```
    This animal eats food.
    The dog barks.
    
    ```
    
    ---
    
    ### **4. Types of Inheritance in Java**
    
    1. **Single Inheritance**:
        - One subclass inherits from one superclass.
        - Example:
            
            ```java
            class Animal { }
            class Dog extends Animal { }
            
            ```
            
    2. **Multilevel Inheritance**:
        - A subclass acts as a superclass for another class.
        - Example:
            
            ```java
            class Animal { }
            class Dog extends Animal { }
            class Puppy extends Dog { }
            
            ```
            
    3. **Hierarchical Inheritance**:
        - Multiple subclasses inherit from a single superclass.
        - Example:
            
            ```java
            class Animal { }
            class Dog extends Animal { }
            class Cat extends Animal { }
            
            ```
            
    4. **Hybrid Inheritance** (Not Supported):
        - A combination of multiple inheritance types. Java does not support multiple inheritance with classes to avoid ambiguity. Instead, it uses **interfaces**.
    
    ---
    
    ### **5. Overriding Methods**
    
    A subclass can provide its own implementation for a method defined in the superclass. This is known as **method overriding**.
    
    ### **Rules for Method Overriding**:
    
    1. The method in the subclass must have the same signature as in the superclass.
    2. The return type must be the same or a subtype (covariant return).
    3. The access modifier cannot be more restrictive than the superclass method.
    4. The method cannot be marked `final` in the superclass.
    
    **Example**:
    
    ```java
    class Animal {
        void sound() {
            System.out.println("This animal makes a sound.");
        }
    }
    
    class Dog extends Animal {
        @Override
        void sound() {
            System.out.println("The dog barks.");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Animal animal = new Dog();
            animal.sound(); // Output: The dog barks.
        }
    }
    
    ```
    
    ---
    
    ### **6. `super` Keyword**
    
    The `super` keyword is used to refer to the immediate superclass.
    
    1. **Access Superclass Methods**:
        
        ```java
        class Animal {
            void sound() {
                System.out.println("This animal makes a sound.");
            }
        }
        
        class Dog extends Animal {
            void sound() {
                super.sound(); // Calls the superclass method
                System.out.println("The dog barks.");
            }
        }
        
        ```
        
    2. **Access Superclass Constructor**:
        
        ```java
        class Animal {
            Animal() {
                System.out.println("Animal constructor called.");
            }
        }
        
        class Dog extends Animal {
            Dog() {
                super(); // Calls the superclass constructor
                System.out.println("Dog constructor called.");
            }
        }
        
        ```
        
    
    ---
    
    ### **7. Access Modifiers and Inheritance**
    
    | **Access Modifier** | **Same Class** | **Same Package** | **Different Package (Subclass)** | **Other Classes** |
    | --- | --- | --- | --- | --- |
    | `public` | ✅ | ✅ | ✅ | ✅ |
    | `protected` | ✅ | ✅ | ✅ | ❌ |
    | (Default) | ✅ | ✅ | ❌ | ❌ |
    | `private` | ✅ | ❌ | ❌ | ❌ |
    
    ---
    
    ### **8. Polymorphism and Inheritance**
    
    Using inheritance, you can achieve **runtime polymorphism**, where a superclass reference can hold a subclass object and invoke overridden methods.
    
    **Example**:
    
    ```java
    class Animal {
        void sound() {
            System.out.println("This animal makes a sound.");
        }
    }
    
    class Dog extends Animal {
        @Override
        void sound() {
            System.out.println("The dog barks.");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Animal animal = new Dog(); // Polymorphism
            animal.sound(); // Output: The dog barks.
        }
    }
    
    ```
    
    ---
    
    ### **9. Advantages of Inheritance**
    
    1. **Code Reusability**:
        - Common functionality can be written once in the superclass and reused by subclasses.
    2. **Code Maintenance**:
        - Changes in the superclass automatically propagate to subclasses.
    3. **Polymorphism**:
        - Allows flexibility in designing and extending the program.
    4. **Extensibility**:
        - Easily add new functionality by creating subclasses.
    
    ---
    
    ### **10. Disadvantages of Inheritance**
    
    1. **Tight Coupling**:
        - Subclasses are tightly coupled to the superclass, making changes more impactful.
    2. **Overhead**:
        - Too much inheritance can lead to a complex hierarchy.
    3. **Not Always Appropriate**:
        - Composition might be a better alternative in some scenarios.
    
    ---
    
    ### **11. When to Use Inheritance**
    
    - Use inheritance when:
        1. A subclass is a **"type of"** the superclass (e.g., `Dog` is a type of `Animal`).
        2. Code reuse and extension of existing functionality are required.
    - Avoid inheritance when:
        1. Classes are unrelated.
        2. You need to achieve code reuse but not hierarchical relationships (use **composition** instead).
    
    ---
    
    ### **12. Comparison of Inheritance with Composition**
    
    | **Aspect** | **Inheritance** | **Composition** |
    | --- | --- | --- |
    | **Relationship** | "is-a" | "has-a" |
    | **Coupling** | Tightly coupled | Loosely coupled |
    | **Reuse** | Uses existing functionality | Uses delegation |
    | **Flexibility** | Less flexible (single inheritance). | More flexible. |
    
    ---
    
2. **Polymorphism (Overloading and Overriding)**
    
    ### **Polymorphism in Java**
    
    **Polymorphism** is a core concept of Object-Oriented Programming (OOP) that allows one name to have multiple forms. It enables objects to behave differently based on their context. There are two types of polymorphism in Java:
    
    1. **Compile-Time Polymorphism (Method Overloading)**
    2. **Runtime Polymorphism (Method Overriding)**
    
    ---
    
    ### **1. Compile-Time Polymorphism (Method Overloading)**
    
    **Method Overloading** occurs when multiple methods in the same class share the same name but have different parameter lists (type, number, or both). The method to execute is determined at **compile time**.
    
    ### **Rules for Method Overloading**
    
    1. Methods must have the same name.
    2. Methods must differ in their parameter list (number, type, or both).
    3. Return type can be different but is not used to distinguish methods.
    
    ### **Example of Method Overloading**:
    
    ```java
    class Calculator {
        // Overloaded methods
        int add(int a, int b) {
            return a + b;
        }
    
        double add(double a, double b) {
            return a + b;
        }
    
        int add(int a, int b, int c) {
            return a + b + c;
        }
    }
    
    public class OverloadingExample {
        public static void main(String[] args) {
            Calculator calc = new Calculator();
    
            System.out.println(calc.add(2, 3));         // Output: 5
            System.out.println(calc.add(2.5, 3.5));     // Output: 6.0
            System.out.println(calc.add(1, 2, 3));      // Output: 6
        }
    }
    
    ```
    
    ### **Benefits of Method Overloading**
    
    - Improves code readability by grouping related operations.
    - Simplifies method naming, avoiding clutter in the class.
    
    ---
    
    ### **2. Runtime Polymorphism (Method Overriding)**
    
    **Method Overriding** occurs when a subclass provides a specific implementation for a method already defined in its superclass. The method to execute is determined at **runtime** based on the actual object's type.
    
    ### **Rules for Method Overriding**
    
    1. The method in the subclass must have the same signature (name, parameters, and return type) as in the superclass.
    2. The overriding method cannot have a more restrictive access modifier than the overridden method.
    3. The method cannot be marked `final` or `static` in the superclass.
    4. The return type must be the same or a subtype (covariant return type).
    
    ---
    
    ### **Example of Method Overriding**:
    
    ```java
    class Animal {
        void sound() {
            System.out.println("This animal makes a sound.");
        }
    }
    
    class Dog extends Animal {
        @Override
        void sound() {
            System.out.println("The dog barks.");
        }
    }
    
    public class OverridingExample {
        public static void main(String[] args) {
            Animal animal = new Dog(); // Runtime Polymorphism
            animal.sound();            // Output: The dog barks.
        }
    }
    
    ```
    
    ---
    
    ### **3. Key Differences Between Overloading and Overriding**
    
    | **Aspect** | **Overloading** | **Overriding** |
    | --- | --- | --- |
    | **Definition** | Same method name, different parameter list. | Subclass redefines a method from superclass. |
    | **Determination** | Determined at compile time. | Determined at runtime. |
    | **Inheritance** | Does not require inheritance. | Requires inheritance. |
    | **Access Modifier** | Can be independent of other methods. | Cannot be more restrictive than the superclass method. |
    | **Return Type** | Can differ between overloaded methods. | Must be the same or a subtype (covariant). |
    
    ---
    
    ### **4. Usage of `super` in Overriding**
    
    The `super` keyword can be used to call a method from the superclass in the subclass.
    
    **Example**:
    
    ```java
    class Animal {
        void sound() {
            System.out.println("This animal makes a sound.");
        }
    }
    
    class Dog extends Animal {
        @Override
        void sound() {
            super.sound(); // Calls the superclass method
            System.out.println("The dog barks.");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Dog dog = new Dog();
            dog.sound();
            // Output:
            // This animal makes a sound.
            // The dog barks.
        }
    }
    
    ```
    
    ---
    
    ### **5. Covariant Return Type**
    
    In overriding, the return type of the overriding method can be a subtype of the return type declared in the superclass method.
    
    **Example**:
    
    ```java
    class Animal {
        Animal getAnimal() {
            return this;
        }
    }
    
    class Dog extends Animal {
        @Override
        Dog getAnimal() {
            return this;
        }
    }
    
    public class CovariantExample {
        public static void main(String[] args) {
            Dog dog = new Dog();
            System.out.println(dog.getAnimal().getClass().getSimpleName()); // Output: Dog
        }
    }
    
    ```
    
    ---
    
    ### **6. Practical Examples**
    
    ### **Overloading Example: Print Utility**
    
    ```java
    class Printer {
        void print(String message) {
            System.out.println("Printing message: " + message);
        }
    
        void print(int number) {
            System.out.println("Printing number: " + number);
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Printer printer = new Printer();
            printer.print("Hello, World!"); // Output: Printing message: Hello, World!
            printer.print(123);            // Output: Printing number: 123
        }
    }
    
    ```
    
    ### **Overriding Example: Payment Processing**
    
    ```java
    class Payment {
        void processPayment() {
            System.out.println("Processing generic payment.");
        }
    }
    
    class CreditCardPayment extends Payment {
        @Override
        void processPayment() {
            System.out.println("Processing credit card payment.");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Payment payment = new CreditCardPayment(); // Runtime polymorphism
            payment.processPayment(); // Output: Processing credit card payment.
        }
    }
    
    ```
    
    ---
    
    ### **7. Benefits of Polymorphism**
    
    1. **Code Reusability**:
        - Common code can reside in the superclass while subclasses handle specifics.
    2. **Flexibility**:
        - A single method call can behave differently depending on the object's type.
    3. **Extensibility**:
        - Easily extend existing systems by adding new subclasses.
    
    ---
    
    ### **8. Summary Table**
    
    | **Aspect** | **Method Overloading** | **Method Overriding** |
    | --- | --- | --- |
    | **Polymorphism Type** | Compile-time polymorphism. | Runtime polymorphism. |
    | **Class Relationship** | Same class. | Requires inheritance. |
    | **Use Case** | Method with the same name but different parameters. | Customize or replace superclass methods. |
    | **Determination** | At compile time. | At runtime. |
    
    ---
    
3. **Encapsulation and Abstraction**
    
    ### **Encapsulation and Abstraction in Java**
    
    **Encapsulation** and **Abstraction** are core principles of Object-Oriented Programming (OOP) in Java. They are designed to make software modular, maintainable, and secure by controlling access to data and hiding implementation details.
    
    ---
    
    ## **1. Encapsulation**
    
    **Encapsulation** is the process of wrapping data (fields) and methods (behaviors) together into a single unit (class). It restricts direct access to the internal state of the object and exposes it through public methods, ensuring control over data integrity.
    
    ---
    
    ### **Key Features of Encapsulation**
    
    1. **Data Hiding**:
        - Internal details of the object are hidden from the outside world.
        - Achieved by using private fields and providing public getters and setters.
    2. **Control Access**:
        - Only the methods of the class can directly access or modify the fields, ensuring controlled access.
    3. **Improves Maintainability**:
        - Encapsulation makes it easier to modify or debug the code without affecting other parts of the application.
    
    ---
    
    ### **How to Implement Encapsulation**
    
    1. **Declare fields as `private`.**
    2. **Provide public getter and setter methods** to access and update the fields.
    
    ---
    
    ### **Example of Encapsulation**
    
    ```java
    class Employee {
        // Private fields
        private String name;
        private double salary;
    
        // Getter for name
        public String getName() {
            return name;
        }
    
        // Setter for name
        public void setName(String name) {
            this.name = name;
        }
    
        // Getter for salary
        public double getSalary() {
            return salary;
        }
    
        // Setter for salary
        public void setSalary(double salary) {
            if (salary > 0) { // Validation
                this.salary = salary;
            } else {
                System.out.println("Salary must be positive.");
            }
        }
    }
    
    public class EncapsulationExample {
        public static void main(String[] args) {
            Employee emp = new Employee();
            emp.setName("John");
            emp.setSalary(50000);
    
            System.out.println("Employee Name: " + emp.getName());
            System.out.println("Employee Salary: $" + emp.getSalary());
        }
    }
    
    ```
    
    **Output**:
    
    ```
    Employee Name: John
    Employee Salary: $50000.0
    
    ```
    
    ---
    
    ### **Advantages of Encapsulation**
    
    1. **Improved Security**:
        - Fields can only be accessed and modified in controlled ways.
    2. **Code Maintainability**:
        - Makes classes easier to update without affecting other parts of the code.
    3. **Reusability**:
        - Encapsulated code can be reused with minimal impact on other components.
    
    ---
    
    ## **2. Abstraction**
    
    **Abstraction** is the process of hiding implementation details and exposing only the essential features of an object. It focuses on "what an object does" rather than "how it does it."
    
    ---
    
    ### **Key Features of Abstraction**
    
    1. **Simplified View**:
        - Reduces complexity by showing only relevant details.
    2. **Implementation Hiding**:
        - Users interact with the object through its interface, unaware of the underlying implementation.
    3. **Achieved Using**:
        - **Abstract Classes**: Provide partial abstraction.
        - **Interfaces**: Provide full abstraction.
    
    ---
    
    ### **How to Implement Abstraction**
    
    1. **Abstract Classes**:
        - Declared with the `abstract` keyword.
        - Can have abstract (unimplemented) and concrete (implemented) methods.
    2. **Interfaces**:
        - All methods are abstract by default (until Java 8 introduced default methods).
        - A class implements an interface and provides implementations for all its methods.
    
    ---
    
    ### **Example of Abstraction Using Abstract Class**
    
    ```java
    abstract class Animal {
        // Abstract method (no implementation)
        abstract void sound();
    
        // Concrete method
        void eat() {
            System.out.println("This animal eats food.");
        }
    }
    
    class Dog extends Animal {
        @Override
        void sound() {
            System.out.println("The dog barks.");
        }
    }
    
    public class AbstractionExample {
        public static void main(String[] args) {
            Animal animal = new Dog();
            animal.sound(); // Output: The dog barks.
            animal.eat();   // Output: This animal eats food.
        }
    }
    
    ```
    
    ---
    
    ### **Example of Abstraction Using Interface**
    
    ```java
    interface Shape {
        double calculateArea();
    }
    
    class Circle implements Shape {
        private double radius;
    
        Circle(double radius) {
            this.radius = radius;
        }
    
        @Override
        public double calculateArea() {
            return Math.PI * radius * radius;
        }
    }
    
    class Rectangle implements Shape {
        private double length, width;
    
        Rectangle(double length, double width) {
            this.length = length;
            this.width = width;
        }
    
        @Override
        public double calculateArea() {
            return length * width;
        }
    }
    
    public class InterfaceExample {
        public static void main(String[] args) {
            Shape circle = new Circle(5);
            Shape rectangle = new Rectangle(4, 6);
    
            System.out.println("Circle Area: " + circle.calculateArea());
            System.out.println("Rectangle Area: " + rectangle.calculateArea());
        }
    }
    
    ```
    
    **Output**:
    
    ```
    Circle Area: 78.53981633974483
    Rectangle Area: 24.0
    
    ```
    
    ---
    
    ### **Advantages of Abstraction**
    
    1. **Reduces Complexity**:
        - Provides a clear and simplified interface for users.
    2. **Enhances Modularity**:
        - Changes to implementation do not affect users of the abstracted features.
    3. **Improves Flexibility**:
        - Allows swapping of implementations without altering the code that uses them.
    
    ---
    
    ## **Comparison: Encapsulation vs. Abstraction**
    
    | **Aspect** | **Encapsulation** | **Abstraction** |
    | --- | --- | --- |
    | **Focus** | Hides data (fields) and controls access. | Hides implementation details. |
    | **Purpose** | Protects the internal state of an object. | Simplifies usage by exposing essential features. |
    | **Implementation** | Achieved through `private` fields and methods. | Achieved using `abstract` classes and `interfaces`. |
    | **Level of Hiding** | Restricts access to data. | Hides implementation but shows behavior. |
    | **Example** | Getters and setters. | Abstract classes or interfaces. |
    
    ---
    
    ### **When to Use**
    
    - **Encapsulation**:
        - Use when you need to secure and control access to internal data.
        - Example: Banking applications where account details must be protected.
    - **Abstraction**:
        - Use when you want to provide a simple and clear interface, hiding implementation details.
        - Example: Defining shapes in a graphics application.
    
