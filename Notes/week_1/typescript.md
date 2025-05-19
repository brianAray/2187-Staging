# TypeScript Notes

## **Unit: TypeScript Orientation**

### **What is TypeScript**

- TypeScript is a strongly typed programming language built on JavaScript. It adds static types to JavaScript to catch errors during development.
- Developed by Microsoft, it is a superset of JavaScript, meaning any valid JavaScript code is valid TypeScript.

---

### **JavaScript vs TypeScript**

| Feature | JavaScript | TypeScript |
| --- | --- | --- |
| **Typing** | Dynamically typed | Statically typed |
| **Error Detection** | Runtime | Compile-time |
| **Features** | ES5/ES6 features only | Includes ES5/ES6 + additional features |
| **Learning Curve** | Easy to learn | Requires understanding of types |

---

### **Why & How to Use TypeScript**

- **Why Use TypeScript**:
    - Improves code quality and readability.
    - Prevents runtime errors through static type checking.
    - Enhances IDE support with autocomplete and inline documentation.
    - Supports modern JavaScript features and beyond.
- **How to Use TypeScript**:
    - Install TypeScript:
        
        ```bash
        npm install -g typescript
        
        ```
        
    - Write `.ts` files instead of `.js` files.
    - Compile TypeScript into JavaScript:
        
        ```bash
        tsc file.ts
        
        ```
        

---

### **TypeScript Compiler and TypeScript Installation**

- The TypeScript Compiler (`tsc`) converts TypeScript code to JavaScript.
- Installation:
    
    ```bash
    npm install -g typescript
    
    ```
    

---

### **Package.json**

- The `package.json` file is a configuration file for Node.js projects, used to manage dependencies and scripts.
    - Example:
        
        ```json
        {
          "name": "my-typescript-project",
          "version": "1.0.0",
          "scripts": {
            "build": "tsc",
            "start": "node dist/index.js"
          },
          "devDependencies": {
            "typescript": "^4.0.0"
          }
        }
        
        ```
        

---

### **Node as JS Runtime**

- Node.js is a JavaScript runtime built on Chrome's V8 engine. It executes JavaScript outside the browser.
- With TypeScript, Node is often used to run the compiled JavaScript code.

---

### **Unit: TypeScript Foundation**

### **Simple or Variable Types**

- **Basic Types**:
    - `number`: For integers and floating-point values.
    - `string`: For text.
    - `boolean`: For `true` or `false`.
    - `any`: Accepts any value.
    - Example:
        
        ```tsx
        let age: number = 25;
        let name: string = "Alice";
        let isActive: boolean = true;
        
        ```
        

---

### **Special Types**

- `void`: For functions that don't return a value.
- `null` and `undefined`: For variables with no value.
- `never`: Represents values that never occur (e.g., functions that throw errors).
- Example:
    
    ```tsx
    function logMessage(): void {
      console.log("This is a message");
    }
    
    ```
    

---

### **Object Types**

- Objects with specific structures can be typed.
    - Example:
        
        ```tsx
        let user: { name: string; age: number } = {
          name: "Alice",
          age: 25,
        };
        
        ```
        

---

### **Union Types**

- Union types allow variables to hold more than one type.
    - Example:
        
        ```tsx
        let id: number | string;
        id = 101;  // Valid
        id = "A123";  // Also valid
        
        ```
        

---

### **Type Aliases and Interfaces**

In TypeScript, **Type Aliases** and **Interfaces** are both ways to define custom types, but they have different use cases and capabilities. Here's an explanation of both, along with examples:

### **Type Aliases**

A **Type Alias** allows you to create a new name for a type. It is flexible and can be used for primitive types, unions, intersections, or more complex structures.

### Syntax:

```tsx
type AliasName = Type;

```

### Example:

```tsx
type Person = {
  name: string;
  age: number;
};

let john: Person = {
  name: "John",
  age: 25
};

```

### Features of Type Aliases:

- Can define complex types like unions or intersections.
- Can alias primitives, arrays, tuples, or other types.

### Example with Union Type:

```tsx
type ID = string | number; // ID can be either a string or a number
let userId: ID = 123; // valid
userId = "abc"; // valid

```

### Example with Intersection Type:

```tsx
type Contact = {
  email: string;
};

type Address = {
  street: string;
  city: string;
};

type ContactDetails = Contact & Address; // Combines both types
let userContact: ContactDetails = {
  email: "user@example.com",
  street: "123 Main St",
  city: "Metropolis"
};

```

