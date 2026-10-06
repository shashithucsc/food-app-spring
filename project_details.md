# Food Delivery Platform - Microservices Architecture

## Project Goal
A highly scalable, multi-vendor food delivery web application designed to demonstrate industry-standard distributed system patterns. The platform separates core business domains into independent microservices, utilizing the Database-per-Service pattern, centralized routing, and secure identity management.

## Core Features
* **Guest & Customer Portal:** Browse and search food items (read-heavy, powered by MongoDB).
* **Account Management:** Secure user registration and authentication via Keycloak.
* **Supplier Dashboard:** Inventory management for individual sellers to track and update stock.
* **Admin Controls:** Cross-platform user management and global sales monitoring.
* **Resilient Routing:** Centralized API Gateway handling all incoming traffic and dynamic service discovery.

## Technology Stack
* **Frontend:** Next.js (React)
* **Backend:** Java 17, Spring Boot 3.2.x, Spring Cloud (Gateway, Netflix Eureka)
* **Databases:** PostgreSQL (Relational/Transactions), MongoDB (NoSQL/Document Search)
* **Security:** Keycloak (Identity and Access Management)
* **Infrastructure:** Docker & Docker Compose

## Complete Monorepo Structure

```text
food-delivery-platform/
├── infrastructure/               # DevOps and Infrastructure
│   ├── docker-compose.yml        # Multi-container orchestration
│   └── init.sql                  # PostgreSQL database bootstrapping
│
├── discovery-server/             # Spring Boot: Netflix Eureka Registry
│   └── (Port: 8761)              # Dynamic service phonebook
│
├── api-gateway/                  # Spring Boot: Spring Cloud Gateway
│   └── (Port: 8081)              # Single entry point & route resolution
│
├── services/                     # Business Domain Microservices
│   ├── catalog-service/          # Spring Boot: Food & Category search
│   │   └── (Database: MongoDB)   # High-speed document reads
│   │
│   ├── user-service/             # Spring Boot: User profiles & roles
│   │   └── (Database: PostgreSQL)# Relational user data
│   │
│   ├── inventory-service/        # Spring Boot: Supplier stock management
│   │   └── (Database: PostgreSQL)# ACID-compliant inventory tracking
│   │
│   └── order-service/            # Spring Boot: Cart, checkout & history
│       └── (Database: PostgreSQL)# Transactional order processing
│
├── frontend/                     # Next.js Application (Client UI)
│
└── README.md                     # Architecture documentation & diagrams