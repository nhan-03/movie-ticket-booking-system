# Database Design

## Entity-Relationship Diagram (ERD)

![ERD](images/erd.png)

---

## Table

### users
Stores user account information.

| Field     | Type         | Constraints        | Description       |
|-----------|--------------|--------------------|-------------------|
| id        | BIGINT       | PK, AUTO_INCREMENT | User identifier   |
| full_name | VARCHAR(100) | NOT NULL           | Full name         |
| email     | VARCHAR(255) | UNIQUE, NOT NULL   | User email        |
| password  | VARCHAR(255) | NOT NULL           | Hashed password   |
| phone_number | VARCHAR(20)  | UNIQUE, NOT NULL   | Phone number      |
| role      | ENUM         | NOT NULL       | ADMIN / USER      |
| status    | ENUM         | NOT NULL           | ACTIVE / INACTIVE |
| created_at | TIMESTAMP    | NOT NULL           | Created time      |
| updated_at | TIMESTAMP    | NOT NULL           | Updated time      |

---

### genres

Represents a movie genre category.

| Attribute | Type | Constraints | Description      |
|---|---|---|------------------|
| id | BIGINT | PK, AUTO_INCREMENT | Genre identifier |
| name | VARCHAR(50) | NOT NULL, UNIQUE | Genre name       |
| created_at | TIMESTAMP    | NOT NULL           | Created time      |
| updated_at | TIMESTAMP    | NOT NULL           | Updated time      |

---

### movies
Stores movie information.

| Field              | Type         | Constraints | Description              |
|--------------------|--------------|---|--------------------------|
| id                 | BIGINT       | PK, AUTO_INCREMENT | Movie identifier         |
| title              | VARCHAR(255) | NOT NULL | Movie title              |
| duration_minutes   | INT          | NOT NULL | Duration in minutes      |
| production_country | VARCHAR(50)  | NOT NULL | Movie production country |
| translation_type   | ENUM         | NOT NULL | SUBTITLE / DUBBED        |
| age_rating         | ENUM         | NOT NULL | P / C13 / C16 / C18      |
| director           | VARCHAR(150) | NOT NULL | Movie director           |
| actors             | VARCHAR(500) | NOT NULL | Movie actors             |
| release_date       | DATE        | NOT NULL | Release date                       |
| synopsis           | TEXT         | NOT NULL | Movie synopsis           |
| poster_url         | VARCHAR(500) | NULL | Poster URL                         |
| trailer_url        | VARCHAR(500) | NULL | Trailer URL                        |
| status             | ENUM        | NOT NULL | COMMING_SOON / NOW_SHOWING / ENDED |
| created_at         | TIMESTAMP   | NOT NULL | Created time                       |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### movie_genres

Junction table representing the many-to-many relationship between movies and genres.

| Attribute | Type | Constraints | Description |
|---|---|---|---|
| movie_id | BIGINT | PK, FK | Referenced movie |
| genre_id | BIGINT | PK, FK | Referenced genre |
| created_at | TIMESTAMP    | NOT NULL           | Created time      |
| updated_at | TIMESTAMP    | NOT NULL           | Updated time      |

### cinemas
Stores cinema branch information.

| Field | Type | Constraints | Description |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | Cinema identifier |
| name | VARCHAR(255) | NOT NULL | Cinema name |
| address | VARCHAR(255) | NOT NULL | Cinema address |
| city | VARCHAR(100) | NOT NULL | City |
| created_at | TIMESTAMP | NOT NULL | Created time |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### rooms
Stores screening rooms.

| Field | Type | Constraints | Description |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | Room identifier |
| cinema_id | BIGINT | FK, NOT NULL | Cinema identifier |
| name | VARCHAR(100) | NOT NULL | Room name |
| capacity | INT | NOT NULL | Total seats |
| created_at | TIMESTAMP | NOT NULL | Created time |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### seats
Stores room seat information.

| Field | Type | Constraints | Description     |
|---|---|---|-----------------|
| id | BIGINT | PK, AUTO_INCREMENT | Seat identifier |
| room_id | BIGINT | FK, NOT NULL | Room identifier |
| seat_row | VARCHAR(5) | NOT NULL | Seat row        |
| seat_number | INT | NOT NULL | Seat number     |
| seat_type | ENUM | NOT NULL | SINGLE / COUPLE |
| created_at | TIMESTAMP | NOT NULL | Created time    |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### showtimes
Stores movie schedules.

