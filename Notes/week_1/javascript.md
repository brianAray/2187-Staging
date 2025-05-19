# JavaScript Notes

## **Unit: JavaScript Foundation**

### **JavaScript Introduction**

- JavaScript is a high-level, interpreted programming language used for creating interactive effects within web browsers.
- It is often used alongside HTML and CSS to enhance web functionality.
- Common uses include manipulating web pages (DOM manipulation), handling events (clicks, form submissions), and performing asynchronous tasks (API calls, timers).

---

### **Naming Conventions**

- **Camel Case**: Used for variables and function names, e.g., `myVariableName`, `calculateTotalAmount`.
- **Pascal Case**: Used for class names, e.g., `Person`, `CarModel`.
- **Snake Case**: Often used in file names or constants in some languages, e.g., `my_variable_name`.
- **Uppercase for Constants**: Constants are written in uppercase, e.g., `MAX_VALUE = 100`.

---

### **Datatypes**

- **Primitive Types**:
    - `Number`: Represents numeric values, e.g., `123`, `10.5`.
    - `String`: Represents text values, e.g., `"Hello World"`.
    - `Boolean`: Represents `true` or `false`.
    - `undefined`: A variable declared but not assigned a value.
    - `null`: Represents no value or an empty object reference.
    - `Symbol`: A unique and immutable value used as an identifier.
    - `BigInt`: Large integers that are beyond the size limit for the `Number` type.
- **Non-Primitive Types**:
    - `Object`: Collections of key-value pairs, e.g., `{ name: "Alice", age: 25 }`.
    - `Array`: A special kind of object used for storing ordered lists.

---

### **Type Coercion**

Type coercion is the process of converting a value from one type to another in JavaScript. It can happen **explicitly** (when the developer explicitly converts the type) or **implicitly** (when JavaScript automatically converts the type during runtime).

---

### **1. Types of Type Coercion**

1. **Explicit Coercion:**
    - When you intentionally convert a value from one type to another.
    - Example: `String(123)`, `Number("456")`, or `Boolean(0)`.
2. **Implicit Coercion:**
    - When JavaScript automatically converts types in certain operations.
    - Example: `1 + "2"` results in `"12"` because `1` is coerced into a string.

---

### **2. Coercion Rules**

### **a. To String:**

JavaScript converts non-string values to strings when they are used in a string context, such as concatenation.

```jsx
console.log(123 + "");  // "123"
console.log(true + ""); // "true"
console.log(null + ""); // "null"
console.log(undefined + ""); // "undefined"

```

### **b. To Number:**

Values are coerced to numbers when they are used in arithmetic operations (except addition with a string).

```jsx
console.log("123" - 0);     // 123
console.log("123" * 2);     // 246
console.log("123" / "3");   // 41
console.log("abc" - 0);     // NaN
console.log(true + 1);      // 2 (true is coerced to 1)
console.log(null + 1);      // 1 (null is coerced to 0)
console.log(undefined + 1); // NaN (undefined can't be coerced to a number)

```

### **c. To Boolean:**

JavaScript uses "truthy" and "falsy" values to coerce types to `boolean`. Falsy values include:

| Value | Coerced Boolean |
| --- | --- |
| `false` | `false` |
| `0` | `false` |
| `""` | `false` |
| `null` | `false` |
| `undefined` | `false` |
| `NaN` | `false` |

Everything else is **truthy**.

```jsx
console.log(Boolean(0));        // false
console.log(Boolean(""));       // false
console.log(Boolean("hello"));  // true
console.log(Boolean([]));       // true
console.log(Boolean({}));       // true

```

---

### **3. Implicit Coercion in Operations**

### **a. String Context:**

When one operand in a binary `+` operation is a string, JavaScript converts the other operand to a string and performs concatenation.

```jsx
console.log("123" + 456); // "123456"
console.log(123 + "456"); // "123456"

```

### **b. Number Context:**

Other arithmetic operators (`-`, `*`, `/`, `%`) convert both operands to numbers.

```jsx
console.log("123" - "23"); // 100
console.log("5" * 2);      // 10
console.log("10" / 2);     // 5
console.log("abc" * 2);    // NaN

```

### **c. Equality (`==`) vs Strict Equality (`===`):**

The `==` operator performs type coercion, while `===` does not.

```jsx
console.log(123 == "123");  // true (string is coerced to number)
console.log(123 === "123"); // false (different types)
console.log(null == undefined); // true
console.log(null === undefined); // false
console.log(true == 1);    // true
console.log(false == 0);   // true

```

---

---

### **Arrays**

- Arrays are used to store multiple values in a single variable.
    - Example:
        
        ```jsx
        let fruits = ["apple", "banana", "cherry"];
        console.log(fruits[0]);  // Outputs "apple"
        
        ```
        
- **Common Array Methods**:
    - `push()`: Adds an element to the end of an array.
    - `pop()`: Removes the last element from an array.
    - `shift()`: Removes the first element from an array.
    - `unshift()`: Adds an element to the start of an array.

---

### **Functions**

- Functions allow you to define reusable blocks of code.
    - Example:
        
        ```jsx
        function greet(name) {
            console.log("Hello, " + name);
        }
        greet("Alice");  // Outputs "Hello, Alice"
        
        ```
        
- **Return Statement**: Functions can return values to be used later.
    
    ```jsx
    function add(a, b) {
        return a + b;
    }
    console.log(add(2, 3));  // Outputs 5
    
    ```
    

---

### **Assignment Operators**

