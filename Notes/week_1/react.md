# React Notes

### **Webpack**

- Webpack is a module bundler used in React projects to compile JavaScript, CSS, and other files into a bundle for deployment.
- **Core Features**:
    - **Loaders**: Process files other than JavaScript, e.g., CSS or images.
    - **Plugins**: Enhance functionality like minification or environment variables.
    - Example `webpack.config.js`:
        
        ```jsx
        const path = require('path');
        module.exports = {
          entry: './src/index.js',
          output: {
            filename: 'bundle.js',
            path: path.resolve(__dirname, 'dist'),
          },
          module: {
            rules: [
              { test: /\.css$/, use: ['style-loader', 'css-loader'] },
            ],
          },
        };
        
        ```
        

---

### **Single Page Applications (SPAs)**

- SPAs dynamically update content without reloading the entire page.
- React enables building SPAs by using the Virtual DOM and efficient state management.

---

### **React Introduction**

- React is a JavaScript library for building user interfaces, maintained by Facebook.
- Core Concepts:
    - Component-based architecture.
    - Declarative views.
    - React Virtual DOM for efficient rendering.

---

### **React Setup**

- Use **Create React App (CRA)**:
    
    ```bash
    npx create-react-app my-app
    cd my-app
    npm start
    
    ```
    
- For custom setups, configure Webpack and Babel.

---

### **Library vs Framework**

- **Library**: Focuses on specific functionality (e.g., React).
- **Framework**: Provides a full-stack solution (e.g., Angular).

---

### **React with JavaScript vs TypeScript**

- JavaScript is flexible, but TypeScript adds type safety and enhanced IDE support.
- TypeScript requires `.tsx` files, where you define types explicitly.

---

### **React vs React Native vs Angular**

- **React**: For web apps; component-based.
- **React Native**: For mobile apps; uses native components.
- **Angular**: Framework for building full-scale web applications with dependency injection and two-way data binding.

---

### **Unit: React Foundation**

### **React Component Architecture**

React's component architecture is a modular approach to building user interfaces. Components are the building blocks of React applications, encapsulating logic, structure, and styling in a reusable and maintainable manner.

---

### **Core Principles of React Components**

1. **Reusable**:
    - Components are designed to be reused across the application, reducing code duplication.
2. **Declarative**:
    - React components describe **what** the UI should look like, rather than specifying **how** to achieve it.
3. **Composable**:
    - Small components can be combined to build larger, more complex components.
4. **Encapsulation**:
    - Each component manages its state and logic, isolating it from others.

---

### **Component Types**

1. **Functional Components** (Stateless):
    - Simple JavaScript functions.
    - Best suited for presentational logic.
    - Can use **React Hooks** for state and side effects.
    
    ```jsx
    function Greeting({ name }) {
      return <h1>Hello, {name}!</h1>;
    }
    
    ```
    
2. **Class Components** (Stateful):
    - ES6 classes extending `React.Component`.
    - Use `state` and lifecycle methods.
    
    ```jsx
    class Greeting extends React.Component {
      render() {
        return <h1>Hello, {this.props.name}!</h1>;
      }
    }
    
    ```
    

---

### **Component Structure**

A typical React component consists of the following:

1. **Import Statements**:
    - Importing React, other libraries, or child components.
2. **Component Logic**:
    - State, props, and event handlers.
3. **JSX Template**:
    - The returned UI structure.
4. **Styling**:
    - Inline styles, CSS modules, or external stylesheets.

### Example:

```jsx
import React from 'react';

function Button({ label, onClick }) {
  return (
    <button onClick={onClick}>
      {label}
    </button>
  );
}

export default Button;

```

---

### **Component Architecture Patterns**

### **1. Container and Presentational Components**

- **Presentational Components**:
    - Focus on UI rendering.
    - Receive data via `props`.
    
    ```jsx
    function UserCard({ user }) {
      return (
        <div>
          <h2>{user.name}</h2>
          <p>{user.email}</p>
        </div>
      );
    }
    
    ```
    
- **Container Components**:
    - Handle data fetching, state, and business logic.
    - Pass data to presentational components.
    
    ```jsx
    function UserListContainer() {
      const [users, setUsers] = React.useState([]);
    
      React.useEffect(() => {
        fetch('/api/users')
          .then((res) => res.json())
          .then((data) => setUsers(data));
      }, []);
    
      return (
        <div>
          {users.map((user) => (
            <UserCard key={user.id} user={user} />
          ))}
        </div>
      );
    }
    
    ```
    

---

### **2. Higher-Order Components (HOC)**

- A pattern for reusing component logic by wrapping one component with another.
- Commonly used for authentication, logging, or data-fetching logic.

```jsx
function withAuth(Component) {
  return function AuthenticatedComponent(props) {
    const isAuthenticated = useAuth();
    return isAuthenticated ? <Component {...props} /> : <p>Please log in.</p>;
  };
}

const DashboardWithAuth = withAuth(Dashboard);

```

---

### **3. Render Props**

- A technique for sharing logic between components by using a render function.

```jsx
function DataFetcher({ url, render }) {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch(url).then((res) => res.json()).then(setData);
  }, [url]);

  return render(data);
}

// Usage
<DataFetcher
  url="/api/users"
  render={(data) => (
    data ? <UserList users={data} /> : <p>Loading...</p>
  )}
/>;

```

---

### **Component Communication**

1. **Props**:
    - Pass data from parent to child components.
    
    ```jsx
    function Parent() {
      return <Child message="Hello!" />;
    }
    
    function Child({ message }) {
      return <p>{message}</p>;
    }
    
    ```
    
2. **State Lifting**:
    - Share state between components by lifting it to the nearest common parent.
    
    ```jsx
    function Parent() {
      const [count, setCount] = React.useState(0);
    
      return (
        <div>
          <Child1 count={count} />
          <Child2 setCount={setCount} />
        </div>
      );
    }
    
    ```
    
3. **Context API**:
    - Share data across components without explicitly passing props.
    
    ```jsx
    const ThemeContext = React.createContext();
    
    function App() {
      const theme = 'dark';
    
      return (
        <ThemeContext.Provider value={theme}>
          <Child />
        </ThemeContext.Provider>
      );
    }
    
    function Child() {
      const theme = React.useContext(ThemeContext);
      return <p>Theme: {theme}</p>;
    }
    
    ```
    

---

### **File Organization**

Organize components in a structured manner for better maintainability.

