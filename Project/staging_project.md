# Staging Project

This staging project is aimed to be relatively straightforward. Instead of focusing on something complex to build out as a web app, we are focusing on building our conceptual understanding of the technologies we are working with.

As you work with each of the technologies, focus on the "why?". Why are you using these technologies? Why are these technologies built this way? Understand the context and history that these technologies were built within to aid in your conceptual understanding. None of these technologies exist within a vacuum. You can learn all the syntax you want, and you can get a lot of practical understanding of them, but this will limit you if that is all you do. You must understand the bigger picture of why these technologies exist and what they are trying to do not just what they do.

## Requirements:

- Login and registration
- Task Manager (Create, Read, Update, and Delete tasks)
    - Tasks Model
        - ID
        - Created User ID
        - Task Type
        - Task Description ()
        - Creation Date
        - Due Date
        - Status
- Persist the data through PostgreSQL and an RDS
- Dockerize the backend and deploy to an EC2 instance using Jenkins
- Host the frontend on S3

---

## Technologies:
### Frontend
- React
- TypeScript
- S3

### Backend
- Java
- PostgreSQL
- Spring Boot
- Spring MVC
- Spring Data
- EC2
- RDS

### Testing
- JUnit
- Mockito
- Postman

### DevOps
- Docker
- Jenkins

## **Conceptual Focus Areas**  
1. **React**: Virtual DOM, component lifecycle, unidirectional data flow.  
2. **Spring Boot**: Dependency injection, inversion of control (IoC).  
3. **Docker**: Containerization vs. virtualization.  
4. **AWS**: Hosting and Connecting different cloud services.
5. **Testing**: Unit testing and mocking dependencies vs. integration testing.  

---

### **Week 1: Foundation & Core Implementation**
#### **Frontend (React + TypeScript + S3)**
1. **Component Architecture**:  
   - Create a React app with TypeScript enforcing strict typing.  
   - Implement 3 interconnected components demonstrating:  
     - Props drilling vs. Context API  
     - Component lifecycle methods (e.g., `useEffect` for data fetching)  
   - **Requirement**: Explain in documentation why React's virtual DOM improves performance.

2. **TypeScript**:  
   - Define custom types/interfaces for all API response/request structures.  

3. **S3 Basics**:  
   - Host static assets (images, fonts) in S3.  

#### **Backend (Java + Spring Boot + PostgreSQL)**
1. **Spring Boot Setup**:  
   - Initialize a Spring Boot project with Spring Data JPA and Spring MVC.  
   - Configure PostgreSQL connection in `application.properties`.  

2. **JPA Entity Design**:  
   - Create 2 JPA entities with relationships (e.g., `@OneToMany`, `@ManyToOne`).  
   - **Requirement**: Explain lazy vs. eager loading in your entity relationships.

3. **Basic API Endpoints**:  
   - Implement CRUD endpoints using Spring Data repositories.  
   - Validate request bodies using `@Valid` and custom exception handling.

#### **DevOps (Docker + Jenkins)**  
1. **Containerization**:  
   - Dockerize the backend applications.   
   - **Requirement**: Explain the difference between `COPY` and `ADD` in Dockerfiles.  

---

### **Week 2: Advanced Features & Integration**
#### **Frontend**  
1. **State Management**:  
   - Implement global state using React Context. 

2. **API Integration**:  
   - Fetch/patch data from Spring Boot API using Axios.  
   - Handle loading/error states with TypeScript.

3. **S3 Deployment Prep**:  
   - Configure React build for S3 static hosting.  

#### **Backend**  
1. **Service Layer**:  
   - Create a service class with business logic (e.g., validation rules).  

2. **Testing (JUnit + Mockito)**:  
   - Write unit tests for a service class mocking the repository layer.  
   - Achieve 80% line coverage.  
   - **Requirement**: Explain the purpose of `@Mock` vs. `@InjectMocks`.  

3. **Advanced API**:  
   - Add pagination/sorting to an endpoint using Spring Data `Pageable`.  
   - Secure one endpoint with Spring Security (basic auth).  

#### **DevOps**  
1. **Jenkins Pipeline**:  
   - Create a Jenkinsfile to automate:  
     - Building Docker images  
     - Running tests  
   - **Requirement**: Explain the role of Jenkins agents/executors.  

---

### **Week 3: Testing, Deployment & Reflection**
#### **Final Integration**  
1. **End-to-End Testing**:  
   - Frontend: Write Jest tests for component interactions.  
   - Backend: Integration tests and API tests with Postman.  

2. **Deployment**:  
   - Backend: Deploy Spring Boot app to EC2 using Docker.  
   - Frontend: Deploy React app to S3.  

3. **Observability**:  
   - Add Spring Boot Actuator for health checks.  
   - Log API requests to a file using SLF4J.  

#### **Documentation & Presentation**  
- Write a technical doc explaining:  
   - How Spring MVC handles HTTP requests/responses.  
   - Why Docker is used for environment consistency.  
   - Tradeoffs between S3 static hosting and server-side rendering.  