- **Assignment Operators** are used to assign values to variables:
    - `=`: Basic assignment.
    - `+=`: Adds and assigns, e.g., `x += 1` is equivalent to `x = x + 1`.
    - `=`: Subtracts and assigns.
    - `=`: Multiplies and assigns.

---

### **Variable Scopes**

Variable scope determines where in the code a variable can be accessed. JavaScript has **three types of scopes**: **global scope**, **function scope**, and **block scope**.

---

### **1. Types of Scopes**

### **a. Global Scope**

- Variables declared outside any function or block have global scope.
- These variables are accessible from anywhere in the code.

**Example:**

```jsx
var globalVar = "I am global";

function test() {
    console.log(globalVar); // Accessible
}

test();
console.log(globalVar); // Accessible

```

---

### **b. Function Scope**

- Variables declared inside a function using `var`, `let`, or `const` are scoped to that function.
- They cannot be accessed outside the function.

**Example:**

```jsx
function testFunction() {
    var functionVar = "I am scoped to the function";
    console.log(functionVar); // Accessible
}

testFunction();
console.log(functionVar); // Error: functionVar is not defined

```

---

### **c. Block Scope**

- Variables declared with `let` or `const` are scoped to the block in which they are declared (e.g., inside `{}` braces).
- Variables declared with `var` do **not** have block scope¿they are scoped to the enclosing function or global scope.

**Example:**

```jsx
if (true) {
    let blockScoped = "I am block scoped";
    console.log(blockScoped); // Accessible
}
console.log(blockScoped); // Error: blockScoped is not defined

if (true) {
    var notBlockScoped = "I am not block scoped";
}
console.log(notBlockScoped); // Accessible

```

---

### **2. Scope and Declaration Keywords**

### **a. `var`**

- **Function-scoped:** Accessible within the function it is declared.
- **No block scope:** Ignores block boundaries (e.g., `if`, `for`).
- **Hoisted:** Can be accessed before declaration (initializes as `undefined`).

**Example:**

```jsx
function testVar() {
    console.log(myVar); // undefined (hoisting)
    var myVar = "Hello";
    console.log(myVar); // Hello
}
testVar();

```

---

### **b. `let`**

- **Block-scoped:** Restricted to the block where it is declared.
- **No hoisting:** Cannot be accessed before declaration.

**Example:**

```jsx
function testLet() {
    console.log(myLet); // Error: Cannot access 'myLet' before initialization
    let myLet = "Hello";
    console.log(myLet); // Hello
}
testLet();

```

---

### **c. `const`**

- **Block-scoped:** Same as `let`.
- **No re-assignment:** Value cannot be changed after initialization.
- **No hoisting:** Cannot be accessed before declaration.

**Example:**

```jsx
function testConst() {
    const myConst = "Hello";
    console.log(myConst); // Hello

    // myConst = "New Value"; // Error: Assignment to constant variable
}
testConst();

```

---

### **3. Closures and Scope**

Closures allow a function to retain access to its outer scope even after the outer function has finished executing.

**Example:**

```jsx
function createCounter() {
    let count = 0;

    return function () {
        count++;
        console.log(count);
    };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
counter(); // 3

```

---

### **`let`, `const`, and `var` in JavaScript**

JavaScript provides three keywords for declaring variables: `let`, `const`, and `var`. Each has distinct characteristics and use cases.

---

### **1. `let`**

`let` is used to declare variables that can be reassigned but are block-scoped.

### **Features of `let`:**

1. **Block Scope:**
    - The variable is only accessible within the block `{}` in which it is declared.
2. **Can Be Reassigned:**
    - You can change the value of a `let` variable after it is initialized.
3. **Not Hoisted (Temporal Dead Zone):**
    - The variable exists in a "temporal dead zone" from the start of the block until the declaration is encountered.

**Example:**

```jsx
if (true) {
    let x = 10;
    console.log(x); // 10
}
console.log(x); // Error: x is not defined

let y = 20;
y = 30; // Reassignment allowed
console.log(y); // 30

```

---

### **2. `const`**

`const` is used to declare variables whose values cannot be reassigned. These variables are also block-scoped.

### **Features of `const`:**

1. **Block Scope:**
    - Like `let`, `const` is block-scoped.
2. **Immutable Variable Binding:**
    - You cannot reassign a `const` variable, but the value of the object it points to can be modified.
3. **Must Be Initialized:**
    - `const` variables must be assigned a value at the time of declaration.
4. **Not Hoisted (Temporal Dead Zone):**
    - Like `let`, `const` variables are not accessible before their declaration.

**Example:**

```jsx
if (true) {
    const z = 50;
    console.log(z); // 50
}
console.log(z); // Error: z is not defined

const a = 100;
// a = 200; // Error: Assignment to constant variable

const obj = { key: "value" };
obj.key = "newValue"; // Allowed, as the object itself is not reassigned
console.log(obj); // { key: "newValue" }

```

---

### **3. `var`**

`var` is the oldest way to declare variables in JavaScript. It has function scope and lacks block scope, which can lead to bugs.

### **Features of `var`:**

1. **Function Scope:**
    - `var` variables are scoped to the enclosing function, not the block.
2. **Can Be Reassigned:**
    - You can reassign `var` variables.
3. **Hoisted:**
    - Variables declared with `var` are hoisted to the top of their scope and initialized with `undefined`.

**Example:**

```jsx
if (true) {
    var b = 10;
    console.log(b); // 10
}
console.log(b); // 10 (No block scope, accessible outside the block)

console.log(c); // undefined (Hoisting)
var c = 20;
console.log(c); // 20

```