### Example Directory Structure:

```
src/
¿¿¿ components/
¿   ¿¿¿ Header/
¿   ¿   ¿¿¿ Header.tsx
¿   ¿   ¿¿¿ Header.css
¿   ¿   ¿¿¿ Header.test.tsx
¿   ¿¿¿ Footer/
¿   ¿   ¿¿¿ Footer.tsx
¿   ¿¿¿ Button/
¿       ¿¿¿ Button.tsx
¿       ¿¿¿ Button.styled.ts
¿¿¿ hooks/
¿   ¿¿¿ useFetch.ts
¿   ¿¿¿ useAuth.ts
¿¿¿ context/
¿   ¿¿¿ ThemeContext.tsx
¿¿¿ App.tsx

```

---

### **Best Practices**

1. **Keep Components Small**:
    - Break components into smaller units for better readability and reuse.
2. **Use Descriptive Names**:
    - Name components and files meaningfully (e.g., `UserCard` instead of `Card`).
3. **Leverage Composition**:
    - Favor composition over inheritance for component reuse.
4. **Prop-Drilling**:
    - Avoid excessive prop drilling; use context or state management libraries.
5. **Test Components**:
    - Use testing libraries like Jest and React Testing Library to test components.

---

### **React JSX**

### **JSX (JavaScript XML)**

JSX is a syntax extension for JavaScript that resembles XML or HTML. It is commonly used with React to define UI components and layouts. JSX allows you to write HTML-like structures directly in JavaScript, making your code more readable and expressive.

---

### **Why Use JSX?**

1. **Declarative Syntax**:
    - Makes code easier to read and understand.
    
    ```jsx
    const element = <h1>Hello, World!</h1>;
    
    ```
    
2. **JavaScript Integration**:
    - Embed JavaScript expressions directly within JSX.
    
    ```jsx
    const name = "Alice";
    const greeting = <h1>Hello, {name}!</h1>;
    
    ```
    
3. **Powerful Abstraction**:
    - JSX compiles to `React.createElement` calls, enabling virtual DOM rendering.

---

### **Basic JSX Syntax**

1. **Embedding JavaScript**:
    - Use curly braces `{}` to insert JavaScript expressions.
    
    ```jsx
    const element = <h1>{1 + 1}</h1>; // Output: <h1>2</h1>
    
    ```
    
2. **Attributes**:
    - Use camelCase for attributes in JSX.
    
    ```jsx
    const button = <button className="btn" disabled={true}>Click Me</button>;
    
    ```
    
3. **Child Elements**:
    - JSX can have nested elements.
    
    ```jsx
    const element = (
      <div>
        <h1>Hello, World!</h1>
        <p>Welcome to JSX.</p>
      </div>
    );
    
    ```
    

---

### **React Virtual DOM**

The **Virtual DOM** is a lightweight, in-memory representation of the **real DOM**. It is one of the core concepts behind React's performance and efficiency. React uses the Virtual DOM to optimize updates to the UI by minimizing direct manipulations of the real DOM.

---

### **How Does the Virtual DOM Work?**

1. **Initial Render**:
    - When a React application is loaded, the UI is represented as a Virtual DOM tree (a JavaScript object).
2. **State or Prop Changes**:
    - When the state or props of a component change, React creates a new Virtual DOM tree to reflect the updated UI.
3. **Diffing Algorithm**:
    - React compares the new Virtual DOM tree with the previous one using a **diffing algorithm** to determine the minimal set of changes needed.
4. **Reconciliation**:
    - React reconciles the changes by updating only the affected parts of the real DOM, rather than re-rendering the entire UI.
5. **Real DOM Updates**:
    - The calculated changes are applied to the real DOM in a single batch for optimal performance.

---

### **Advantages of the Virtual DOM**

1. **Performance**:
    - Real DOM updates are slow because they trigger layout recalculations and re-rendering. The Virtual DOM minimizes these updates by batching them.
2. **Efficiency**:
    - By comparing the old and new Virtual DOM trees, React applies only the necessary updates, avoiding unnecessary DOM manipulations.
3. **Declarative Programming**:
    - Developers describe the desired UI state, and React manages the actual updates under the hood.

---

### **Example Workflow**

### Without Virtual DOM:

1. **State Change**:
    - Update directly modifies the real DOM.
2. **Real DOM Update**:
    - Triggers a reflow and repaint, which can be costly for large-scale applications.

### With Virtual DOM:

1. **State Change**:
    - React creates a new Virtual DOM.
2. **Diffing**:
    - React compares the old and new Virtual DOM.
3. **Update Real DOM**:
    - React applies only the calculated changes to the real DOM.

---

### **Performance Benefits**

1. **Reduced Repaints and Reflows**:
    - Updates are applied in batches, reducing the frequency of costly DOM recalculations.
2. **Optimized Rendering**:
    - React avoids re-rendering components or DOM elements that haven¿t changed.
3. **Consistency Across Platforms**:
    - The Virtual DOM abstraction works for both browsers (real DOM) and native environments (React Native).

---

### **Misconceptions About the Virtual DOM**

1. **Not Faster Than Real DOM**:
    - Manipulating the real DOM isn't inherently slow. It's the excessive and inefficient updates that are costly. The Virtual DOM optimizes this process.
2. **Only a Concept**:
    - Virtual DOM isn't a browser feature or specification; it's an abstraction implemented by libraries like React.

---

### **Conditional Rendering**

- Display components based on conditions.
    - Example:
        
        ```jsx
        const isLoggedIn = true;
        return isLoggedIn ? <h1>Welcome!</h1> : <h1>Please log in.</h1>;
        
        ```
        

---

### **Lists and Keys**

- Keys are used to uniquely identify elements in a list.
    - Example:
        
        ```jsx
        const items = ['Apple', 'Banana'];
        const list = items.map((item, index) => <li key={index}>{item}</li>);
        
        ```
        

---

### **Event Handling**

- React uses camelCase for event names.
    - Example:
        
        ```jsx
        function handleClick() {
          alert('Button clicked!');
        }
        <button onClick={handleClick}>Click Me</button>
        
        ```
        

### **Unit: React Lifecycle and Hooks**

---

### **React Component Lifecycle**

The **React Component Lifecycle** refers to the series of methods and events that a React component goes through during its lifetime. This lifecycle is divided into three main phases:

