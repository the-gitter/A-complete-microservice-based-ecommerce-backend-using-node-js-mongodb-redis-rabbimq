# E-commerce Backend Microservices

This project is a full-scale, production-ready e-commerce backend built using a microservice architecture. It is designed to manage an online store for selling audio systems and event management equipment.

## Table of Contents

- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Microservices](#microservices)
  - [User Service](#user-service)
  - [Catalog Service](#catalog-service)
  - [Order Service](#order-service)
  - [Payment Service](#payment-service)
  - [Inventory Service](#inventory-service)
  - [Notification Service](#notification-service)
- [Message Broker](#message-broker)
- [Setup and Installation](#setup-and-installation)
- [API Documentation](#api-documentation)
- [CI/CD Pipeline](#cicd-pipeline)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Architecture

The system is designed as a microservice architecture, with each service handling a specific business domain. Services communicate asynchronously using RabbitMQ.

![Architecture Diagram](./assets/db-schema.png)

## Tech Stack

- **Node.js**
- **TypeScript**
- **Mongodb** a Nosql db for storing data
- **RabbitMQ** for asynchronous messaging
- **Redis** for caching and session management
- **Firebase Admin** for user authentication
- **JWT** for token-based authentication
- **Cloudinary** for image storage and management
- **Docker** for containerization
- **CI/CD** using GitHub Actions
- **Postman** for API testing and documentation

## Microservices

### User Service

Handles user authentication, registration, and profile management.

**Features:**
- User registration and login
- Profile management
- Role-based access control 

### Catalog Service

Manages products, categories, and stock levels.

**Features:**
- Product and category management
- Stock updates
- Product reviews
 

### Order Service

Handles order creation, item management, and status updates.

**Features:**
- Order management
- Order status tracking
 

### Payment Service

Processes payments and manages transactions.

**Features:**
- Payment processing
- Transaction management
- Refund handling
 

### Inventory Service

Manages and syncs stock levels.

**Features:**
- Inventory management
- Stock adjustments
 
### Notification Service

Sends email and SMS notifications.

**Features:**
- Email notifications
- SMS notifications
- Notification templates management
 
## Message Broker

RabbitMQ is used to facilitate asynchronous communication between microservices. It handles various events such as user registration, order creation, and payment processing.
 