---

### **Hoisting in JavaScript**

Hoisting is JavaScript's default behavior of moving variable, function, or class declarations to the top of their scope during the compilation phase, before the code is executed. This means you can use variables and functions before they are declared, but there are important rules to understand.

---

### **1. How Hoisting Works**

1. **Variable Declarations** are hoisted but not initialized:
    - For `var`, the variable is initialized to `undefined`.
    - For `let` and `const`, the variable is hoisted but remains in the "temporal dead zone" (TDZ) until the declaration is encountered.
2. **Function Declarations** are fully hoisted:
    - You can call the function before it is declared.
3. **Class Declarations** are hoisted but not initialized:
    - They remain in the TDZ and cannot be used before their declaration.

---

### **2. Hoisting Behavior by Declaration Type**

### **a. `var` Variables**

- `var` is hoisted to the top of its function or global scope and initialized with `undefined`.

**Example:**

```jsx
console.log(a); // undefined
var a = 5;
console.log(a); // 5

```

### **b. `let` and `const` Variables**

- Both are hoisted but remain in the **Temporal Dead Zone** (TDZ) until the interpreter reaches the declaration. Accessing them before declaration results in a `ReferenceError`.

**Example:**

```jsx
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;

console.log(c); // ReferenceError: Cannot access 'c' before initialization
const c = 20;

```

### **c. Function Declarations**

- Function declarations are fully hoisted, meaning you can call them before their declaration.

**Example:**

```jsx
sayHello(); // "Hello!"

function sayHello() {
    console.log("Hello!");
}

```

### **d. Function Expressions (with `var`, `let`, or `const`)**

- Function expressions are treated like variables and are not hoisted as callable functions.

**Example:**

```jsx
console.log(sayHi); // undefined
var sayHi = function () {
    console.log("Hi!");
};
sayHi(); // "Hi!"

console.log(sayHey); // ReferenceError: Cannot access 'sayHey' before initialization
let sayHey = function () {
    console.log("Hey!");
};

```

---

### **Strict Mode**

- Strict mode enforces stricter parsing and error handling in JavaScript.
    - Activating strict mode:
        
        ```jsx
        "use strict";
        let x = 3.14;  // Error: Variable is assigned but never declared
        
        ```
        

---

### **Arrow Functions**

Arrow functions, introduced in ES6, provide a concise syntax for writing functions. They are particularly useful for shorter, more readable function expressions.

---

### **1. Syntax**

The syntax of an arrow function is simpler compared to a regular function.

**Basic Syntax:**

```jsx
(param1, param2, ..., paramN) => expression

```

If there¿s only one parameter, the parentheses `()` can be omitted:

```jsx
param => expression

```

If there are no parameters, an empty pair of parentheses is required:

```jsx
() => expression

```

For functions with multiple statements or a block of code, wrap the body in curly braces `{}` and use `return` explicitly if returning a value:

```jsx
(param1, param2) => {
    const result = param1 + param2;
    return result;
}

```

---

### **2. Examples**

### **a. Single-Line Arrow Function:**

```jsx
const add = (a, b) => a + b;
console.log(add(5, 3)); // 8

```

### **b. Multi-Line Arrow Function:**

```jsx
const multiply = (a, b) => {
    const result = a * b;
    return result;
};
console.log(multiply(4, 5)); // 20

```

### **c. Single Parameter:**

```jsx
const greet = name => `Hello, ${name}!`;
console.log(greet("Alice")); // "Hello, Alice!"

```

### **d. No Parameters:**

```jsx
const sayHi = () => "Hi there!";
console.log(sayHi()); // "Hi there!"

```

---

### **3. Key Differences from Regular Functions**

### **a. `this` Binding**

Arrow functions do not have their own `this`. Instead, they inherit `this` from their surrounding (lexical) context.

**Example:**

```jsx
function Person(name) {
    this.name = name;

    // Regular function
    this.sayName = function() {
        console.log(`My name is ${this.name}`);
    };

    // Arrow function
    this.sayNameArrow = () => {
        console.log(`My name is ${this.name}`);
    };
}

const alice = new Person("Alice");
alice.sayName(); // "My name is Alice"
alice.sayNameArrow(); // "My name is Alice"

```

When used as a callback:

```jsx
const obj = {
    count: 10,
    regularFn: function () {
        setTimeout(function () {
            console.log(this.count); // undefined (global `this`)
        }, 1000);
    },
    arrowFn: function () {
        setTimeout(() => {
            console.log(this.count); // 10 (lexical `this`)
        }, 1000);
    },
};

obj.regularFn();
obj.arrowFn();

```

### **b. No `arguments` Object**

Arrow functions do not have their own `arguments` object. Instead, you can use rest parameters (`...args`) to access arguments.

**Example:**

```jsx
const regularFn = function() {
    console.log(arguments);
};

const arrowFn = (...args) => {
    console.log(args);
};

regularFn(1, 2, 3); // [Arguments] { '0': 1, '1': 2, '2': 3 }
arrowFn(1, 2, 3);   // [ 1, 2, 3 ]

```

---

### **4. Use Cases**

### **a. Callbacks**

Arrow functions are ideal for callbacks due to their concise syntax.

```jsx
const nums = [1, 2, 3, 4];
const squares = nums.map(num => num * num);
console.log(squares); // [1, 4, 9, 16]

```

### **b. Object Methods**

