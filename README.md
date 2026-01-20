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

 -- User Service Key Concepts:
  (Stores both internal user ID and keycloakId & Supports validation via either internal ID or Keycloak sub)

- **Activity Service**
  - MongoDB database
  - Manages fitness activities

- **AI Service**
  - MongoDB database
  - Uses Gemini API for personalized activity recommendations
 