1. **Mounting**: When the component is being created and inserted into the DOM.
2. **Updating**: When the component is being re-rendered due to changes in props, state, or context.
3. **Unmounting**: When the component is being removed from the DOM.

---

### **Lifecycle Methods**

### 1. **Mounting Phase**

This phase involves the initial creation and insertion of a component into the DOM.

- **`constructor()`**:
    - Initializes the component.
    - Used to set up state and bind methods.
    
    ```jsx
    constructor(props) {
      super(props);
      this.state = { count: 0 };
    }
    
    ```
    
- **`static getDerivedStateFromProps(props, state)`**:
    - Synchronizes state with props.
    - Rarely used; avoids side effects.
    
    ```jsx
    static getDerivedStateFromProps(props, state) {
      if (props.value !== state.value) {
        return { value: props.value };
      }
      return null;
    }
    
    ```
    
- **`render()`**:
    - Describes the UI structure.
    - Returns JSX or `null`.
    
    ```jsx
    render() {
      return <h1>Hello, {this.props.name}!</h1>;
    }
    
    ```
    
- **`componentDidMount()`**:
    - Invoked once the component is inserted into the DOM.
    - Used for side effects like fetching data or setting up subscriptions.
    
    ```jsx
    componentDidMount() {
      fetch('/api/data')
        .then((response) => response.json())
        .then((data) => this.setState({ data }));
    }
    
    ```
    

---

### 2. **Updating Phase**

This phase occurs when the component is re-rendered due to state, props, or context changes.

- **`static getDerivedStateFromProps(props, state)`**:
    - Also called during updates.
    - Allows updating state based on new props.
- **`shouldComponentUpdate(nextProps, nextState)`**:
    - Determines whether the component should re-render.
    - Used to optimize performance.
    
    ```jsx
    shouldComponentUpdate(nextProps, nextState) {
      return nextProps.value !== this.props.value;
    }
    
    ```
    
- **`render()`**:
    - Re-renders the UI with updated state/props.
- **`getSnapshotBeforeUpdate(prevProps, prevState)`**:
    - Captures some information from the DOM before updates are applied.
    - The value returned is passed to `componentDidUpdate`.
    
    ```jsx
    getSnapshotBeforeUpdate(prevProps, prevState) {
      if (prevProps.scrollPosition !== this.props.scrollPosition) {
        return this.divRef.scrollHeight;
      }
      return null;
    }
    
    ```
    
- **`componentDidUpdate(prevProps, prevState, snapshot)`**:
    - Invoked after the component updates.
    - Commonly used for DOM manipulations or additional data fetching.
    
    ```jsx
    componentDidUpdate(prevProps, prevState, snapshot) {
      if (snapshot !== null) {
        console.log('Previous scroll height:', snapshot);
      }
    }
    
    ```
    

---

### 3. **Unmounting Phase**

This phase occurs when the component is removed from the DOM.

- **`componentWillUnmount()`**:
    - Used to clean up resources like event listeners or timers.
    
    ```jsx
    componentWillUnmount() {
      clearInterval(this.timer);
    }
    
    ```
    

---

### **Key Differences**

| **Class Components** | **Functional Components (Hooks)** |
| --- | --- |
| Lifecycle methods like `componentDidMount` | Uses `useEffect` for lifecycle behaviors. |
| Stateful with `this.state` | Stateful with `useState`. |
| Requires method binding | No need for method binding. |
| More boilerplate code | Concise and easier to write. |

---

### **Best Practices**

1. **Use Functional Components**:
    - Prefer functional components with Hooks unless there¿s a specific need for class components.
2. **Minimize Side Effects**:
    - Keep side effects (like data fetching) isolated in `useEffect` or lifecycle methods.
3. **Optimize Rendering**:
    - Use `shouldComponentUpdate`, `React.memo`, or the dependency array in `useEffect` to optimize performance.

By understanding and effectively using React's lifecycle, you can build dynamic, optimized, and maintainable applications.

---

### **React Hooks**

React **Hooks** are functions introduced in React 16.8 that allow you to use state and other React features in **functional components**. Hooks simplify component logic, improve readability, and eliminate the need for class components in many cases.

---

### **Why Use Hooks?**

1. **State Management in Functional Components**:
    - Hooks bring `state` and `lifecycle` methods to functional components.
2. **Simplify Code**:
    - Avoid boilerplate associated with class components (like `this`, binding, etc.).
3. **Reuse Logic**:
    - Custom Hooks allow you to encapsulate and reuse stateful logic.

---

### **Basic Hooks**

### **1. `useState`**

Manages local state in a functional component.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Declare state variable

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

```

- **Syntax**:
    
    ```jsx
    const [state, setState] = useState(initialValue);
    
    ```
    

---

### **2. `useEffect`**

Handles side effects (e.g., data fetching, subscriptions, or DOM updates).

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds((s) => s + 1), 1000);
    return () => clearInterval(interval); // Cleanup
  }, []); // Empty dependency array: effect runs only on mount/unmount

  return <p>Elapsed Time: {seconds}s</p>;
}

```

- **Syntax**:
    
    ```jsx
    useEffect(() => {
      // Side effect logic
      return () => {
        // Cleanup logic (optional)
      };
    }, [dependencies]);
    
    ```
    

---

### **3. `useContext`**

---

### **Using `useContext` for User Authentication**

We¿ll create a `UserContext` to manage the logged-in user state and provide methods for logging in and logging out. Components will consume the context to access the user's information.

---

### **1. Define the Context**

### **Create the `UserContext`**

```tsx
import React, { createContext, ReactNode, useContext, useState } from 'react';

// Define the shape of the context value
interface User {
  username: string;
}

interface UserContextType {
  user: User | null;
  login: (username: string) => void;
  logout: () => void;
}

// Create the context with a default value
export const UserContext = createContext<UserContextType | undefined>(undefined);
```

### **Create the Provider**

```tsx
interface UserProviderProps {
  children: ReactNode;
}

export const UserProvider: React.FC<UserProviderProps> = ({ children }) => {
  const [user, setUser] = useState<User | null>(null);

  const login = (username: string) => {
    setUser({ username });
  };

  const logout = () => {
    setUser(null);
  };

  return (
    <UserContext.Provider value={{ user, login, logout }}>
      {children}
    </UserContext.Provider>
  );
};

```

---

### **2. Consuming the Context**

### **Login Component**

This component allows the user to log in by providing their username.