Avoid using arrow functions for object methods if you need `this` to refer to the object.

```jsx
const obj = {
    value: 42,
    method: () => console.log(this.value), // `this` is not `obj`, but the enclosing context
};
obj.method(); // undefined

```

---

### **5. Limitations of Arrow Functions**

1. **No `this`, `arguments`, or `super`:**
    - Arrow functions do not bind their own `this`, `arguments`, or `super`.
2. **Not Suitable for Methods:**
    - Avoid using them as object methods because they do not have their own `this`.
3. **Cannot Be Used as Constructors:**
    - Arrow functions cannot be used with the `new` keyword.

**Example:**

```jsx
const ArrowConstructor = () => {};
const obj = new ArrowConstructor(); // TypeError: ArrowConstructor is not a constructor

```

---

### **Summary**

| Feature | Arrow Function | Regular Function |
| --- | --- | --- |
| **Syntax** | Concise | Verbose |
| **`this` Binding** | Lexical (inherits `this`) | Dynamic (`this` changes) |
| **`arguments` Object** | Not available | Available |
| **Constructor Support** | No | Yes |
| **Use Case** | Callbacks, short functions | Object methods, constructors |

---

### **Arithmetic Operators**

- Used for performing basic mathematical operations.
    - `+`: Addition
    - ``: Subtraction
    - ``: Multiplication
    - `/`: Division
    - `%`: Modulus (remainder)

---

### **Comparison and Logical Operators**

- **Comparison Operators**:
    - `==`: Equality (compares values)
    - `===`: Strict equality (compares both value and type)
    - `!=`: Inequality
    - `>`: Greater than
    - `<`: Less than
- **Logical Operators**:
    - `&&`: Logical AND
    - `||`: Logical OR
    - `!`: Logical NOT

---

### **Control Flow**

- **If-Else**: Used for decision-making.
    
    ```jsx
    if (x > 10) {
        console.log("Greater");
    } else {
        console.log("Smaller or equal");
    }
    
    ```
    

---

### **Object Literals**

- Objects represent collections of key-value pairs.
    - Example:
        
        ```jsx
        let person = {
            name: "Alice",
            age: 25,
            greet: function() {
                console.log("Hello!");
            }
        };
        person.greet();  // Outputs "Hello!"
        
        ```
        

---

### **Template Literals**

- Template literals allow embedding expressions inside strings using backticks (``).
    - Example:
        
        ```jsx
        let name = "Alice";
        console.log(`Hello, ${name}!`);  // Outputs "Hello, Alice!"
        
        ```
        

---

### **Unit: JavaScript Advanced**

### **OOP (Object-Oriented Programming)**

- OOP is a programming paradigm based on the concept of objects, which contain data and methods.
- Key principles include encapsulation, inheritance, and polymorphism.

---

### **this Keyword**

- The `this` keyword refers to the context in which the function is called.
    - Example:
        
        ```jsx
        function greet() {
            console.log(this.name);
        }
        const person = { name: "Alice", greet: greet };
        person.greet();  // Outputs "Alice"
        
        ```
        

---

### **Classes**

- Classes are blueprints for creating objects in JavaScript.
    - Example:
        
        ```jsx
        class Person {
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
            greet() {
                console.log(`Hello, my name is ${this.name}`);
            }
        }
        const person1 = new Person("Alice", 25);
        person1.greet();  // Outputs "Hello, my name is Alice"
        
        ```
        

---

### **Errors**

- Errors occur when the code execution fails.
    - Handling errors using `try-catch`:
        
        ```jsx
        try {
            let result = x / 0;
        } catch (error) {
            console.log("Error: " + error.message);
        }
        
        ```
        

---

### **Default Parameters**

- Default parameters allow functions to be called with fewer arguments than defined.
    - Example:
        
        ```jsx
        function greet(name = "Guest") {
            console.log(`Hello, ${name}`);
        }
        greet();  // Outputs "Hello, Guest"
        
        ```
        

---

### **Spread & Rest Operators**

- **Spread Operator** (`...`): Expands an array or object into individual elements.
    - Example:
        
        ```jsx
        const arr1 = [1, 2, 3];
        const arr2 = [...arr1, 4, 5];
        
        ```
        
- **Rest Operator** (`...`): Collects multiple elements into an array.
    - Example:
        
        ```jsx
        function sum(...numbers) {
            return numbers.reduce((acc, num) => acc + num, 0);
        }
        console.log(sum(1, 2, 3, 4));  // Outputs 10
        
        ```
        

---

### **Anonymous Functions**

- Functions without a name, often used as argumentsor for callbacks.
- Example:
    
    ```jsx
    setTimeout(function() {
        console.log("Executed after 2 seconds");
    }, 2000);
    
    ```
    

---

### **Unit: JavaScript DOM**

### **DOM Structure**

The Document Object Model (DOM) represents the structure of a webpage as a tree of objects. Each HTML element, attribute, and piece of text is a **node** in this tree, which JavaScript can manipulate to change the document dynamically.

---

### **1. Basic DOM Tree Structure**

For a simple HTML document like this:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Example</title>
</head>
<body>
    <h1 id="header">Welcome</h1>
    <p>This is a paragraph.</p>
    <div class="container">
        <ul>
            <li>Item 1</li>
            <li>Item 2</li>
        </ul>
    </div>
</body>
</html>

