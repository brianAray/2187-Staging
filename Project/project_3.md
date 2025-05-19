# Project 3 - Deployment Basics  
This project focuses on deploying the backend and frontend using Docker and AWS, emphasizing environment consistency and cloud services.  

## Technologies  
- Docker  
- AWS EC2 (Backend)  
- AWS S3 (Frontend)  
- PostgreSQL (AWS RDS)  

## Requirements  

### 1. Core Features  
- Dockerize the backend and frontend apps:  
  - Use multi-stage builds to optimize image size.  
- Deploy the backend to EC2 and frontend to S3.  
- Migrate the PostgreSQL database from local to AWS RDS.  

### 2. Conceptual Focus  
- Explain why S3 is used for static assets instead of serving them from the backend.  
- Explain why we containerize our applications for deployment


## Key Concepts  

#### 1. Docker  
- Containerization:  
  - Isolate apps with dependencies using `Dockerfile` and `docker-compose.yml`.  
  - Example backend Dockerfile:  
    ```dockerfile
    FROM openjdk:17-jdk-slim AS build
    COPY . /app
    WORKDIR /app
    RUN ./mvnw package -DskipTests

    FROM openjdk:17-jdk-slim
    COPY --from=build /app/target/*.jar /app.jar
    ENTRYPOINT ["java", "-jar", "/app.jar"]
    ```  

- Multi-Stage Builds:  
  - Reduce image size by separating build and runtime environments.  

#### 2. AWS  
- EC2:  
  - Deploy Dockerized backend as a cloud VM.  
  - Use security groups to allow HTTP/HTTPS traffic.  

- S3:  
  - Host static React build files with bucket policies for public read access.  
  - Enable static website hosting in S3 settings.  

- RDS:  
  - Configure a managed PostgreSQL instance.  
  - Update `application.properties` to use RDS endpoint:  
    ```properties
    spring.datasource.url=jdbc:postgresql://<RDS_ENDPOINT>:5432/mydb
    ```  

#### 3. Environment Configurations  
- Local vs. Production:  
  - Use environment variables (e.g., `DATABASE_URL`) to switch configurations.  
  - Spring Boot profiles (`application-prod.properties`).  
