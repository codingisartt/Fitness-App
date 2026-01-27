## Fitness App – Microservice Architecture

This project is a microservice-based fitness application designed with real-world backend practices in mind. It demonstrates authentication & authorization, service discovery, centralized configuration, asynchronous communication, and AI-powered recommendations.
The system is built to be scalable, modular, and cloud-ready, following common enterprise architecture patterns.

### Tech Stack Overview

Backend
- Java 17
- Spring Boot
- Spring Cloud (Gateway, Eureka, Config Server)
- Spring Security
- Spring Data JPA & MongoDB & PostgreSQL

## Database Strategy

- **PostgreSQL** is used in User Service due to strong consistency and relational user data.
- **MongoDB** is used in Activity and AI services for flexible schemas and fast iteration on activity and recommendation data.
  
### Core Infrastructure Components
- **Config Server** – Centralized configuration management for all services.
- **Eureka Server** – Enables dynamic service registration and discovery.
- **API Gateway** – Acts as the single entry point to the system. Handles routing, authentication, and security concerns.
- **Keycloak** – Manages user authentication and authorization. Issues JWT tokens used across services. (Dockerized)
- **RabbitMQ** – Provides asynchronous communication between services. (Dockerized)

### AI Integration

- Gemini API – Activity recommendations

### Build & Dependency Management

- Maven Multi-Module Project with Parent POM

### Authentication & Authorization Flow

- User authenticates via Keycloak
- Keycloak issues a JWT token
- Requests pass through API Gateway
- Gateway validates the token and forwards requests
- Services extract claims (sub, email, roles) from JWT
- A custom Keycloak User Sync Filter ensures that Keycloak users are synchronized with the internal User Service database.

### Services
- **User Service**   
  - PostgreSQL database
  - Stores internal user data
  - Synchronizes users from Keycloak

 **User Service Key Concepts**
- Stores both internal user ID and Keycloak ID
- Supports validation via either internal ID or Keycloak `sub`

- **Activity Service**
  - MongoDB database
  - Manages fitness activities

- **AI Service**
  - MongoDB database
  - Uses Gemini API for personalized activity recommendations

###  Frontend
- React
- Vite
- Material UI (MUI)
- Axios

### Login Page  
Live Demo (Local): http://localhost:5173
<img width="888" height="520" alt="image" src="https://github.com/user-attachments/assets/64416052-8d18-43fa-8e3d-2f6741478638" />

 ### User Authentication Page
 <img width="605" height="356" alt="image" src="https://github.com/user-attachments/assets/86e3cb42-55c5-4930-b36e-4c4332dbff17" />

 ### Eureka
 <img width="605" height="280" alt="image" src="https://github.com/user-attachments/assets/968f44c9-8792-49c4-bba0-dbb71e2babc9" />

 ### Gateway with Keycloak Token
 <img width="605" height="482" alt="image" src="https://github.com/user-attachments/assets/69d4e450-4cae-496f-875f-998669f69058" />
<img width="605" height="355" alt="image" src="https://github.com/user-attachments/assets/429364da-6808-4d06-8106-68584020c449" />

### Activites Page
<img width="605" height="428" alt="image" src="https://github.com/user-attachments/assets/ff897b45-8edd-4aa8-9f00-9def30353d1e" />

### Activity Details with Gemini API Recommendations
<img width="605" height="608" alt="image" src="https://github.com/user-attachments/assets/1a6bf4fb-b90c-4d38-9952-d9071fcb270e" />
<img width="1057" height="961" alt="image" src="https://github.com/user-attachments/assets/c8c1c4b8-6724-4366-93f6-10385f54bda3" />

### Default Recommendations
<img width="605" height="505" alt="image" src="https://github.com/user-attachments/assets/e4349261-dff3-4f94-9729-4415f02efa5c" />
When the AI service is unavailable or returns an invalid response, the backend applies a fallback mechanism to generate safe default recommendations. This ensures uninterrupted user experience and system resilience.

### RabbitMQ – Queues for Asynchronous Communication
<img width="1632" height="965" alt="image" src="https://github.com/user-attachments/assets/73f37a97-2554-475e-a666-fd3960d0471f" />
<img width="1208" height="658" alt="image" src="https://github.com/user-attachments/assets/b16fd1cd-2c3a-4684-9eef-c381738df371" />
<img width="605" height="290" alt="image" src="https://github.com/user-attachments/assets/75ea5237-fd1f-4440-a7de-972c0eb1d74e" />

### Keycloak – User Management
<img width="1640" height="667" alt="image" src="https://github.com/user-attachments/assets/795c38fb-150a-47c1-a184-499611948285" />

### PostgreSQL – User Service Database
<img width="1307" height="565" alt="image" src="https://github.com/user-attachments/assets/dbbab3a6-7c2b-4c7c-8900-961fe388e584" />

### MongoDB – AI Service Database
<img width="1301" height="927" alt="image" src="https://github.com/user-attachments/assets/f0f3193d-2f9f-4c26-854d-2768935d84de" />