```tsx
import React, { useContext, useState } from 'react';
import { UserContext } from './Context/UserContext';

const Login: React.FC = () => {
  const [username, setUsername] = useState<string>('');
  const context = useContext(UserContext);

  if (!context) {
    throw new Error('Login must be used within a UserProvider');
  }

  const { login } = context;

  const handleLogin = () => {
    login(username);
  };

  return (
    <div>
      <input
        type="text"
        placeholder="Enter your username"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
      />
      <button onClick={handleLogin}>Login</button>
    </div>
  );
};

export default Login;

```

---

### **User Info Component**

This component displays the logged-in user's information and provides a logout button.

```tsx
import React, { useContext } from 'react';
import { UserContext } from '../Context/UserContext';

const UserInfo: React.FC = () => {
  const context = useContext(UserContext);

  if (!context) {
    throw new Error('UserInfo must be used within a UserProvider');
  }

  const { user, logout } = context;

  return (
    <div>
      {user ? (
        <div>
          <p>Welcome, {user.username}!</p>
          <button onClick={logout}>Logout</button>
        </div>
      ) : (
        <p>No user logged in.</p>
      )}
    </div>
  );
};

export default UserInfo;

```

---

### **3. Wrapping the Application**

Wrap the components in the `UserProvider` to make the context available.

```tsx
import React from 'react';
import ReactDOM from 'react-dom';
import { UserProvider } from './UserContext';
import Login from './Login';
import UserInfo from './UserInfo';

const App: React.FC = () => (
  <UserProvider>
    <div>
      <h1>React TypeScript UseContext Example</h1>
      <Login />
      <UserInfo />
    </div>
  </UserProvider>
);

ReactDOM.render(<App />, document.getElementById('root'));

```

---

### **Key Points**

1. **Type Definition**:
    - Use TypeScript interfaces (`User` and `UserContextType`) to define the shape of the user object and context.
2. **Context Default Value**:
    - Use `undefined` as the default value for `createContext` and handle the absence of context explicitly.
3. **State Management**:
    - The `UserProvider` manages the `user` state and provides `login` and `logout` methods.
4. **Direct Use of `useContext`**:
    - Use `useContext` directly in components like `Login` and `UserInfo` to access the context.

---

This implementation shows how to manage user authentication with `useContext` and TypeScript, ensuring type safety and a clean architecture.

---

### **4. `useReducer`**

### **1. Define the Reducer and Context**

### **Create the Reducer**

Define the reducer function to handle authentication actions (`login`, `logout`).

```tsx
import React, { createContext, useContext, useReducer, ReactNode } from 'react';

// Define User and Actions
interface User {
  username: string;
}

interface AuthState {
  user: User | null;
}

type AuthAction =
  | { type: 'LOGIN'; payload: User }
  | { type: 'LOGOUT' };

// Reducer Function
const authReducer = (state: AuthState, action: AuthAction): AuthState => {
  switch (action.type) {
    case 'LOGIN':
      return { user: action.payload };
    case 'LOGOUT':
      return { user: null };
    default:
      throw new Error(`Unhandled action type: ${action.type}`);
  }
};

```

---

### **Create the Context**

Set up the context with TypeScript.

```tsx
// Context Type
interface AuthContextType {
  state: AuthState;
  dispatch: React.Dispatch<AuthAction>;
}

// Create Context
const AuthContext = createContext<AuthContextType | undefined>(undefined);

// Initial State
const initialAuthState: AuthState = {
  user: null,
};

// Provider Component
interface AuthProviderProps {
  children: ReactNode;
}

export const AuthProvider: React.FC<AuthProviderProps> = ({ children }) => {
  const [state, dispatch] = useReducer(authReducer, initialAuthState);

  return (
    <AuthContext.Provider value={{ state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
};

```

---

### **2. Consuming the Context**

### **Login Component**

This component dispatches a `LOGIN` action when a user logs in.

```tsx
import React, { useContext, useState } from 'react';
import { AuthContext } from './AuthContext';

const Login: React.FC = () => {
  const [username, setUsername] = useState<string>('');
  const context = useContext(AuthContext);

  if (!context) {
    throw new Error('Login must be used within an AuthProvider');
  }

  const { dispatch } = context;

  const handleLogin = () => {
    dispatch({ type: 'LOGIN', payload: { username } });
  };

  return (
    <div>
      <input
        type="text"
        placeholder="Enter your username"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
      />
      <button onClick={handleLogin}>Login</button>
    </div>
  );
};

export default Login;

```

---

### **User Info Component**

This component displays the user information and dispatches a `LOGOUT` action.

```tsx
import React, { useContext } from 'react';
import { AuthContext } from './AuthContext';

const UserInfo: React.FC = () => {
  const context = useContext(AuthContext);

  if (!context) {
    throw new Error('UserInfo must be used within an AuthProvider');
  }

  const { state, dispatch } = context;

  return (
    <div>
      {state.user ? (
        <div>
          <p>Welcome, {state.user.username}!</p>
          <button onClick={() => dispatch({ type: 'LOGOUT' })}>Logout</button>
        </div>
      ) : (
        <p>No user logged in.</p>
      )}
    </div>
  );
};

export default UserInfo;

```

---

### **3. Wrapping the Application**

Wrap the application in the `AuthProvider` to provide the context to all components.

```tsx
import React from 'react';
import ReactDOM from 'react-dom';
import { AuthProvider } from './AuthContext';
import Login from './Login';
import UserInfo from './UserInfo';

const App: React.FC = () => (
  <AuthProvider>
    <div>
      <h1>React TypeScript UseContext + UseReducer Example</h1>
      <Login />
      <UserInfo />
    </div>
  </AuthProvider>
);

ReactDOM.render(<App />, document.getElementById('root'));

```

---

---

### **Unit: React State Management**

### **State Management in React**

State management is the process of controlling how data flows and is shared between components in a React application. In React, the **state** represents the dynamic data that influences how a component renders and behaves.

---

### **Levels of State**

1. **Local State**:
    - Managed within a single component using `useState` or `useReducer`.
    - Example: Form inputs, toggles, counters.
2. **Global State**:
    - Shared across multiple components.
    - Example: User authentication status, themes, or app-wide settings.
3. **Server State**:
    - Represents data fetched from an external API or database.
    - Often managed using libraries like **React Query** or handled manually with hooks.
4. **URL State**:
    - Includes data managed in the URL, like query parameters or routes.
    - Managed with libraries like **React Router**.

---

### **Techniques for State Management**

### **1. Local State Management**

