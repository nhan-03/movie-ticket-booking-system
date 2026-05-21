# API Design

## Authentication APIs

### Register

POST /api/auth/register

Request

```json
{
  "email": "nhan@gmail.com",
  "password": "123456",
  "fullName": "Khong Huu Nhan",
  "phoneNumber": "0862840490"
}
```

Response

```json
{
  "id": 1,
  "email": "nhan@gmail.com",
  "fullName": "Khong Huu Nhan",
  "role": "USER"
}
```

---

### Login

POST /api/auth/login

Request

```json
{
  "email": "nhan@gmail.com",
  "password": "123456"
}
```

Response

```json
{
  "accessToken": "jwt-access-token",
  "refreshToken": "jwt-refresh-token"
}
```

---

### Refresh Access Token

POST /api/auth/refresh

Request

```json
{
  "refreshToken": "jwt-refresh-token"
}
```

Response

```json
{
  "accessToken": "new-access-token"
}
```

---

## User APIs

### Get My Profile

GET /api/users/me

Response

```json
{
  "id": 1,
  "email": "nhan@gmail.com",
  "fullName": "Khong Huu Nhan",
  "phoneNumber": "0862840490",
  "role": "USER",
  "status": "ACTIVE"
}
```

---

### Update My Profile

PATCH /api/users/me

Request

```json
{
  "fullName": "Nguyen Hoang Nhat",
  "phoneNumber": "0378150550"
}
```

Response

```json
{
  "id": 1,
  "email": "nhan@gmail.com",
  "fullName": "Nguyen Hoang Nhat",
  "phoneNumber": "0378150550"
}
```

---

### Change Password

PATCH /api/users/me/password

Request

```json
{
  "oldPassword": "123456",
  "newPassword": "654321"
}
```

Response

```json
{
  "message": "Password changed successfully"
}
```

---

## Movie APIs

### Get All Movies

GET /api/movies?page=1&size=10&keyword=avengers&genre=Action&sortBy=releaseDate&direction=desc

Response

```json
{
  "content": [
    {
      "id": 1,
      "title": "Avengers: Endgame",
      "duration": 181,
      "genre": "Action",
      "language": "English",
      "posterUrl": "https://image.tmdb.org/endgame.jpg",
      "ageRating": "13+"
    },
    {
      "id": 2,
      "title": "Spider-Man: No Way Home",
      "duration": 148,
      "genre": "Action",
      "language": "English",
      "posterUrl": "https://image.tmdb.org/spiderman.jpg",
      "ageRating": "13+"
    }
  ],
  "page": 1,
  "size": 10,
  "totalElements": 120,
  "totalPages": 12
}
```

---

### Get Movie Detail

GET /api/movies/1

Response

```json
{
  "id": 1,
  "title": "Avengers: Endgame",
  "description": "After the devastating events of Infinity War, the Avengers assemble once more to reverse Thanos's actions and restore balance to the universe.",
  "duration": 181,
  "genre": "Action",
  "language": "English",
  "releaseDate": "2019-04-26",
  "posterUrl": "https://image.tmdb.org/endgame.jpg",
  "trailerUrl": "https://youtube.com/watch?v=TcMBFSGVi1c",
  "ageRating": "13+",
  "status": "ACTIVE"
}
```

---

### Create Movie

POST /api/admin/movies

Request

```json
{
  "title": "Interstellar",
  "description": "A team of explorers travel through a wormhole in space in an attempt to ensure humanity's survival.",
  "duration": 169,
  "genre": "Sci-Fi",
  "language": "English",
  "releaseDate": "2014-11-07",
  "posterUrl": "https://image.tmdb.org/interstellar.jpg",
  "trailerUrl": "https://youtube.com/watch?v=zSWdZVtXT7E",
  "ageRating": "13+"
}
```

Response

```json
{
  "id": 3,
  "title": "Interstellar",
  "status": "ACTIVE"
}
```

---

### Update Movie

PATCH /api/admin/movies/3

Request

```json
{
  "duration": 170,
  "genre": "Science Fiction"
}
```

Response

```json
{
  "id": 3,
  "title": "Interstellar",
  "duration": 170,
  "genre": "Science Fiction"
}
```

---

### Update Movie Status

PATCH /api/admin/movies/3/status

Request

```json
{
  "status": "INACTIVE"
}
```

Response

```json
{
  "id": 3,
  "status": "INACTIVE"
}
```

---

## Cinema APIs

### Get All Cinemas

GET /api/cinemas

Response

```json
[
  {
    "id": 1,
    "name": "CGV Vincom Thu Duc",
    "address": "216 Vo Van Ngan",
    "city": "Ho Chi Minh City"
  },
  {
    "id": 2,
    "name": "Lotte Cinema Binh Duong",
    "address": "Aeon Mall Binh Duong",
    "city": "Binh Duong"
  }
]
```

---

### Get Cinema Detail

GET /api/cinemas/1

Response

```json
{
  "id": 1,
  "name": "CGV Vincom Thu Duc",
  "address": "216 Vo Van Ngan",
  "city": "Ho Chi Minh City"
}
```

---

## Showtime APIs

### Get Showtimes By Movie

GET /api/showtimes/movies/1

Response

```json
[
  {
    "id": 1,
    "cinemaName": "CGV Vincom Thu Duc",
    "roomName": "Room 1",
    "startTime": "2026-06-01T18:00:00",
    "endTime": "2026-06-01T21:01:00"
  },
  {
    "id": 2,
    "cinemaName": "Lotte Cinema Binh Duong",
    "roomName": "Room 3",
    "startTime": "2026-06-01T20:00:00",
    "endTime": "2026-06-01T23:01:00"
  }
]
```

