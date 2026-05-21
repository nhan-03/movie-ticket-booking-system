# Project Structure

## Overview

The project uses a feature-based package structure to improve maintainability, scalability, and separation of concerns.

```txt
movie-ticket-booking/
├── backend/
├── frontend/
├── docs/
├── docker-compose.yml
└── README.md
```

---

# Backend Structure

```txt
backend/
└── src/
    └── main/
        ├── java/
        │   └── com/
        │       └── nhan/
        │           └── moviebooking/
        │               ├── common/
        │               ├── config/
        │               ├── security/
        │               ├── exception/
        │               ├── auth/
        │               ├── user/
        │               ├── movie/
        │               ├── cinema/
        │               ├── showtime/
        │               ├── booking/
        │               └── payment/
        │
        └── resources/
            ├── application.yml
            ├── application-dev.yml
            ├── application-prod.yml
            └── db/
                └── migration/
```

---

# Common Package

Contains reusable shared components used across the application.

```txt
common/
├── base/
├── constants/
└── response/
```

---

## base/

Contains shared base classes.

Example:

```txt
BaseEntity
```

Responsibilities:
- Common entity fields
- Audit fields
- Shared entity behavior

---

## constants/

Contains shared constants.

Example:

```txt
SecurityConstants
PaginationConstants
```

Responsibilities:
- Security constants
- Pagination constants
- Shared application constants

---

## response/

Contains common API response models.

Example:

```txt
ApiResponse<T>
```

Responsibilities:
- Standard API response format
- Success response wrapper
- Error response wrapper

---

# Config Package

Contains Spring Boot configuration classes.

```txt
config/
├── OpenApiConfig.java
└── RabbitMQConfig.java
```

---

## OpenApiConfig

Responsibilities:
- Swagger/OpenAPI configuration
- API documentation setup

---

## RabbitMQConfig

Responsibilities:
- Queue configuration
- Exchange configuration
- Binding configuration

---

# Security Package

Handles authentication and authorization.

```txt
security/
├── JwtAuthenticationFilter.java
├── JwtService.java
├── CustomUserDetailsService.java
└── SecurityConfig.java
```

---

## JwtAuthenticationFilter

Responsibilities:
- Intercept incoming requests
- Extract JWT token
- Authenticate users

---

## JwtService

Responsibilities:
- Generate JWT tokens
- Validate JWT tokens
- Extract user information from tokens

---

## CustomUserDetailsService

Responsibilities:
- Load user information
- Integrate with Spring Security

---

## SecurityConfig

Responsibilities:
- Configure Spring Security
- Configure authentication rules
- Configure authorization rules
- Configure stateless JWT authentication

---

# Exception Package

Handles global exception processing.

```txt
exception/
├── GlobalExceptionHandler.java
├── BusinessException.java
└── ErrorCode.java
```

---

## GlobalExceptionHandler

Responsibilities:
- Handle application exceptions
- Return standardized error responses

---

## BusinessException

Responsibilities:
- Represent business logic exceptions
- Store error codes and messages

---

## ErrorCode

Responsibilities:
- Store application error codes
- Define standardized error messages

---

# Auth Module

Handles authentication features.

```txt
auth/
├── controller/
├── service/
├── dto/
│   ├── request/
│   └── response/
└── mapper/
```

---

## Responsibilities

- Register
- Login
- Refresh token
- Logout

---

# Feature Module Structure

Each feature module contains its own layers.

Example:

```txt
movie/
├── controller/
├── service/
├── repository/
├── entity/
├── dto/
│   ├── request/
│   └── response/
├── mapper/
└── specification/
```

---

# Controller Layer

Responsibilities:
- Receive HTTP requests
- Validate request data
- Return API responses

---

# Service Layer

Responsibilities:
- Process business logic
- Handle transactions
- Coordinate repositories

---

# Repository Layer

Responsibilities:
- Database access
- CRUD operations
- Pagination and filtering

---

# Entity Layer

Responsibilities:
- Database mapping
- Entity relationships

---

# DTO Layer

```txt
dto/
├── request/
└── response/
```

Responsibilities:
- Request validation
- Response formatting
- Prevent exposing entities directly

---

# Mapper Layer

Responsibilities:
- Convert entities to DTOs
- Convert DTOs to entities

---

# Specification Layer

Responsibilities:
- Dynamic filtering
- Search conditions
- Query building

---

# Resources Structure

```txt
resources/
├── application.yml
├── application-dev.yml
└── db/
    └── migration/
```

---

# Application Configuration

## application.yml

Contains shared application configuration.

Example:

```yaml
server:
  port: 8080
```

---

## application-dev.yml

Contains development environment configuration.

Example:

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/movie_booking
```

---

# Database Migration

Uses Flyway for database version control.

Migration files are stored in:

```txt
db/migration/
```

Example:

```txt
V1__create_users_table.sql
V2__create_movies_table.sql
V3__create_bookings_table.sql
```

---

# Naming Conventions

| Type | Example |
|---|---|
| Controller | MovieController |
| Service | MovieService |
| Repository | MovieRepository |
| Entity | Movie |
| Request DTO | CreateMovieRequest |
| Response DTO | MovieDetailResponse |
| Mapper | MovieMapper |

---

# API Naming Convention

| Method | Endpoint |
|---|---|
| GET | /api/movies |
| GET | /api/movies/{id} |
| POST | /api/admin/movies |
| PATCH | /api/admin/movies/{id} |

---

# Architectural Principles

- Feature-based package structure
- Layered architecture
- Separation of concerns
- DTO-based API design
- Stateless JWT authentication
- RESTful API design
- Flyway database migration
- Modular monolith architecture