- **Using `useState`**:
    
    ```jsx
    import React, { useState } from 'react';
    
    function Counter() {
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <p>Count: {count}</p>
          <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
      );
    }
    
    ```
    
- **Using `useReducer` for Complex State**:
    
    ```jsx
    import React, { useReducer } from 'react';
    
    function reducer(state, action) {
      switch (action.type) {
        case 'increment':
          return { count: state.count + 1 };
        case 'decrement':
          return { count: state.count - 1 };
        default:
          throw new Error();
      }
    }
    
    function Counter() {
      const [state, dispatch] = useReducer(reducer, { count: 0 });
    
      return (
        <div>
          <p>Count: {state.count}</p>
          <button onClick={() => dispatch({ type: 'increment' })}>+</button>
          <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
        </div>
      );
    }
    
    ```
    

---

### **2. Global State Management**

When state needs to be shared across multiple components, you can use:

- **React Context API**:
    
    ```jsx
    import React, { createContext, useContext, useState } from 'react';
    
    const ThemeContext = createContext();
    
    function ThemeProvider({ children }) {
      const [theme, setTheme] = useState('light');
      return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
          {children}
        </ThemeContext.Provider>
      );
    }
    
    function App() {
      return (
        <ThemeProvider>
          <Toolbar />
        </ThemeProvider>
      );
    }
    
    function Toolbar() {
      const { theme, setTheme } = useContext(ThemeContext);
      return (
        <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
          Toggle Theme
        </button>
      );
    }
    
    ```
    
- **State Management Libraries**:
    - **Redux**:
        - A predictable state container for JavaScript applications.
        - Centralized store for state, with actions and reducers.
    - **Recoil**:
        - Minimal, React-centric global state management.
    - **Zustand**:
        - A lightweight state management library.

---

### **3. Server State Management**

- **Manual with Hooks**:
    
    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function FetchData() {
      const [data, setData] = useState(null);
    
      useEffect(() => {
        fetch('/api/data')
          .then((response) => response.json())
          .then(setData);
      }, []);
    
      return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
    }
    
    ```
    

---

### **4. URL State Management**

- **React Router**:
    
    ```jsx
    import { BrowserRouter as Router, Route, useParams } from 'react-router-dom';
    
    function UserProfile() {
      const { id } = useParams();
      return <div>User ID: {id}</div>;
    }
    
    function App() {
      return (
        <Router>
          <Route path="/user/:id" component={UserProfile} />
        </Router>
      );
    }
    
    ```
    
- **URL Query Parameters**:
    
    ```jsx
    import { useLocation } from 'react-router-dom';
    
    function Search() {
      const query = new URLSearchParams(useLocation().search);
      return <div>Search Term: {query.get('q')}</div>;
    }
    
    ```
    

---

### **Choosing the Right State Management Approach**

| **Use Case** | **Recommended Solution** |
| --- | --- |
| Local state within a single component | `useState`, `useReducer` |
| Global state shared across components | Context API, Redux, Zustand, Recoil |
| Server state (API calls) | React Query, SWR, Manual Fetching |
| URL or route-based state | React Router |

---

### **Best Practices**

1. **Minimize State**:
    - Store only necessary data in state; derive the rest from props or context.
2. **Use Context Sparingly**:
    - Avoid overusing React Context for deeply nested components as it can cause performance issues.
3. **Optimize Performance**:
    - Memoize functions and components with `useCallback` and `React.memo`.
4. **Split Responsibility**:
    - Divide state management between local, global, and server appropriately.

---

### **Immutability of State, Lifting State, and One-Way Data Flow in React**

These are foundational concepts in React development that ensure predictable updates, maintainable code, and efficient rendering.

---

### **1. Immutability of State**

In React, **state is immutable**, meaning it should not be modified directly. Instead, always create a new copy of the state with the desired changes. This ensures React can properly detect changes and update the DOM efficiently.

### **Why is Immutability Important?**

- **Performance**: React uses a virtual DOM to optimize updates. Immutable changes allow React to efficiently compare old and new states (via shallow comparison).
- **Predictability**: State updates are deterministic and avoid unintended side effects.
- **Debugging**: Immutable states make debugging easier by preserving historical states (useful for tools like Redux DevTools).

### **Correct Way to Update State**

- **Using `useState`:**
    
    ```jsx
    const [list, setList] = useState([1, 2, 3]);
    
    // Add a new item (immutable approach)
    setList([...list, 4]); // Spread operator creates a new array
    
    ```
    
- **Using `useReducer`:**
    
    ```jsx
    function reducer(state, action) {
      switch (action.type) {
        case 'add':
          return { ...state, items: [...state.items, action.payload] }; // Copy state and update
        default:
          return state;
      }
    }
    
    ```
    

---

### **2. Lifting State**

"Lifting state up" refers to moving state to the nearest common ancestor of components that need to share or manage that state. This ensures a **single source of truth** and facilitates the communication between components via props.

### **Why Lift State?**

- Prevents duplication of state across components.
- Centralizes state management.
- Enables one-way data flow by passing state as props.

### **Example of Lifting State**

- **Problem**: Two sibling components need shared state.

```jsx
function TemperatureInput({ label, temperature, onTemperatureChange }) {
  return (
    <div>
      <label>{label}</label>
      <input
        value={temperature}
        onChange={(e) => onTemperatureChange(e.target.value)}
      />
    </div>
  );
}

function TemperatureConverter() {
  const [celsius, setCelsius] = useState('');
  const [fahrenheit, setFahrenheit] = useState('');

  const handleCelsiusChange = (value) => {
    setCelsius(value);
    setFahrenheit((value * 9) / 5 + 32);
  };

  const handleFahrenheitChange = (value) => {
    setFahrenheit(value);
    setCelsius(((value - 32) * 5) / 9);
  };

  return (
    <div>
      <TemperatureInput
        label="Celsius"
        temperature={celsius}
        onTemperatureChange={handleCelsiusChange}
      />
      <TemperatureInput
        label="Fahrenheit"
        temperature={fahrenheit}
        onTemperatureChange={handleFahrenheitChange}
      />
    </div>
  );
}