### **Interfaces**

An **Interface** is similar to a type alias but with a primary focus on defining the structure of an object. It can be extended or implemented by other interfaces or classes, making it more suited for object-oriented programming.

### Syntax:

```tsx
interface InterfaceName {
  propertyName: Type;
}

```

### Example:

```tsx
interface Person {
  name: string;
  age: number;
}

let john: Person = {
  name: "John",
  age: 25
};

```

### Features of Interfaces:

- Primarily used to define object shapes.
- Can be extended using the `extends` keyword.
- Can be implemented by classes using the `implements` keyword.
- Supports **declaration merging**, which allows multiple declarations of the same interface to be merged together.

### Example of Extending Interfaces:

```tsx
interface Contact {
  email: string;
}

interface Address {
  street: string;
  city: string;
}

interface ContactDetails extends Contact, Address {
  phone: string;
}

let userContact: ContactDetails = {
  email: "user@example.com",
  street: "123 Main St",
  city: "Metropolis",
  phone: "123-456-7890"
};

```

### Example of Implementing an Interface in a Class:

```tsx
interface Shape {
  area: () => number;
}

class Circle implements Shape {
  radius: number;
  constructor(radius: number) {
    this.radius = radius;
  }
  area() {
    return Math.PI * this.radius * this.radius;
  }
}

const circle = new Circle(5);
console.log(circle.area()); // Outputs the area of the circle

```

### **Key Differences Between Type Aliases and Interfaces**

| Feature | Type Alias | Interface |
| --- | --- | --- |
| **Basic Use Case** | Used for any type, including objects, unions, tuples, etc. | Primarily used for object types |
| **Declaration Merging** | No (cannot merge multiple type aliases) | Yes (can declare an interface multiple times and merge them) |
| **Extending** | Can extend using intersections (`&`) | Can extend other interfaces using `extends` |
| **Implementing in Classes** | Not applicable directly | Can be implemented in classes using `implements` |
| **Flexibility** | More flexible in defining complex types (unions, intersections) | Best suited for defining object shapes |

### **When to Use Each:**

- **Use Type Aliases** when you need to define more complex types such as unions, intersections, or when you want a more general-purpose way of creating types.
- **Use Interfaces** when you are working with object-oriented patterns or defining shapes for objects, especially when you want to extend or implement them.

### **Example Comparing Both:**

```tsx
// Using Type Alias
type Animal = {
  name: string;
  age: number;
};

// Using Interface
interface Animal {
  name: string;
  age: number;
}

// Both can be used in the same way
const dog: Animal = {
  name: "Buddy",
  age: 5
};

```

In most cases, either `type` or `interface` will work for object shapes, but if you need to extend or merge multiple definitions, **interfaces** are more suitable.

---

### **Casting**

- Used to override TypeScript¿s type inference.
    - Example:
        
        ```tsx
        let value: any = "Hello World";
        let length: number = (value as string).length;
        
        ```
        

---

### **Functions**

In TypeScript, functions are a core feature and are strongly typed. This ensures that you can define and use functions with predictable behavior and type safety.

---

### **Defining Functions**

### Basic Syntax:

```tsx
function functionName(parameters): returnType {
  // function body
}

```

### Example:

```tsx
function greet(name: string): string {
  return `Hello, ${name}!`;
}

console.log(greet("Alice")); // Output: Hello, Alice!

```

---

### **Typing Function Parameters and Return Values**

1. **Parameter Types**:
    - Each parameter can have a type specified.
    - By default, parameters are required.
2. **Return Type**:
    - You can specify the return type of a function.
    - If no type is provided, TypeScript infers the return type.

### Example:

```tsx
function add(a: number, b: number): number {
  return a + b;
}

function logMessage(message: string): void {
  console.log(message); // No return value
}

```

---

### **Optional and Default Parameters**

1. **Optional Parameters**:
Use a `?` after the parameter name to make it optional.
    
    ```tsx
    function greet(name: string, greeting?: string): string {
      return `${greeting || "Hello"}, ${name}!`;
    }
    
    console.log(greet("Alice")); // Output: Hello, Alice!
    console.log(greet("Alice", "Hi")); // Output: Hi, Alice!
    
    ```
    