| Field | Type | Constraints | Description |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | Showtime identifier |
| movie_id | BIGINT | FK, NOT NULL | Movie identifier |
| room_id | BIGINT | FK, NOT NULL | Room identifier |
| start_time | TIMESTAMP | NOT NULL | Start time |
| end_time | TIMESTAMP | NOT NULL | End time |
| status | ENUM | NOT NULL | ACTIVE / CANCELLED |
| created_at | TIMESTAMP | NOT NULL | Created time |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### pricing_rules
Represents pricing configuration based on seat type and day type.

| Field | Type | Constraints | Description             |
|---|---|---|-------------------------|
| id | BIGINT | PK | Pricing rule identifier |
| seat_type | ENUM | NOT NULL | SINGLE / COUPLE         |
| day_type | ENUM | NOT NULL | WEEKDAY / WEEKEND       |
| price | DECIMAL(10,2) | NOT NULL | Ticket price            |
| created_at | TIMESTAMP | NOT NULL | Created time |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### bookings
Stores booking transactions.

| Field | Type | Constraints | Description |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | Booking identifier |
| user_id | BIGINT | FK, NOT NULL | User identifier |
| showtime_id | BIGINT | FK, NOT NULL | Showtime identifier |
| booking_code | VARCHAR(50) | UNIQUE, NOT NULL | Booking code |
| total_price | DECIMAL(10,2) | NOT NULL | Total amount |
| status | ENUM | NOT NULL | PENDING / PAID / CANCELLED |
| created_at | TIMESTAMP | NOT NULL | Created time |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### booking_seats
Stores selected seats in a booking.

| Field      | Type | Constraints | Description |
|------------|---|---|---|
| booking_id | BIGINT | PK, FK | Booking identifier |
| seat_id    | BIGINT | PK, FK | Seat identifier |
| seat_price | DECIMAL(10,2) | NOT NULL | Seat price |
| created_at | TIMESTAMP | NOT NULL | Created time |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

### payments
Stores payment transactions.

| Field            | Type          | Constraints        | Description                |
|------------------|---------------|--------------------|----------------------------|
| id               | BIGINT        | PK, AUTO_INCREMENT | Payment identifier         |
| booking_id       | BIGINT        | FK, NOT NULL       | Booking identifier         |
| payment_method   | ENUM          | NOT NULL           | MOMO / VNPAY               |
| transaction_code | VARCHAR(100)  | UNIQUE, NOT NULL   | Transaction code           |
| amount           | DECIMAL(10,2) | NOT NULL           | Payment amount             |
| status           | ENUM          | NOT NULL           | PENDING / SUCCESS / FAILED |
| paid_at          | TIMESTAMP     | NULL           | Payment time               |
| created_at       | TIMESTAMP     | NOT NULL           | Created time               |
| updated_at         | TIMESTAMP   | NOT NULL | Updated time                       |

---

## Primary Keys
- users.id
- genres.id
- movies.id
- cinemas.id
- rooms.id
- seats.id
- showtimes.id
- bookings.id
- payments.id

## Composite Primary Key
- movie_genres (movie_id, genre_id)
- booking_seats (booking_id, seat_id)

---

## Foreign Keys

| Table         | Foreign Key | References   |
|---------------|-------------|--------------|
| rooms         | cinema_id   | cinemas.id   |
| users         | role_id     | roles.id     |
| seats         | room_id     | rooms.id     |
| showtimes     | movie_id    | movies.id    |
| showtimes     | room_id     | rooms.id     |
| bookings      | user_id     | users.id     |
| bookings      | showtime_id | showtimes.id |
| booking_seats | booking_id  | bookings.id  |
| booking_seats | seat_id     | seats.id     |
| payments      | booking_id  | bookings.id  |

---

## Unique Constraints
- seats (room_id, seat_row, seat_number)
- pricing_rules (seat_type, day_type)

---

## Relationships
- One Movie has many MovieGenres
- One Genre has many MovieGenres
- One Cinema has many Rooms
- One Room has many Seats
- One Movie has many Showtimes
- One Room has many Showtimes
- One User has many Bookings
- One Showtime has many Bookings
_ One PricingRule applies to one seat type and one day type
- One Booking has many Booking Seats
- One Seat can belong to many Booking Seats
- One Booking has one Payment

---

## Pricing Logic
Ticket price is determined based on:
- Seat type (SINGLE or COUPLE)
- Day type (WEEKDAY or WEEKEND)
The calculated price is stored in booking_seats.seat_price at booking time to preserve historical pricing.