```

In this example, state is lifted to the `TemperatureConverter` component to synchronize the two inputs.

---

### **3. One-Way Data Flow**

React enforces **one-way data flow**, meaning data flows from **parent to child** via **props**. Child components cannot modify the state of their parents but can communicate changes through callback functions provided as props.

### **Why One-Way Data Flow?**

- Simplifies debugging and reasoning about application state.
- Prevents unexpected side effects caused by uncontrolled state updates.
- Encourages predictable and maintainable component hierarchies.

### **Example of One-Way Data Flow**

```jsx
function Parent() {
  const [message, setMessage] = useState('Hello, World!');

  return (
    <div>
      <Child message={message} onUpdate={(newMessage) => setMessage(newMessage)} />
      <p>Parent Message: {message}</p>
    </div>
  );
}

function Child({ message, onUpdate }) {
  return (
    <div>
      <p>Child Message: {message}</p>
      <button onClick={() => onUpdate('New Message from Child')}>Update</button>
    </div>
  );
}

```

- **Parent Component**: Holds the state.
- **Child Component**: Receives data (`message`) via props and communicates changes (`onUpdate`) back to the parent.

---

### **How These Concepts Work Together**

1. **Immutability** ensures predictable updates, making state easier to manage and debug.
2. **Lifting State** consolidates shared state into a common ancestor to facilitate one-way data flow.
3. **One-Way Data Flow** ensures a clear and predictable flow of data, reducing the complexity of interactions between components.

---

### **Best Practices**

- **Keep State Where It Belongs**: Place state in the most specific parent component where it's needed.
- **Minimize State Duplication**: Avoid having multiple copies of the same state across components.
- **Immutability by Default**: Always treat state as immutable, using tools like the spread operator or libraries like **Immer** for complex updates.
- **Pass Callbacks**: Use functions passed as props for child-to-parent communication instead of letting children modify state directly.

---

### **Unit: React Depth**

### **Styling Components in React**

Styling React components is a crucial part of building attractive and user-friendly applications. React offers multiple ways to style components, each with its strengths and use cases.

---

### **1. Inline Styles**

- **How It Works**: Styles are written as JavaScript objects and passed to the `style` attribute of a component.
- **Pros**:
    - Simple to use for dynamic styles.
    - Scoped to the specific element.
- **Cons**:
    - No support for pseudo-classes (e.g., `:hover`) or media queries.
    - Can become verbose for complex styles.

```jsx
function InlineStyleExample() {
  const style = {
    color: 'blue',
    backgroundColor: 'lightgray',
    padding: '10px',
    borderRadius: '5px',
  };

  return <div style={style}>This is styled inline!</div>;
}

```

---

### **2. CSS Classes**

- **How It Works**: Use traditional CSS files and apply class names to elements using the `className` attribute.
- **Pros**:
    - Familiar for developers experienced with CSS.
    - Full CSS capabilities, including pseudo-classes and media queries.
- **Cons**:
    - Classes are global, which can lead to name conflicts in large projects.

```css
/* styles.css */
.button {
  color: white;
  background-color: blue;
  padding: 10px;
  border-radius: 5px;
}

```

```jsx
import './styles.css';

function CSSClassExample() {
  return <button className="button">Styled with CSS</button>;
}

```

---

### **Handling Forms in React**

Forms in React are used to collect user input. Unlike traditional HTML forms, React uses a controlled or uncontrolled component approach to handle inputs. Each approach offers different benefits depending on the use case.

---

### **1. Controlled Components**

In controlled components, form data is handled by React state. The value of the form elements is controlled through state, making it easy to manage and manipulate.

### **Example: Simple Controlled Form**

```jsx
import { useState } from 'react';

function ControlledForm() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(`Name: ${name}, Email: ${email}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input
          type="text"
          value={name}
          onChange={(e) => setName(e.target.value)}
        />
      </label>
      <br />
      <label>
        Email:
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
      </label>
      <br />
      <button type="submit">Submit</button>
    </form>
  );
}

```

### **Key Points**:

- `value` attribute binds the input to the state.
- `onChange` handler updates the state when the user types.

---

### **2. Uncontrolled Components**

In uncontrolled components, form data is handled by the DOM instead of React state. Accessing data requires `Refs` to directly retrieve input values.

### **Example: Uncontrolled Form**

```jsx
import { useRef } from 'react';

function UncontrolledForm() {
  const nameRef = useRef(null);
  const emailRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(`Name: ${nameRef.current.value}, Email: ${emailRef.current.value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" ref={nameRef} />
      </label>
      <br />
      <label>
        Email:
        <input type="email" ref={emailRef} />
      </label>
      <br />
      <button type="submit">Submit</button>
    </form>
  );
}

```

### **Key Points**:

- Input values are managed by the DOM, not React state.
- Use `useRef` to access values when needed.

---

### **3. Form Validation**

Validation ensures that the form data meets specified requirements before submission.

### **Example: Validation with Controlled Components**

```jsx
import { useState } from 'react';

function FormWithValidation() {
  const [email, setEmail] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!email.includes('@')) {
      setError('Please enter a valid email address.');
      return;
    }
    console.log(`Submitted email: ${email}`);
    setError('');
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Email:
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
      </label>
      {error && <p style={{ color: 'red' }}>{error}</p>}
      <br />
      <button type="submit">Submit</button>
    </form>
  );
}

```

---

### **4. Handling Multiple Inputs**

When handling multiple inputs, you can use a single state object.

### **Example: Dynamic Form Handling**

```jsx
import { useState } from 'react';

