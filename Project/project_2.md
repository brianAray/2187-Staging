# Project 2 - Frontend-Backend Integration

This project focuses on building a React frontend that connects to the Spring Boot backend, emphasizing API integration, state management, and TypeScript.

## Technologies
- React
- TypeScript
- Axios
- Spring Boot (Backend from Project 1)

## Requirements

1. Core Features
    - Build a UI to perform CRUD operations on the entity (e.g., Book).
    - Display a list of items fetched from the backend.
    - Add forms to create/edit items with validation (e.g., prevent empty fields).
    - Use Axios to interact with the backend API (GET, POST, PUT, DELETE).
    - Define TypeScript interfaces for API request/response payloads.

2. Conceptual Focus
    - Explain how state is managed in React in a component, and globally using state management tools
    - Explain how React’s component lifecycle (e.g., useEffect) manages data fetching.

### Key Concepts  

#### 1. React  
- Virtual DOM:  
  - Efficiently updates the UI by comparing virtual DOM snapshots.  
  - Explain how re-renders work after API calls (e.g., updating state triggers UI changes).  

- Component Lifecycle:  
  - Use `useEffect` to fetch data on component mount:  
    ```typescript
    useEffect(() => {
      axios.get<Book[]>("/api/books").then((res) => setBooks(res.data));
    }, []);
    ```  
  - Cleanup functions for avoiding memory leaks.  

- State Management:  
  - Use `useState` for local component state.  
  - Use Context API or Redux Toolkit for global state (e.g., shared user session).  

#### 2. TypeScript  
- Static Typing:  
  - Define interfaces for API data:  
    ```typescript
    interface Book {
      id: number;
      title: string;
      author: string;
    }
    ```  
  - Use generics in Axios requests:  
    ```typescript
    axios.get<Book[]>("/api/books");
    ```  

- Type Safety:  
  - Catch errors at compile time (e.g., mismatched data types in API responses).  

#### 3. Axios & API Integration  
- HTTP Client:  
  - Configure base URLs and headers:  
    ```typescript
    axios.create({ baseURL: "http://localhost:8080" });
    ```  
  - Handle errors using `try/catch` or `.catch()`.  

- CORS:  
  - Explain the `@CrossOrigin` annotation in the Spring Boot controller.  
