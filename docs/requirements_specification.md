# Software Requirements Specification (SRS)

## Table of Contents

- [1. Introduction](#1-introduction)
- [2. User Roles](#2-user-roles)
- [3. Functional Requirements](#3-functional-requirements)
    - [3.1 Authentication](#31-authentication)
    - [3.2 User profile](#32-user-profile)
    - [3.3 Movie](#33-movie)
    - [3.4 Cinema](#34-cinema)
    - [3.5 Showtime](#35-showtime)
    - [3.6 Booking](#36-booking)
    - [3.7 Payment](#37-payment)
    - [3.8 Administration](#38-administration)
        - [3.8.1 Movie management](#381-movie-management)
        - [3.8.2 Movie genre management](#382-movie-genre-management)
        - [3.8.3 Cinema management](#383-cinema-management)
        - [3.8.4 Screening room management](#384-screening-room-management)
        - [3.8.5 Showtime management](#385-showtime-management)
        - [3.8.6 User management](#386-user-management)
        - [3.8.7 Statistics](#387-statistics)
        - [3.8.8 Pricing management](#388-pricing-management)
- [4. Non-functional Requirements](#4-non-functional-requirements)

## 1. Introduction

This document describes the functional and non-functional requirements for the **Movie Ticket Booking System**. It focuses on **what the system should do** rather than **how it will be implemented**.

## 2. User roles

- **Guest:** An unregistered visitor who can browse movies, cinemas and showtimes but cannot book tickets.
- **Customer:** A registered customer who extends the Guest role with capabilities to book movie tickets, make payments and manage their account.
- **Admin:** A system administrator with full administrative access, responsible for managing system resources such as movies, showtimes,...

## 3. Functional requirements

### 3.1 Authentication

- Register
- Log in
- Log out
- Change password
- Forgot password

### 3.2 User profile

- View profile
- Update profile

### 3.3 Movie

- View now showing movies
- View coming soon movies
- Search movies
- View movie details
- Watch movie trailer

### 3.4 Cinema

- View cinema list
- View cinema details
- View pricing rules

### 3.5 Showtime

- View showtime list
- Filter showtimes

### 3.6 Booking

- View available seats
- Select seats
- Booking ticket (Create booking)
- View booking history
- View booking details
- View e-ticket
- Cancel booking

### 3.7 Payment

- Create payment

### 3.8 Administration

#### 3.8.1 Movie management

- View movie list
- View movie details
- Create movie
- Update movie
- Change movie status

#### 3.8.2 Movie genre management

- View genre list
- Create genre
- Update genre
- Change genre status

#### 3.8.3 Cinema management

- View cinema list
- View cinema details
- Create cinema
- Update cinema
- Change cinema status

#### 3.8.4 Screening room management

- View screening room list
- View screening room details
- Create screening room
- Update screening room
- Change screening room status

#### 3.8.5 Showtime management

- View showtime list
- Filter showtimes
- Create showtime
- Update showtime
- Change showtime status

#### 3.8.6 User management

- View user list
- View user details

#### 3.8.7 Statistics

- Revenue statistics by day
- Now showing movie revenue

#### 3.8.8 Pricing management

- View pricing rules
- Create pricing rule
- Update pricing rule
- Change pricing rule status

## 4. Non-functional Requirements

### 4.1 Performance

- Response time: ≤ 2 seconds.
- Support concurrent users.

### 4.2 Security

- JWT authentication.
- Password hashing (BCrypt).
- HTTPS support (when deployed).
- Role-based access control.

### 4.3 Reliability

- Accurate data storage.
- Prevent duplicate seat bookings.
- Proper error handling.

### 4.4 Usability

- User-friendly interface.
- Responsive design for desktop and mobile devices.

### 4.5 Maintainability

- Layered architecture.
- Easy to maintain and extend.