2. **Default Parameters**:
Assign a default value to a parameter.
    
    ```tsx
    function greet(name: string, greeting: string = "Hello"): string {
      return `${greeting}, ${name}!`;
    }
    
    console.log(greet("Alice")); // Output: Hello, Alice!
    console.log(greet("Alice", "Hi")); // Output: Hi, Alice!
    
    ```
    

---

### **Function Types**

You can define a function type that specifies the types of parameters and return value.

### Example:

```tsx
// Define a function type
type MathOperation = (a: number, b: number) => number;

// Use the function type
const multiply: MathOperation = (a, b) => a * b;

console.log(multiply(2, 3)); // Output: 6

```

---

### **Arrow Functions**

Arrow functions provide a shorter syntax for defining functions.

### Example:

```tsx
const greet = (name: string): string => `Hello, ${name}!`;

console.log(greet("Alice")); // Output: Hello, Alice!

```

---

### **Rest Parameters**

Rest parameters allow you to accept a variable number of arguments.

### Example:

```tsx
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4)); // Output: 10

```

---

### **Overloading**

TypeScript supports **function overloading**, where you define multiple function signatures for the same function.

### Example:

```tsx
function getInfo(id: number): string;
function getInfo(name: string): string;
function getInfo(value: number | string): string {
  if (typeof value === "number") {
    return `User with ID: ${value}`;
  }
  return `User with name: ${value}`;
}

console.log(getInfo(123)); // Output: User with ID: 123
console.log(getInfo("Alice")); // Output: User with name: Alice

```

---

### **Anonymous Functions**

Functions can be defined without names and assigned to variables or used as arguments.

### Example:

```tsx
const greet = function (name: string): string {
  return `Hello, ${name}!`;
};

console.log(greet("Alice")); // Output: Hello, Alice!

```

---

### **Higher-Order Functions**

Functions that accept other functions as arguments or return functions are called higher-order functions.

### Example:

```tsx
function applyOperation(a: number, b: number, operation: (x: number, y: number) => number): number {
  return operation(a, b);
}

const result = applyOperation(5, 3, (x, y) => x + y);
console.log(result); // Output: 8

```

---

### **Function Interface**

You can use an **interface** to define the structure of a function.

### Example:

```tsx
interface MathOperation {
  (a: number, b: number): number;
}

const subtract: MathOperation = (a, b) => a - b;

console.log(subtract(10, 5)); // Output: 5

```

---

### **Generic Functions**

Generics allow functions to work with multiple types without losing type safety.

### Example:

```tsx
function identity<T>(value: T): T {
  return value;
}

console.log(identity<string>("Hello")); // Output: Hello
console.log(identity<number>(42)); // Output: 42

```

---

### **Key Points**

1. TypeScript ensures function type safety by enforcing correct parameter and return types.
2. Optional and default parameters provide flexibility.
3. Overloading and generics make functions more powerful.
4. Using function types and interfaces promotes code reuse and clarity.

---

### **Classes**

TypeScript enhances object-oriented programming by providing powerful features for **classes**, including strong typing, inheritance, access modifiers, and interfaces. Here's an overview of TypeScript classes and their features.

---

### **Defining a Class**

A class in TypeScript is defined using the `class` keyword. It can include properties, constructors, and methods.

### Example:

```tsx
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }
}

const person = new Person("Alice", 30);
console.log(person.greet()); // Output: Hello, my name is Alice and I am 30 years old.

```

---

### **Access Modifiers**

Access modifiers control the visibility of properties and methods within a class.

1. **`public`** (default):
    - Accessible everywhere.
2. **`private`**:
    - Accessible only within the class.
3. **`protected`**:
    - Accessible within the class and its subclasses.

### Example:

```tsx
class Example {
  public publicProp: string = "Public";
  private privateProp: string = "Private";
  protected protectedProp: string = "Protected";

  public showProps() {
    console.log(this.publicProp); // Accessible
    console.log(this.privateProp); // Accessible
    console.log(this.protectedProp); // Accessible
  }
}

class SubExample extends Example {
  public showProtected() {
    console.log(this.protectedProp); // Accessible in a subclass
    // console.log(this.privateProp); // Error: privateProp is private
  }
}

const example = new Example();
console.log(example.publicProp); // Accessible
// console.log(example.privateProp); // Error: privateProp is private

```

---

### **Readonly Properties**

Use the `readonly` modifier to make a property immutable after it is initialized.

### Example:

