# Database Design

## Entity Relationship Diagram

![ERD](images/erd.png)

---

# Database Design

## Entities

### Users
Stores user account information for authentication and booking.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| email | varchar | Unique email |
| password | varchar | Hashed password |
| full_name | varchar | User full name |
| phone_number | varchar | Phone number |
| role | varchar | USER / ADMIN |
| status | varchar | Account status |
| created_at | timestamp | Created time |
| updated_at | timestamp | Updated time |

---

### Movies
Stores movie information displayed to users.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| title | varchar | Movie title |
| description | text | Movie description |
| duration | int | Duration in minutes |
| genre | varchar | Genre |
| language | varchar | Language |
| release_date | date | Release date |
| poster_url | varchar | Poster image URL |
| trailer_url | varchar | Trailer URL |
| age_rating | varchar | Age restriction |
| status | varchar | ACTIVE / INACTIVE |
| created_at | timestamp | Created time |
| updated_at | timestamp | Updated time |

---

### Cinemas
Stores cinema branch information.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| name | varchar | Cinema name |
| address | varchar | Address |
| city | varchar | City |
| created_at | timestamp | Created time |

---

### Rooms
Stores screening rooms inside cinemas.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| cinema_id | bigint | Foreign key to cinemas |
| name | varchar | Room name |
| room_type | varchar | STANDARD / VIP / IMAX |
| capacity | int | Total seats |
| created_at | timestamp | Created time |

---

### Seats
Stores seat layout for each room.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| room_id | bigint | Foreign key to rooms |
| seat_row | varchar | Row |
| seat_number | int | Number |
| seat_type | varchar | NORMAL / VIP / COUPLE |
| created_at | timestamp | Created time |

---

### Showtimes
Stores movie schedules in rooms.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| movie_id | bigint | Foreign key to movies |
| room_id | bigint | Foreign key to rooms |
| start_time | timestamp | Start time |
| end_time | timestamp | End time |
| price | decimal | Ticket price |
| status | varchar | ACTIVE / CANCELLED |
| created_at | timestamp | Created time |

---

### Bookings
Stores ticket booking transactions.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| user_id | bigint | Foreign key to users |
| showtime_id | bigint | Foreign key to showtimes |
| booking_code | varchar | Unique code |
| total_price | decimal | Total amount |
| status | varchar | PENDING / PAID / CANCELLED |
| created_at | timestamp | Created time |

---

### Booking_Seats
Stores seats selected in each booking.

| Field | Type | Description |
|------|------|-------------|
| booking_id | bigint | Foreign key to bookings |
| seat_id | bigint | Foreign key to seats |
| price | decimal | Seat price |

---

### Payments
Stores payment transactions.

| Field | Type | Description |
|------|------|-------------|
| id | bigint | Primary key |
| booking_id | bigint | Foreign key to bookings |
| payment_method | varchar | Payment provider |
| transaction_id | varchar | External transaction id |
| amount | decimal | Payment amount |
| status | varchar | SUCCESS / FAILED / PENDING |
| paid_at | timestamp | Payment time |
| created_at | timestamp | Created time |

---

## Keys

- Primary Keys:
    - users.id
    - movies.id
    - cinemas.id
    - rooms.id
    - seats.id
    - showtimes.id
    - bookings.id
    - payments.id

- Composite Key:
    - booking_seats (booking_id, seat_id)

- Unique Keys:
    - users.email
    - bookings.booking_code
    - payments.transaction_id

- Foreign Keys:
    - rooms.cinema_id → cinemas.id
    - seats.room_id → rooms.id
    - showtimes.movie_id → movies.id
    - showtimes.room_id → rooms.id
    - bookings.user_id → users.id
    - bookings.showtime_id → showtimes.id
    - booking_seats.booking_id → bookings.id
    - booking_seats.seat_id → seats.id
    - payments.booking_id → bookings.id

---

## Relationships

- One Cinema has many Rooms
- One Room has many Seats
- One Movie has many Showtimes
- One Room has many Showtimes
- One User has many Bookings
- One Showtime has many Bookings
- One Booking has many Booking_Seats
- One Seat can appear in many Booking_Seats (different showtimes)
- One Booking has one Payment