```

The corresponding DOM tree looks like this:

```
#document
   ¿¿¿ html
       ¿¿¿ head
       ¿     ¿¿¿ title
       ¿           ¿¿¿ "Example"
       ¿¿¿ body
             ¿¿¿ h1
             ¿     ¿¿¿ "Welcome"
             ¿¿¿ p
             ¿     ¿¿¿ "This is a paragraph."
             ¿¿¿ div (class="container")
                   ¿¿¿ ul
                         ¿¿¿ li
                         ¿     ¿¿¿ "Item 1"
                         ¿¿¿ li
                               ¿¿¿ "Item 2"

```

---

### **2. Types of Nodes**

The DOM consists of several types of nodes:

| Node Type | Description | Example |
| --- | --- | --- |
| **Document Node** | The root of the DOM tree. | `document` |
| **Element Node** | Represents HTML elements. | `<h1>`, `<p>`, `<div>` |
| **Text Node** | Represents the text inside an element. | `"Welcome"` |
| **Attribute Node** | Represents attributes of elements (rarely used). | `id="header"`, `class="container"` |
| **Comment Node** | Represents HTML comments. | `<!-- This is a comment -->` |

---

### **3. Key Properties of DOM Structure**

### **a. `document`**

- The `document` object is the entry point for interacting with the DOM.

**Example:**

```jsx
console.log(document.documentElement); // <html> element
console.log(document.body); // <body> element
console.log(document.title); // "Example"

```

### **b. Parent-Child Relationships**

- DOM nodes are organized in a **hierarchical structure** with parent-child relationships.

**Example:**

```jsx
const container = document.querySelector(".container");
console.log(container.parentNode); // <body>
console.log(container.childNodes); // NodeList of <ul>

```

### **c. Sibling Relationships**

- Nodes on the same level are **siblings**.

**Example:**

```jsx
const header = document.getElementById("header");
console.log(header.nextElementSibling); // <p>

```

### **d. Root Node**

- The `<html>` element is the root node of the document.

**Example:**

```jsx
console.log(document.documentElement); // <html> element

```

---

### **4. Commonly Used Properties and Methods**

| Property/Method | Description |
| --- | --- |
| `document.documentElement` | Returns the root `<html>` element. |
| `document.body` | Returns the `<body>` element. |
| `document.head` | Returns the `<head>` element. |
| `element.childNodes` | Returns all child nodes (including text and comments). |
| `element.children` | Returns only child elements (ignores text and comments). |
| `element.parentNode` | Returns the parent node of the element. |
| `element.nextElementSibling` | Returns the next sibling element. |
| `element.previousElementSibling` | Returns the previous sibling element. |

---

### **Selecting Elements from the DOM**

In JavaScript, you can interact with and manipulate the DOM (Document Object Model) by selecting elements using various methods. These methods allow you to target elements by their tag name, ID, class, attributes, or relationships within the DOM tree.

---

### **1. DOM Selection Methods**

### **a. `document.getElementById()`**

- Selects an element by its `id`.
- Returns the element as an object or `null` if no element is found.

**Example:**

```jsx
const title = document.getElementById("main-title");
console.log(title); // <h1 id="main-title">Hello World</h1>

```

### **b. `document.getElementsByClassName()`**

- Selects all elements with a specific `class`.
- Returns an HTMLCollection (array-like, but not an array).

**Example:**

```jsx
const items = document.getElementsByClassName("item");
console.log(items); // HTMLCollection of elements with class "item"

```

### **c. `document.getElementsByTagName()`**

- Selects all elements by their tag name.
- Returns an HTMLCollection.

**Example:**

```jsx
const paragraphs = document.getElementsByTagName("p");
console.log(paragraphs); // HTMLCollection of <p> elements

```

### **d. `document.querySelector()`**

- Selects the **first** element that matches a CSS selector.
- Returns the element or `null` if no match is found.

**Example:**

```jsx
const firstItem = document.querySelector(".item");
console.log(firstItem); // The first element with class "item"

```

### **e. `document.querySelectorAll()`**

- Selects **all** elements that match a CSS selector.
- Returns a NodeList (array-like, but can be iterated with `forEach`).

**Example:**

```jsx
const allItems = document.querySelectorAll(".item");
allItems.forEach(item => console.log(item)); // Logs each element with class "item"