```tsx
class ReadOnlyExample {
  readonly id: number;

  constructor(id: number) {
    this.id = id;
  }
}

const example = new ReadOnlyExample(123);
console.log(example.id); // Output: 123
// example.id = 456; // Error: Cannot assign to 'id' because it is a read-only property.

```

---

### **Getters and Setters**

Use `get` and `set` to define custom behavior for accessing and modifying properties.

### Example:

```tsx
class User {
  private _password: string;

  constructor(password: string) {
    this._password = password;
  }

  get password(): string {
    return "******"; // Masked password
  }

  set password(newPassword: string) {
    if (newPassword.length >= 6) {
      this._password = newPassword;
    } else {
      console.log("Password must be at least 6 characters long.");
    }
  }
}

const user = new User("secure123");
console.log(user.password); // Output: ******
user.password = "short"; // Output: Password must be at least 6 characters long.

```

---

### **Inheritance**

TypeScript supports single inheritance using the `extends` keyword.

### Example:

```tsx
class Animal {
  constructor(public name: string) {}

  speak(): string {
    return `${this.name} makes a noise.`;
  }
}

class Dog extends Animal {
  speak(): string {
    return `${this.name} barks.`;
  }
}

const dog = new Dog("Buddy");
console.log(dog.speak()); // Output: Buddy barks.

```

---

### **Abstract Classes**

Abstract classes define a blueprint for other classes. They cannot be instantiated directly and may contain abstract methods that must be implemented by subclasses.

### Example:

```tsx
abstract class Shape {
  abstract area(): number; // Must be implemented by subclasses

  describe(): string {
    return "I am a shape.";
  }
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

const circle = new Circle(5);
console.log(circle.area()); // Output: Area of the circle
console.log(circle.describe()); // Output: I am a shape.

```

---

### **Interfaces and Classes**

Classes can implement interfaces to enforce the shape of the class.

### Example:

```tsx
interface Drivable {
  speed: number;
  drive(): void;
}

class Car implements Drivable {
  speed: number;

  constructor(speed: number) {
    this.speed = speed;
  }

  drive(): void {
    console.log(`Driving at ${this.speed} km/h.`);
  }
}

const car = new Car(120);
car.drive(); // Output: Driving at 120 km/h.

```

---

### **Static Members**

Static properties and methods belong to the class itself, not its instances.

### Example:

```tsx
class MathUtils {
  static PI: number = 3.14;

  static circleArea(radius: number): number {
    return this.PI * radius * radius;
  }
}

console.log(MathUtils.PI); // Output: 3.14
console.log(MathUtils.circleArea(5)); // Output: 78.5

```

---

### **Parameterized Constructors with Short Syntax**

You can define and initialize class properties directly in the constructor.

### Example:

```tsx
class Employee {
  constructor(public id: number, public name: string) {}
}

const emp = new Employee(101, "Alice");
console.log(emp.id); // Output: 101
console.log(emp.name); // Output: Alice

```

---

### **Private Constructors and Singleton Classes**

A `private` constructor prevents the class from being instantiated outside the class itself.

### Example:

```tsx
class Singleton {
  private static instance: Singleton;

  private constructor() {}

  static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }
}

const singleton1 = Singleton.getInstance();
const singleton2 = Singleton.getInstance();
console.log(singleton1 === singleton2); // Output: true

```

---

### **Key Features Recap**

- **Access Modifiers**: `public`, `private`, `protected`, and `readonly`.
- **Inheritance**: Classes can inherit from one another.
- **Abstract Classes**: Define a blueprint for derived classes.
- **Interfaces**: Classes can implement interfaces.
- **Static Members**: Belong to the class, not instances.
- **Encapsulation**: Use getters, setters, and private members.
- **Simplified Constructor**: Automatically define and initialize properties.

---

### **Decorators**

**TypeScript Decorators** are a powerful feature that allows you to modify classes, methods, properties, or parameters at design time. Decorators are a special kind of **declaration** that can be attached to a class, method, accessor, property, or parameter.

They are widely used in frameworks like Angular for metadata configuration.

---

### **Enabling Decorators**

To use decorators in TypeScript, you need to enable the `experimentalDecorators` compiler option in your `tsconfig.json` file:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}

```

---

### **Types of Decorators**

TypeScript provides the following types of decorators:

1. **Class Decorators**
2. **Method Decorators**
3. **Accessor Decorators**
4. **Property Decorators**
5. **Parameter Decorators**

---

### **1. Class Decorators**

A class decorator is applied to a class declaration. It receives the constructor function of the class as its argument.

### Example:

```tsx
function Component(target: Function) {
  target.prototype.componentName = "MyComponent";
}