function MultiInputForm() {
  const [formData, setFormData] = useState({ name: '', email: '' });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData((prevData) => ({
      ...prevData,
      [name]: value,
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input
          type="text"
          name="name"
          value={formData.name}
          onChange={handleChange}
        />
      </label>
      <br />
      <label>
        Email:
        <input
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
      </label>
      <br />
      <button type="submit">Submit</button>
    </form>
  );
}

```

### **Key Points**:

- Use the `name` attribute of the input element to identify the field.
- Update state dynamically based on the `name` property.

---

### **React Routing**

React Router is a standard library for managing navigation and routing in a React application. It allows you to define routes, render components based on the URL, and navigate between views.

---

### **1. Installation**

To use React Router, you need to install the package:

```bash
npm install react-router-dom

```

---

### **2. Basic Concepts**

### **a. Router Components**

- **BrowserRouter**: Uses the HTML5 history API for clean URLs (recommended for web apps).
- **HashRouter**: Uses the hash part of the URL (`#`) for routing (useful for older browsers or static file hosting).

### **b. Route**

Defines a path and the component to render for that path.

### **c. Link & NavLink**

- **Link**: Used for client-side navigation without a page reload.
- **NavLink**: Similar to `Link` but adds styling or classes to indicate the active link.

### **d. Outlet**

Used in nested routing to render child routes.

### **e. useNavigate**

A hook to programmatically navigate between routes.

---

### **3. Setting Up Routes**

### **Example: Basic Routing**

```jsx
import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';

function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Page</h2>;
}

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}

export default App;

```

---

### **4. Nested Routes**

You can create routes inside other routes for hierarchical navigation.

```jsx
import { BrowserRouter as Router, Routes, Route, Link, Outlet } from 'react-router-dom';

function Dashboard() {
  return (
    <div>
      <h2>Dashboard</h2>
      <nav>
        <Link to="profile">Profile</Link> | <Link to="settings">Settings</Link>
      </nav>
      <Outlet />
    </div>
  );
}

function Profile() {
  return <h3>Profile Page</h3>;
}

function Settings() {
  return <h3>Settings Page</h3>;
}

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Dashboard />}>
          <Route path="profile" element={<Profile />} />
          <Route path="settings" element={<Settings />} />
        </Route>
      </Routes>
    </Router>
  );
}

export default App;

```

---

### **5. Dynamic Routes**

Dynamic routes are used for paths that include parameters.

```jsx
import { BrowserRouter as Router, Routes, Route, useParams } from 'react-router-dom';

function UserProfile() {
  const { userId } = useParams();
  return <h2>User Profile for ID: {userId}</h2>;
}

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/user/:userId" element={<UserProfile />} />
      </Routes>
    </Router>
  );
}

export default App;

```

---

### **6. Programmatic Navigation**

The `useNavigate` hook allows you to navigate programmatically.

```jsx
import { useNavigate } from 'react-router-dom';

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // Perform login logic
    navigate('/dashboard');
  };

  return <button onClick={handleLogin}>Login</button>;
}

```

---

### **7. Redirects**

Redirect users from one route to another.

```jsx
import { Navigate } from 'react-router-dom';

function App() {
  const isLoggedIn = false;

  return (
    <Routes>
      <Route path="/" element={<h2>Home Page</h2>} />
      <Route
        path="/dashboard"
        element={isLoggedIn ? <h2>Dashboard</h2> : <Navigate to="/" />}
      />
    </Routes>
  );
}

```

---

### **8. Protected Routes**

Guard routes to prevent unauthorized access.

```jsx
import { Navigate } from 'react-router-dom';

function ProtectedRoute({ children, isAuthenticated }) {
  return isAuthenticated ? children : <Navigate to="/login" />;
}

function App() {
  const isAuthenticated = false;

  return (
    <Routes>
      <Route path="/" element={<h2>Home Page</h2>} />
      <Route
        path="/dashboard"
        element={
          <ProtectedRoute isAuthenticated={isAuthenticated}>
            <h2>Dashboard</h2>
          </ProtectedRoute>
        }
      />
    </Routes>
  );
}

```

---

### **Unit: React with HTTP**

### **Using Axios with React**

Axios is a popular promise-based HTTP client for making API requests. It is often used in React applications to fetch data from or send data to a server. Here¿s a detailed guide on integrating and using Axios with React.

---

### **1. Installation**

To use Axios in your React project, install it via npm:

```bash
npm install axios

```

---

### **2. Basic Usage**

### **Making GET Requests**

```jsx
import React, { useEffect, useState } from 'react';
import axios from 'axios';

function App() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    axios
      .get('https://jsonplaceholder.typicode.com/posts')
      .then((response) => {
        setData(response.data);
        setLoading(false);
      })
      .catch((error) => console.error('Error fetching data:', error));
  }, []);

  return (
    <div>
      {loading ? (
        <p>Loading...</p>
      ) : (
        data.map((post) => <p key={post.id}>{post.title}</p>)
      )}
    </div>
  );
}

export default App;

```

---

### **Making POST Requests**

```jsx
import React, { useState } from 'react';
import axios from 'axios';

function App() {
  const [title, setTitle] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    axios
      .post('https://jsonplaceholder.typicode.com/posts', {
        title,
        body: 'This is a sample body.',
        userId: 1,
      })
      .then((response) => console.log('Data posted:', response.data))
      .catch((error) => console.error('Error posting data:', error));
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Title:
        <input
          type="text"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
        />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

export default App;

```

---

### **3. Setting Up Axios Defaults**

You can set up default configurations to avoid repetition.

### **Example: Configuring Axios Defaults**

```jsx
import axios from 'axios';

axios.defaults.baseURL = 'https://jsonplaceholder.typicode.com';
axios.defaults.headers.common['Authorization'] = 'Bearer your-token';

axios.get('/posts').then((response) => console.log(response.data));

```

---

### **4. Using Axios Interceptors**

Interceptors allow you to modify requests or responses globally before they are handled.

### **Request Interceptor Example**

```jsx
axios.interceptors.request.use(
  (config) => {
    config.headers.Authorization = 'Bearer your-token';
    console.log('Request Interceptor:', config);
    return config;
  },
  (error) => Promise.reject(error)
);

```

### **Response Interceptor Example**

```jsx
axios.interceptors.response.use(
  (response) => {
    console.log('Response Interceptor:', response);
    return response;
  },
  (error) => {
    console.error('Error Interceptor:', error);
    return Promise.reject(error);
  }
);

```

---

### **5. Canceling Requests**

You can cancel an Axios request using `AbortController`.

```jsx
import React, { useEffect } from 'react';
import axios from 'axios';

function App() {
  useEffect(() => {
    const controller = new AbortController();

    axios
      .get('https://jsonplaceholder.typicode.com/posts', {
        signal: controller.signal,
      })
      .then((response) => console.log(response.data))
      .catch((error) => {
        if (axios.isCancel(error)) {
          console.log('Request canceled:', error.message);
        } else {
          console.error('Error:', error);
        }
      });

    return () => controller.abort();
  }, []);

  return <div>Check the console for output.</div>;
}

export default App;

```

---

### **6. Error Handling**

Use `try...catch` or `.catch()` for handling errors in requests.

```jsx
axios
  .get('https://jsonplaceholder.typicode.com/posts')
  .then((response) => console.log(response.data))
  .catch((error) => {
    if (error.response) {
      console.error('Error Response:', error.response.data);
    } else if (error.request) {
      console.error('Error Request:', error.request);
    } else {
      console.error('General Error:', error.message);
    }
  });

```

---

### **7. Combining with React Hooks**

Using `useEffect` and `useState` with Axios is common. You can also create custom hooks.

### **Example: Custom Hook for Fetching Data**

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function useAxios(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    axios
      .get(url)
      .then((response) => {
        setData(response.data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err);
        setLoading(false);
      });
  }, [url]);

  return { data, loading, error };
}