```

---

### **DOM Manipulation**

DOM Manipulation allows you to dynamically change the structure, content, and style of a webpage. Using JavaScript, you can interact with HTML elements, add or remove elements, modify attributes, and style them.

---

### **1. Common DOM Manipulation Methods**

### **a. Changing Content**

1. **`textContent`:**
    - Updates or retrieves the textual content of an element.
    
    ```jsx
    const heading = document.getElementById("main-title");
    heading.textContent = "Welcome to DOM Manipulation!";
    console.log(heading.textContent); // "Welcome to DOM Manipulation!"
    
    ```
    
2. **`innerHTML`:**
    - Updates or retrieves the HTML content of an element (including child elements).
    
    ```jsx
    const container = document.getElementById("container");
    container.innerHTML = "<p>New paragraph added!</p>";
    
    ```
    
    **Note:** Be cautious when using `innerHTML` with user-provided input to prevent XSS (Cross-Site Scripting) attacks.
    

---

### **b. Changing Attributes**

1. **`setAttribute`:**
    - Sets a new value for an attribute.
    
    ```jsx
    const link = document.querySelector("a");
    link.setAttribute("href", "https://www.example.com");
    
    ```
    
2. **`getAttribute`:**
    - Retrieves the value of an attribute.
    
    ```jsx
    console.log(link.getAttribute("href")); // "https://www.example.com"
    
    ```
    
3. **`removeAttribute`:**
    - Removes an attribute from an element.
    
    ```jsx
    link.removeAttribute("href");
    
    ```
    
4. **Direct Property Access:**
    - You can also directly modify attributes using properties (e.g., `id`, `src`, `value`).
    
    ```jsx
    const image = document.querySelector("img");
    image.src = "new-image.jpg";
    
    ```
    

---

### **c. Adding and Removing Elements**

1. **`appendChild`:**
    - Adds a child element to a parent element.
    
    ```jsx
    const newElement = document.createElement("div");
    newElement.textContent = "I am a new div!";
    document.body.appendChild(newElement);
    
    ```
    
2. **`removeChild`:**
    - Removes a child element from a parent element.
    
    ```jsx
    const parent = document.getElementById("parent");
    const child = document.getElementById("child");
    parent.removeChild(child);
    
    ```
    
3. **`replaceChild`:**
    - Replaces an existing child element with a new one.
    
    ```jsx
    const newChild = document.createElement("span");
    newChild.textContent = "I replaced the old child!";
    parent.replaceChild(newChild, child);
    
    ```
    
4. **`append`:**
    - Adds multiple elements or strings to a parent element.
    
    ```jsx
    const container = document.getElementById("container");
    container.append("Text added", document.createElement("div"));
    
    ```
    
5. **`prepend`:**
    - Adds elements or strings at the beginning of a parent element.
    
    ```jsx
    container.prepend("Prepended text");
    
    ```
    
6. **`remove`:**
    - Removes an element directly.
    
    ```jsx
    const element = document.getElementById("to-be-removed");
    element.remove();
    
    ```
    

---

### **Traversing the DOM**

DOM traversal refers to navigating through the Document Object Model (DOM) tree to select elements based on their relationships to other elements. You can move up, down, or sideways within the DOM tree to access parent, child, and sibling nodes.

---

### **1. Traversing Parent and Ancestors**

### **a. `parentNode`**

- Returns the direct parent node of the selected element.
- Includes text nodes and document nodes.

**Example:**

```jsx
const child = document.querySelector(".child");
console.log(child.parentNode); // Parent element or node

```

### **b. `parentElement`**

- Similar to `parentNode` but only returns the parent if it is an HTML element.
- Excludes non-element nodes like text nodes.

**Example:**

```jsx
console.log(child.parentElement); // Parent element only

```

---

### **2. Traversing Children**

### **a. `childNodes`**

- Returns a NodeList of all child nodes (including text nodes, comments, and elements).

**Example:**

```jsx
const parent = document.querySelector(".parent");
console.log(parent.childNodes); // NodeList of all child nodes

```

### **b. `children`**

- Returns an HTMLCollection of child elements (excludes text nodes and comments).

**Example:**

```jsx
console.log(parent.children); // HTMLCollection of child elements

```

### **c. `firstChild` and `lastChild`**

- Returns the first or last child node, including text and comment nodes.

**Example:**

```jsx
console.log(parent.firstChild); // First child node
console.log(parent.lastChild); // Last child node

```

### **d. `firstElementChild` and `lastElementChild`**

- Returns the first or last child that is an HTML element.

**Example:**

```jsx
console.log(parent.firstElementChild); // First child element
console.log(parent.lastElementChild); // Last child element

```

---

### **3. Traversing Siblings**

### **a. `nextSibling` and `previousSibling`**

- Returns the next or previous sibling node, including text and comment nodes.

**Example:**

```jsx
const current = document.querySelector(".current");
console.log(current.nextSibling); // Next sibling node
console.log(current.previousSibling); // Previous sibling node

```

### **b. `nextElementSibling` and `previousElementSibling`**

- Returns the next or previous sibling that is an HTML element.

**Example:**

```jsx
console.log(current.nextElementSibling); // Next sibling element
console.log(current.previousElementSibling); // Previous sibling element

```

---

### **Events and Listeners**

Events in JavaScript represent interactions or occurrences on the webpage, such as clicking a button, hovering over an element, typing in a field, or loading the page. Event listeners allow you to execute JavaScript code in response to these events.

---

### **1. Adding Event Listeners**

### **a. Using `addEventListener()`**

- The recommended method to attach an event listener to an element.
- Syntax:
    
    ```jsx
    element.addEventListener(event, handler, options);
    
    ```
    

**Example:**

```jsx
const button = document.querySelector("#myButton");

button.addEventListener("click", () => {
    console.log("Button clicked!");
});

```

### **b. Inline Event Listeners (Not Recommended)**

- You can define event handlers directly in HTML attributes like `onclick`, but this is less maintainable.

**Example:**

```html
<button onclick="alert('Button clicked!')">Click Me</button>

```

### **c. Assigning Event Handlers with Properties**

- Use event handler properties like `onclick` or `onmouseover`.

**Example:**

```jsx
const button = document.querySelector("#myButton");

button.onclick = () => {
    console.log("Button clicked!");
};

```

---

### **2. Commonly Used Events**

| Event Name | Description |
| --- | --- |
| `click` | Fires when an element is clicked. |
| `mouseover` | Fires when the mouse pointer enters an element. |
| `mouseout` | Fires when the mouse pointer leaves an element. |
| `keydown` | Fires when a key is pressed. |
| `keyup` | Fires when a key is released. |
| `submit` | Fires when a form is submitted. |
| `change` | Fires when the value of an input element changes. |
| `input` | Fires on any change to an input element's value. |
| `load` | Fires when the page or an image is fully loaded. |
| `scroll` | Fires when the user scrolls. |

---

### **3. Removing Event Listeners**

Use `removeEventListener()` to remove an event listener that was added with `addEventListener`.

**Example:**

```jsx
function handleClick() {
    console.log("Button clicked!");
}