@Component
class MyClass {}

const instance = new MyClass();
console.log((instance as any).componentName); // Output: MyComponent

```

### Use Case:

Class decorators are commonly used to attach metadata or perform modifications at runtime.

---

### **2. Method Decorators**

A method decorator is applied to a method of a class. It receives the following arguments:

- `target`: The prototype of the class (or the constructor for static methods).
- `propertyKey`: The name of the method.
- `descriptor`: The property descriptor of the method.

### Example:

```tsx
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Method ${propertyKey} called with arguments: ${args}`);
    return originalMethod.apply(this, args);
  };
}

class MyService {
  @LogMethod
  fetchData(id: number) {
    console.log(`Fetching data for ID: ${id}`);
  }
}

const service = new MyService();
service.fetchData(42);
// Output:
// Method fetchData called with arguments: 42
// Fetching data for ID: 42

```

---

### **3. Accessor Decorators**

An accessor decorator is applied to a getter or setter. It has the same arguments as method decorators.

### Example:

```tsx
function LogAccessor(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalGet = descriptor.get;

  descriptor.get = function () {
    console.log(`Getter called for ${propertyKey}`);
    return originalGet?.call(this);
  };
}

class Product {
  private _price: number = 0;

  @LogAccessor
  get price() {
    return this._price;
  }

  set price(value: number) {
    this._price = value;
  }
}

const product = new Product();
product.price = 100;
console.log(product.price); // Logs "Getter called for price" and then 100

```

---

### **4. Property Decorators**

A property decorator is applied to a property of a class. It receives two arguments:

- `target`: The prototype of the class (or the constructor for static properties).
- `propertyKey`: The name of the property.

### Example:

```tsx
function ReadOnly(target: any, propertyKey: string) {
  Object.defineProperty(target, propertyKey, {
    writable: false,
    configurable: false
  });
}

class User {
  @ReadOnly
  name: string = "John";
}

const user = new User();
user.name = "Alice"; // Error in strict mode

```

---

### **5. Parameter Decorators**

A parameter decorator is applied to a specific parameter of a method. It receives three arguments:

- `target`: The prototype of the class.
- `propertyKey`: The name of the method.
- `parameterIndex`: The index of the parameter.

### Example:

```tsx
function LogParameter(target: any, propertyKey: string, parameterIndex: number) {
  console.log(`Parameter ${parameterIndex} of method ${propertyKey} is decorated.`);
}

class Calculator {
  add(@LogParameter a: number, b: number): number {
    return a + b;
  }
}

// Logs: Parameter 0 of method add is decorated.

```

---

### **Common Use Cases for Decorators**

1. **Metadata for Classes**:
    - Annotate classes for dependency injection or metadata.
    - Example: Angular's `@Component`, `@Injectable`.
2. **Logging**:
    - Track method calls or property access.
3. **Validation**:
    - Validate input parameters.
4. **Access Control**:
    - Restrict access to methods or properties based on roles or permissions.
5. **Custom Behavior**:
    - Add custom behavior or modify existing functionality.

---

### **Important Notes**

- Decorators are **syntactic sugar** and work at **design time**.
- They do not modify runtime behavior unless explicitly programmed to do so.
- They are extensively used in frameworks like Angular but are optional in most projects.

---

### **Unit: TypeScript Intermediate**

### **Generics**

**TypeScript Generics** allow you to write reusable, flexible, and type-safe code. They enable functions, classes, and interfaces to work with any type while preserving type information.

---

### **What are Generics?**

Generics are placeholders for types. They allow you to write functions, classes, or interfaces that can operate on various data types without sacrificing type safety.

### Basic Syntax:

```tsx
function identity<T>(value: T): T {
  return value;
}

console.log(identity<string>("Hello")); // Output: Hello
console.log(identity<number>(42));      // Output: 42

```

Here, `T` is a **type parameter** that acts as a placeholder.

---

### **Benefits of Generics**

1. **Type Safety**: Ensures that the types of inputs and outputs are consistent.
2. **Reusability**: Code can be used with different types without duplication.
3. **Readability**: Improves clarity by explicitly specifying types.

---

### **Generic Functions**

### Example:

