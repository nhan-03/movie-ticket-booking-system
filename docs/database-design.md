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
| email     | VARCHAR(255) | UNIQUE, NOT NULL   | User email        |
| password  | VARCHAR(255) | NOT NULL           | Hashed password   |
| full_name | VARCHAR(100) | NOT NULL           | Full name         |
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

---

### movies
Stores movie information.

| Field              | Type        | Constraints | Description                        |
|--------------------|-------------|---|------------------------------------|
| id                 | BIGINT      | PK, AUTO_INCREMENT | Movie identifier                   |
| title              | VARCHAR(255) | NOT NULL | Movie title                        |
| description        | TEXT        | NULL | Movie description                  |
| synopsis           | TEXT        | NULL | Movie synopsis                     |
| duration           | INT         | NOT NULL | Duration in minutes                |
| production_country | VARCHAR(50) | NOT NULL | Movie production country           |
| release_date       | DATE        | NOT NULL | Release date                       |
| poster_url         | VARCHAR(500) | NULL | Poster URL                         |
| translation_type   | ENUM        | NOT NULL | SUBTITLE / DUBBED                  |
| trailer_url        | VARCHAR(500) | NULL | Trailer URL                        |
| age_rating         | VARCHAR(10) | NOT NULL | Age restriction                    |
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

### cinemas
Stores cinema branch information.

| Field | Type | Constraints | Description |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | Cinema identifier |
| name | VARCHAR(255) | NOT NULL | Cinema name |
| address | VARCHAR(255) | NOT NULL | Cinema address |
| city | VARCHAR(100) | NOT NULL | City |
| created_at | TIMESTAMP | NOT NULL | Created time |

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

---

### booking_seats
Stores selected seats in a booking.

| Field      | Type | Constraints | Description |
|------------|---|---|---|
| booking_id | BIGINT | PK, FK | Booking identifier |
| seat_id    | BIGINT | PK, FK | Seat identifier |
| seat_price | DECIMAL(10,2) | NOT NULL | Seat price |

---

### payments
Stores payment transactions.

| Field | Type | Constraints | Description |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | Payment identifier |
| booking_id | BIGINT | FK, NOT NULL | Booking identifier |
| payment_method | VARCHAR(50) | NOT NULL | Payment provider |
| transaction_id | VARCHAR(100) | UNIQUE, NOT NULL | Transaction identifier |
| amount | DECIMAL(10,2) | NOT NULL | Payment amount |
| status | ENUM | NOT NULL | PENDING / SUCCESS / FAILED |
| paid_at | TIMESTAMP | NULL | Payment time |
| created_at | TIMESTAMP | NOT NULL | Created time |

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

### Composite Primary Key
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

## Relationships
- One Movie can have many MovieGenres
- One Genre can have many MovieGenres
- One Cinema has many Rooms
- One Room has many Seats
- One Movie has many Showtimes
- One Room has many Showtimes
- One User has many Bookings
- One Showtime has many Bookings
- One Booking has many Booking Seats
- One Seat can belong to many Booking Seats
- One Booking has one Payment