const button = document.querySelector("#myButton");

// Add listener
button.addEventListener("click", handleClick);

// Remove listener
button.removeEventListener("click", handleClick);

```

---

### **4. Event Object**

When an event occurs, an **event object** is automatically passed to the event handler. It contains information about the event and the element that triggered it.

### **Common Properties of the Event Object:**

| Property | Description |
| --- | --- |
| `type` | The type of event (e.g., `click`, `keydown`). |
| `target` | The element that triggered the event. |
| `currentTarget` | The element the event listener is attached to. |
| `preventDefault()` | Prevents the default action of the event. |
| `stopPropagation()` | Stops the event from bubbling up or capturing down. |

**Example:**

```jsx
document.querySelector("#myButton").addEventListener("click", (event) => {
    console.log("Event type:", event.type); // "click"
    console.log("Event target:", event.target); // The button element
    event.preventDefault(); // Prevent default action (if any)
});

```

---

### **5. Event Bubbling and Capturing**

### **Event Bubbling:**

- Events propagate **up** the DOM tree from the target element to its ancestors.

### **Event Capturing:**

- Events propagate **down** the DOM tree from the root to the target element.

**Example of Bubbling:**

```jsx
document.querySelector("#child").addEventListener("click", () => {
    console.log("Child clicked!");
});
document.querySelector("#parent").addEventListener("click", () => {
    console.log("Parent clicked!");
});

```

When you click the child, the output will be:

```
Child clicked!
Parent clicked!

```

To capture the event, use `{ capture: true }` in `addEventListener`:

```jsx
document.querySelector("#parent").addEventListener("click", () => {
    console.log("Parent clicked during capture phase!");
}, { capture: true });

```

---

### **Unit: JavaScript HTTP**

### **JSON**

- JSON (JavaScript Object Notation) is a lightweight data format used to store and exchange data.
    - Example:
        
        ```jsx
        const obj = { name: "Alice", age: 25 };
        const jsonStr = JSON.stringify(obj);  // Convert to JSON string
        
        ```
        

---

### **Promises, Fetch API, and Async/Await in JavaScript**

These features enable asynchronous programming in JavaScript, allowing you to handle tasks like fetching data from APIs, reading files, or executing long-running processes without blocking the main thread.

---

## **1. Promises**

### **What is a Promise?**

A **Promise** represents a value that might be available now, in the future, or never. It can have one of three states:

1. **Pending**: The operation is still in progress.
2. **Fulfilled**: The operation completed successfully.
3. **Rejected**: The operation failed.

### **Creating a Promise**

```jsx
const myPromise = new Promise((resolve, reject) => {
    const success = true;

    if (success) {
        resolve("Operation succeeded!");
    } else {
        reject("Operation failed!");
    }
});

// Handling the Promise
myPromise
    .then(result => console.log(result)) // Runs if resolved
    .catch(error => console.error(error)) // Runs if rejected
    .finally(() => console.log("Promise completed"));

```

---

## **2. Fetch API**

The **Fetch API** is a modern way to make HTTP requests. It returns a Promise that resolves with the `Response` object.

### **Basic Fetch Example**

```jsx
fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => {
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json(); // Parse JSON response
    })
    .then(data => console.log(data)) // Log the data
    .catch(error => console.error("Fetch error:", error)); // Handle errors

```

### **Posting Data Using Fetch**

```jsx
fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        title: "foo",
        body: "bar",
        userId: 1
    })
})
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error("Fetch error:", error));

```

---

## **3. Async/Await**

### **What is Async/Await?**

- **`async`**: Declares a function that returns a Promise.
- **`await`**: Pauses the execution of the async function until the Promise is resolved or rejected.

### **Example with Async/Await**

```jsx
const fetchData = async () => {
    try {
        const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Error fetching data:", error);
    }
};

fetchData();

```

---

### **Chaining Async Operations**

```jsx
const fetchPostsAndUsers = async () => {
    try {
        const postsResponse = await fetch("https://jsonplaceholder.typicode.com/posts");
        const posts = await postsResponse.json();

        const userResponse = await fetch("https://jsonplaceholder.typicode.com/users/1");
        const user = await userResponse.json();

        console.log("Posts:", posts);
        console.log("User:", user);
    } catch (error) {
        console.error("Error:", error);
    }
};

fetchPostsAndUsers();

```

---

### **Error Handling in Async/Await**

Use `try...catch` to handle errors in asynchronous functions.

```jsx
const fetchWithErrorHandling = async () => {
    try {
        const response = await fetch("https://invalid.url");
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Caught an error:", error);
    }
};

fetchWithErrorHandling();

```

---

### **Comparison of Promises, Fetch, and Async/Await**

| Feature | Promises | Fetch API | Async/Await |
| --- | --- | --- | --- |
| **Ease of Use** | Slightly verbose | Simplifies HTTP requests | Most concise for async tasks |
| **Error Handling** | `.catch()` | `.catch()` | `try...catch` |
| **Asynchronous Flow** | Chaining with `.then()` | Used with `.then()` or async/await | Sequential, like synchronous code |
| **Modern Use** | Core of async patterns | Built-in HTTP client | Best for clean async code |

---

### **Combining Fetch with Async/Await**

```jsx
const fetchPost = async () => {
    const url = "https://jsonplaceholder.typicode.com/posts";
    try {
        // Fetch posts
        const response = await fetch(url);
        if (!response.ok) throw new Error(`Error: ${response.status}`);

        // Parse response
        const posts = await response.json();
        console.log("Posts:", posts);
    } catch (error) {
        console.error("Fetch error:", error);
    }
};