---

### Create Showtime

POST /api/admin/showtimes

Request

```json
{
  "movieId": 1,
  "roomId": 2,
  "startTime": "2026-06-01T18:00:00",
  "endTime": "2026-06-01T21:01:00"
}
```

Response

```json
{
  "id": 5,
  "movieId": 1,
  "roomId": 2
}
```

---

### Update Showtime

PATCH /api/admin/showtimes/5

Request

```json
{
  "startTime": "2026-06-01T19:00:00"
}
```

Response

```json
{
  "id": 5,
  "startTime": "2026-06-01T19:00:00"
}
```

---

### Update Showtime Status

PATCH /api/admin/showtimes/5/status

Request

```json
{
  "status": "CANCELLED"
}
```

Response

```json
{
  "id": 5,
  "status": "CANCELLED"
}
```

---

## Seat APIs

### Get Available Seats

GET /api/showtimes/1/seats

Response

```json
[
  {
    "seatId": 1,
    "seatRow": "A",
    "seatNumber": 1,
    "seatType": "NORMAL",
    "price": 80000,
    "available": true
  },
  {
    "seatId": 2,
    "seatRow": "A",
    "seatNumber": 2,
    "seatType": "VIP",
    "price": 120000,
    "available": false
  }
]
```

---

## Booking APIs

### Create Booking

POST /api/bookings

Request

```json
{
  "showtimeId": 1,
  "seatIds": [1, 3]
}
```

Response

```json
{
  "bookingId": 1,
  "bookingCode": "BK20260601001",
  "status": "PENDING",
  "totalPrice": 160000
}
```

---

### Get My Bookings

GET /api/bookings/me?page=1&size=10

Response

```json
{
  "content": [
    {
      "bookingId": 1,
      "bookingCode": "BK20260601001",
      "status": "PAID",
      "totalPrice": 160000
    },
    {
      "bookingId": 2,
      "bookingCode": "BK20260602001",
      "status": "PENDING",
      "totalPrice": 240000
    }
  ],
  "page": 1,
  "size": 10,
  "totalElements": 20,
  "totalPages": 2
}
```

---

### Get Booking Detail

GET /api/bookings/1

Response

```json
{
  "bookingId": 1,
  "bookingCode": "BK20260601001",
  "status": "PAID",
  "totalPrice": 160000,
  "movieTitle": "Avengers: Endgame",
  "cinemaName": "CGV Vincom Thu Duc",
  "roomName": "Room 1",
  "startTime": "2026-06-01T18:00:00",
  "seats": [
    {
      "seatRow": "A",
      "seatNumber": 1,
      "price": 80000
    },
    {
      "seatRow": "A",
      "seatNumber": 3,
      "price": 80000
    }
  ]
}
```

---

### Cancel Booking

PATCH /api/bookings/1/cancel

Response

```json
{
  "bookingId": 1,
  "status": "CANCELLED"
}
```

---

## Payment APIs

### Create Payment

POST /api/payments

Request

```json
{
  "bookingId": 1,
  "paymentMethod": "VNPAY"
}
```

Response

```json
{
  "paymentUrl": "https://sandbox.vnpayment.vn/paymentv2/vpcpay.html"
}
```

---

### Payment Callback

POST /api/payments/callback

Request

```json
{
  "transactionId": "VNP123456789",
  "bookingCode": "BK20260601001",
  "status": "SUCCESS"
}
```

Response

```json
{
  "message": "Payment processed successfully"
}
```

---

## Admin User APIs

### Get All Users

GET /api/admin/users?page=1&size=10&keyword=nguyen

Response

```json
{
  "content": [
    {
      "id": 1,
      "email": "nhan@gmail.com",
      "fullName": "Khong Huu Nhan",
      "role": "USER",
      "status": "ACTIVE"
    },
    {
      "id": 2,
      "email": "nhat@gmail.com",
      "fullName": "Nguyen Hoang Nhat",
      "role": "USER",
      "status": "INACTIVE"
    }
  ],
  "page": 1,
  "size": 10,
  "totalElements": 50,
  "totalPages": 5
}
```

---

### Get User Detail

GET /api/admin/users/1

Response

```json
{
  "id": 1,
  "email": "nhan@gmail.com",
  "fullName": "Khong Huu Nhan",
  "phoneNumber": "0862840490",
  "role": "USER",
  "status": "ACTIVE"
}
```

---

### Update User Status

PATCH /api/admin/users/1/status

Request

```json
{
  "status": "INACTIVE"
}
```

Response

```json
{
  "id": 1,
  "status": "INACTIVE"
}
```

---

## Revenue APIs

### Get Revenue Summary

GET /api/admin/revenue?from=2026-06-01&to=2026-06-30

Response

```json
{
  "totalRevenue": 250000000,
  "totalBookings": 3200,
  "successfulPayments": 3150
}
```

---

### Get Revenue By Month

GET /api/admin/revenue/monthly?year=2026

Response

```json
[
  {
    "month": 1,
    "revenue": 120000000
  },
  {
    "month": 2,
    "revenue": 180000000
  },
  {
    "month": 3,
    "revenue": 250000000
  }
]
```

---

## Authorization

Protected APIs require JWT token.

Example

```http
Authorization: Bearer <access-token>
```

---

## Roles

### USER

- View movies
- View showtimes
- Book tickets
- Make payments
- Manage personal profile

### ADMIN

- Manage movies
- Manage showtimes
- Manage users
- View bookings
- View revenue