```tsx
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const result = merge({ name: "Alice" }, { age: 30 });
console.log(result); // Output: { name: "Alice", age: 30 }

```

Here, the function `merge` can combine objects of any type `T` and `U`.

---

### **Generic Constraints**

Generics can be constrained to specific types or structures using the `extends` keyword.

### Example:

```tsx
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const person = { name: "Alice", age: 30 };
console.log(getProperty(person, "name")); // Output: Alice
// console.log(getProperty(person, "height")); // Error: Property 'height' does not exist on type '{ name: string; age: number; }'

```

Here, `K` is constrained to the keys of `T`.

---

### **Generic Interfaces**

Generics can be used with interfaces to define reusable type-safe contracts.

### Example:

```tsx
interface Box<T> {
  value: T;
}

const stringBox: Box<string> = { value: "Hello" };
const numberBox: Box<number> = { value: 42 };

console.log(stringBox.value); // Output: Hello
console.log(numberBox.value); // Output: 42

```

---

### **Generic Classes**

Generics can also be applied to classes.

### Example:

```tsx
class GenericQueue<T> {
  private items: T[] = [];

  enqueue(item: T): void {
    this.items.push(item);
  }

  dequeue(): T | undefined {
    return this.items.shift();
  }
}

const queue = new GenericQueue<number>();
queue.enqueue(1);
queue.enqueue(2);
console.log(queue.dequeue()); // Output: 1
console.log(queue.dequeue()); // Output: 2

```

---

### **Generic Type Aliases**

Type aliases can also leverage generics.

### Example:

```tsx
type Pair<T, U> = [T, U];

const pair: Pair<string, number> = ["Alice", 30];
console.log(pair); // Output: ["Alice", 30]

```

---

### **Using Default Types in Generics**

Generics can have default types, which are used when no type is specified.

### Example:

```tsx
function createArray<T = string>(length: number, value: T): T[] {
  return Array(length).fill(value);
}

console.log(createArray(3, "Hello")); // Output: ["Hello", "Hello", "Hello"]
console.log(createArray<number>(3, 42)); // Output: [42, 42, 42]

```

---

### **Generic Utility Types**

TypeScript provides many **built-in utility types** that use generics.

### Examples:

1. **`Partial<T>`**:
    - Makes all properties of `T` optional.
    
    ```tsx
    interface User {
      name: string;
      age: number;
    }
    
    const partialUser: Partial<User> = { name: "Alice" };
    
    ```
    
2. **`Readonly<T>`**:
    - Makes all properties of `T` read-only.
    
    ```tsx
    const readonlyUser: Readonly<User> = { name: "Alice", age: 30 };
    // readonlyUser.age = 40; // Error
    
    ```
    
3. **`Record<K, T>`**:
    - Creates an object type with keys `K` and values `T`.
    
    ```tsx
    const roles: Record<string, string> = { admin: "Alice", user: "Bob" };
    
    ```
    
4. **`Pick<T, K>`**:
    - Picks a subset of properties from `T`.
    
    ```tsx
    const userSubset: Pick<User, "name"> = { name: "Alice" };
    
    ```
    
5. **`Omit<T, K>`**:
    - Omits specific properties from `T`.
    
    ```tsx
    const userWithoutAge: Omit<User, "age"> = { name: "Alice" };
    
    ```
    

---

### **Generic Constraints with Multiple Types**

You can enforce constraints for multiple type parameters.

### Example:

```tsx
function combine<T extends object, U extends object>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const combined = combine({ name: "Alice" }, { age: 30 });
console.log(combined); // Output: { name: "Alice", age: 30 }

```

---

### **Key Points**

1. **Generics increase code flexibility and maintain type safety.**
2. **Constraints ensure type parameters follow specific structures.**
3. **Generics work seamlessly with functions, classes, interfaces, and type aliases.**
4. **Use default generic types for fallback behavior.**

Generics allow you to write reusable, robust, and maintainable code for real-world applications.

---

### **Array Generics**

- Type arrays using generics.
    - Example:
        
        ```tsx
        let numbers: Array<number> = [1, 2, 3];
        
        ```
        

---

### **String Enums**

- Define a set of named string constants.
    - Example:
        
        ```tsx
        enum Status {
          Active = "ACTIVE",
          Inactive = "INACTIVE",
        }
        
        ```
        

---

### **Number Enums**

- Define a set of named numeric constants.
    - Example:
        
        ```tsx
        enum Direction {
          Up = 1,
          Down,
        }
        
        ```
        