fetchPost();

```

---

### **Unit: JavaScript Testing**

---

### **AAA Pattern**

- **Arrange**: Set up the conditions for the test.
- **Act**: Execute the code being tested.
- **Assert**: Verify the result.

---

### **Jest Overview**

**Jest** is a popular JavaScript testing framework developed by Facebook. It is widely used for testing JavaScript applications, especially React applications. Jest provides a rich API for writing unit tests, mocking dependencies, and generating code coverage reports.

---

## **1. Jest Introduction**

### **Key Features of Jest:**

- **Zero Configuration:** Works out of the box for most JavaScript projects.
- **Snapshot Testing:** Verifies that UI components match their previous output.
- **Mocks:** Provides tools to mock functions, modules, and timers.
- **Code Coverage:** Generates code coverage reports for tested code.
- **Runs Tests in Parallel:** Optimizes test execution speed.

---

### **Getting Started with Jest**

1. **Install Jest:**
    
    ```bash
    npm install --save-dev jest
    
    ```
    
2. **Add a Test Script:**
In `package.json`:
    
    ```json
    "scripts": {
      "test": "jest"
    }
    
    ```
    
3. **Run Tests:**
    
    ```bash
    npm test
    
    ```
    
4. **Example Test File:**
Jest looks for test files in a `__tests__` folder or files with `.test.js` or `.spec.js` extensions.
    
    ```jsx
    // sum.js
    const sum = (a, b) => a + b;
    module.exports = sum;
    
    // sum.test.js
    const sum = require('./sum');
    
    test('adds 1 + 2 to equal 3', () => {
        expect(sum(1, 2)).toBe(3);
    });
    
    ```
    

---

## **2. Jest Expect**

The `expect` function is used to create assertions in Jest. It allows you to test the behavior of your code.

### **Basic Matchers**

1. **Equality Matchers:**
    
    ```jsx
    expect(2 + 2).toBe(4); // Exact equality
    expect({ name: "Alice" }).toEqual({ name: "Alice" }); // Object equality
    
    ```
    
2. **Truthy/Falsy Matchers:**
    
    ```jsx
    expect(true).toBeTruthy();
    expect(false).toBeFalsy();
    expect(undefined).toBeUndefined();
    expect(null).toBeNull();
    
    ```
    
3. **Numbers:**
    
    ```jsx
    expect(4).toBeGreaterThan(3);
    expect(4).toBeGreaterThanOrEqual(4);
    expect(3).toBeLessThan(5);
    
    ```
    
4. **Strings:**
    
    ```jsx
    expect("Hello World").toMatch(/World/);
    
    ```
    
5. **Arrays and Iterables:**
    
    ```jsx
    expect([1, 2, 3]).toContain(2);
    
    ```
    
6. **Exceptions:**
    
    ```jsx
    const throwError = () => {
        throw new Error("Test error");
    };
    expect(throwError).toThrow("Test error");
    
    ```
    

---

## **3. Mock Functions**

Mock functions allow you to:

1. **Track calls and arguments** to a function.
2. **Provide custom implementations** for dependencies.
3. **Replace parts of code that are hard to test.**

### **Creating a Mock Function**

1. **Basic Mock Function:**
    
    ```jsx
    const mockFn = jest.fn();
    
    mockFn(1, 2);
    expect(mockFn).toHaveBeenCalled(); // Check if it was called
    expect(mockFn).toHaveBeenCalledWith(1, 2); // Check arguments
    
    ```
    
2. **Mock Implementation:**
    
    ```jsx
    const mockFn = jest.fn((a, b) => a + b);
    
    expect(mockFn(2, 3)).toBe(5);
    
    ```
    
3. **Mock Return Values:**
    
    ```jsx
    const mockFn = jest.fn();
    mockFn.mockReturnValue(42);
    
    expect(mockFn()).toBe(42);
    
    ```
    
4. **Mocking Modules:**
    
    ```jsx
    jest.mock('./module', () => ({
        fetchData: jest.fn(() => Promise.resolve({ data: "mocked data" })),
    }));
    
    const { fetchData } = require('./module');
    test('mocked fetchData', async () => {
        const result = await fetchData();
        expect(result.data).toBe("mocked data");
    });
    
    ```
    

---

## **4. Code Coverage**

Code coverage is a metric to determine how much of your source code is tested by your tests. Jest can generate coverage reports with a simple configuration.

### **Enable Code Coverage**

1. **Run Jest with Coverage:**
    
    ```bash
    jest --coverage
    
    ```
    
2. **Configure Coverage in `package.json`:**
    
    ```json
    "jest": {
      "collectCoverage": true,
      "coverageDirectory": "coverage",
      "collectCoverageFrom": [
        "src/**/*.js"
      ]
    }
    
    ```
    
3. **Output:**
Jest will generate a `coverage/` folder with detailed HTML reports.

### **Coverage Metrics:**

- **Statements:** Percentage of executable statements covered.
- **Branches:** Percentage of branches in conditional statements covered.
- **Functions:** Percentage of functions executed.
- **Lines:** Percentage of lines executed.

---