export default useAxios;

```

### **Usage in a Component**

```jsx
import useAxios from './useAxios';

function App() {
  const { data, loading, error } = useAxios(
    'https://jsonplaceholder.typicode.com/posts'
  );

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return data.map((post) => <p key={post.id}>{post.title}</p>);
}

export default App;

```

---

### **8. Handling Concurrent Requests**

Use `axios.all()` or `Promise.all()` for multiple requests.

```jsx
axios
  .all([
    axios.get('https://jsonplaceholder.typicode.com/posts'),
    axios.get('https://jsonplaceholder.typicode.com/comments'),
  ])
  .then(
    axios.spread((postsResponse, commentsResponse) => {
      console.log('Posts:', postsResponse.data);
      console.log('Comments:', commentsResponse.data);
    })
  );

```

---

### **9. Axios vs Fetch**

| Feature | Axios | Fetch |
| --- | --- | --- |
| Response Parsing | Automatically parses JSON | Requires manual parsing |
| Request Cancellation | Built-in with AbortController support | Requires AbortController |
| Interceptors | Built-in | Not supported |
| Error Handling | Provides rich error objects | Basic error handling |

---

### **Unit: React Testing**

### **Testing React Components with Jest and React Testing Library (RTL)**

React Testing Library (RTL) and Jest are commonly used together for testing React applications. RTL focuses on testing components from the user's perspective, while Jest provides the testing framework and mocking capabilities.

---

### **1. Setting Up Jest and RTL**

### **Installation**

```bash
npm install --save-dev jest @testing-library/react @testing-library/jest-dom @testing-library/user-event @testing-library/dom

```

Add Jest configuration in `package.json` or a `jest.config.js` file if needed. For CRA (Create React App), Jest is pre-configured.

### **Optional Setup File for Jest DOM**

Create a `setupTests.js` file in your project:

```
import '@testing-library/jest-dom';

```

---

### **2. Writing Basic Tests**

### **Example: Testing a Simple Component**

```jsx
// Counter.tsx
import React, { useState } from 'react';

function Counter(): JSX.Element {
  const [count, setCount] = useState<number>(0);

  return (
    <div>
      <p data-testid="count">Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;

```

### **Test File**

```jsx
// Counter.test.tsx
import React from 'react';
import { render } from '@testing-library/react';
import { screen, fireEvent } from '@testing-library/dom'
import Counter from './Counter';

test('renders counter and increments count', () => {
  render(<Counter />);

  const countElement = screen.getByTestId('count');
  expect(countElement).toHaveTextContent('Count: 0');

  const button = screen.getByText(/increment/i);
  fireEvent.click(button);

  expect(countElement).toHaveTextContent('Count: 1');
});

```

---

### **3. Mocking in Jest**

Mocking is used to replace real implementations of modules or functions with mocked versions.

```tsx
// api.ts
export const fetchData = async (): Promise<{ message: string }> => {
  const response = await fetch('https://api.example.com/data');
  return response.json();
};

```

```tsx
// Component.tsx
import React, { useEffect, useState } from 'react';
import { fetchData } from './api';

function Component(): JSX.Element {
  const [data, setData] = useState<{ message: string } | null>(null);

  useEffect(() => {
    fetchData().then((result) => setData(result));
  }, []);

  return <div>{data ? data.message : 'Loading...'}</div>;
}

export default Component;

```

```jsx
// Component.test.tsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import Component from './Component';
import * as api from './api';

jest.mock('./api');

test('renders data fetched from API', async () => {
  (api.fetchData as jest.Mock).mockResolvedValue({ message: 'Hello, World!' });

  render(<Component />);

  expect(screen.getByText(/loading/i)).toBeInTheDocument();

  const resolvedMessage = await screen.findByText(/hello, world/i);
  expect(resolvedMessage).toBeInTheDocument();
});

```

---

### **4. Testing User Interactions**

RTL provides utilities to simulate user interactions.

### **Example: Testing Form Input**

```jsx
// Login.tsx
import React, { useState } from 'react';

interface LoginProps {
  onSubmit: (username: string) => void;
}

function Login({ onSubmit }: LoginProps): JSX.Element {
  const [username, setUsername] = useState<string>('');

  const handleSubmit = () => onSubmit(username);

  return (
    <div>
      <input
        type="text"
        placeholder="Enter username"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
      />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}

export default Login;

```

```tsx
// Login.test.tsx
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import Login from './Login';

test('handles user input and form submission', () => {
  const mockSubmit = jest.fn();
  render(<Login onSubmit={mockSubmit} />);

  const input = screen.getByPlaceholderText(/enter username/i);
  fireEvent.change(input, { target: { value: 'John Doe' } });

  const button = screen.getByText(/submit/i);
  fireEvent.click(button);

  expect(mockSubmit).toHaveBeenCalledWith('John Doe');
});

```

---

### **5. Testing Async Code**

RTL provides `findBy` and `waitFor` for asynchronous assertions.

### **Example: Testing Loading States**

```jsx
// AsyncComponent.tsx
import React, { useEffect, useState } from 'react';

function AsyncComponent(): JSX.Element {
  const [data, setData] = useState<string | null>(null);

  useEffect(() => {
    const timer = setTimeout(() => setData('Hello, Async!'), 1000);
    return () => clearTimeout(timer);
  }, []);

  return <div>{data || 'Loading...'}</div>;
}

export default AsyncComponent;

```

```tsx
// AsyncComponent.test.tsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import AsyncComponent from './AsyncComponent';

test('displays loading initially and renders data after async operation', async () => {
  render(<AsyncComponent />);

  expect(screen.getByText(/loading/i)).toBeInTheDocument();

  const resolvedText = await screen.findByText(/hello, async/i);
  expect(resolvedText).toBeInTheDocument();
});

```

---

### **Best Practices**

1. **Focus on Behavior**: Test user interaction and visible output, not implementation details.
2. **Avoid Snapshot Testing**: Unless you are testing static content.
3. **Mock External Dependencies**: Avoid real API calls in tests.
4. **Write Modular Tests**: Test individual components, not entire apps in one go.