---

### **Tuples**

- Tuples are arrays with fixed types and lengths.
    - Example:
        
        ```tsx
        let tuple: [number, string] = [1, "Alice"];
        
        ```
        

---

### **Unit: TypeScript Config**

### **TypeScript Compiler (TSC)**

The **TypeScript Compiler (TSC)** is a command-line tool that compiles TypeScript code (`.ts` files) into JavaScript code (`.js` files). It performs type checking and ensures that your code adheres to the rules defined by TypeScript.

---

### **Installing TypeScript and TSC**

To use TSC, you need to install TypeScript globally on your system via npm:

```bash
npm install -g typescript

```

After installation, you can verify it using:

```bash
tsc --version

```

---

### **Compiling TypeScript Files**

To compile a single TypeScript file:

```bash
tsc <filename>.ts

```

### Example:

If you have a `hello.ts` file:

```tsx
const greet = (name: string): string => `Hello, ${name}!`;
console.log(greet("World"));

```

Compile it with:

```bash
tsc hello.ts

```

This generates a `hello.js` file:

```jsx
const greet = (name) => `Hello, ${name}!`;
console.log(greet("World"));

```

---

### **tsconfig.json**

The `tsconfig.json` file is a configuration file for the TypeScript compiler. It defines how the TypeScript files in a project should be compiled.

### Creating a `tsconfig.json` File:

```bash
tsc --init

```

This generates a default configuration file. You can customize it based on your project requirements.

### Example `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES6",                // JavaScript version
    "module": "commonjs",           // Module system
    "strict": true,                 // Enable strict type-checking
    "outDir": "./dist",             // Output directory
    "rootDir": "./src",             // Root directory for source files
    "esModuleInterop": true,        // Support for ES Module imports
    "skipLibCheck": true            // Skip type checking of declaration files
  },
  "include": ["src/**/*"],          // Files to include
  "exclude": ["node_modules"]       // Files to exclude
}

```

With `tsconfig.json` in place, run the compiler without specifying a file:

```bash
tsc

```

---

### **Compiler Options**

The TypeScript compiler supports numerous options to customize the compilation process. Here are some commonly used options:

| **Option** | **Description** |
| --- | --- |
| `--target` | Specifies the JavaScript version (e.g., `ES5`, `ES6`). |
| `--module` | Specifies the module system (`commonjs`, `es6`, `amd`, etc.). |
| `--outDir` | Directory for output files. |
| `--rootDir` | Directory for input files. |
| `--strict` | Enables strict type-checking. |
| `--noImplicitAny` | Disallows implicit `any` types. |
| `--sourceMap` | Generates source map files for debugging. |
| `--watch` | Re-compiles files automatically when changes are detected. |
| `--declaration` | Generates `.d.ts` declaration files for libraries. |

### Example:

```bash
tsc --target ES6 --outDir dist src/index.ts

```

---

### **Watch Mode**

The `--watch` or `-w` flag automatically recompiles TypeScript files whenever changes are detected.

```bash
tsc --watch

```

---

### **Key Features of TSC**

1. **Type Checking**:
    - Ensures your code adheres to TypeScript's rules.
    - Prevents runtime errors by catching issues during compilation.
2. **Compilation**:
    - Converts TypeScript into clean, readable JavaScript.
3. **Configuration Flexibility**:
    - Use `tsconfig.json` to define project-specific compilation settings.
4. **Integration**:
    - Seamlessly integrates with build tools like Webpack, Gulp, and Babel.

---

### **Integration with IDEs**

Most modern IDEs like **VS Code** provide excellent TypeScript support:

- Syntax highlighting.
- Real-time error checking.
- Code completion.

Install the TypeScript extension for better developer experience.

---

### **Advantages of Using TSC**

1. **Improved Code Quality**: Type checking ensures fewer runtime errors.
2. **Cross-Platform Compatibility**: Target various JavaScript versions.
3. **Extensive Configuration**: Tailor the compilation process for different environments.
4. **Ecosystem Integration**: Works seamlessly with Node.js, frontend frameworks, and build tools.

The TypeScript Compiler is a cornerstone of TypeScript development, empowering developers with robust, scalable, and maintainable codebases.

### **Strict Mode**

- Enable strict type-checking:
    
    ```json
    {
      "compilerOptions": {
        "strict": true
      }
    }
    
    ```
    

---
