# API Design

## Authentication APIs

### Register

POST /api/auth/register

Request

```json
{
  "fullName": "Khong Huu Nhan",
  "email": "nhan@gmail.com",
  "password": "123456",
  "phoneNumber": "0862840490"
}
```

Response

```json
{
  "id": 1,
  "fullName": "Khong Huu Nhan",
  "email": "nhan@gmail.com",
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
  "fullName": "Khong Huu Nhan",
  "email": "nhan@gmail.com",
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
  "fullName": "Nguyen Hoang Nhat",
  "email": "nhan@gmail.com",
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

GET /api/movies

Response

```json
{
  "content": [
    {
      "id": 1,
      "title": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
      "genres": ["Hoạt hình", "Phiêu lưu"],
      "duration_minutes": 101,
      "translation_type": "Nhật Bản",
      "ageRating": "P",
      "release_date": "2026-04-30",
      "posterUrl": "https://d1j8pt39mxlh8d.cloudfront.net/...jpg",
      "trailerUrl": "https://youtube.com/watch?v=zSWdZVtXT7E"
    },
    {
      "id": 2,
      "title": "Ngôi đền kỳ quái",
      "genres": ["Hài", "Kinh dị"],
      "duration_minutes": 118,
      "translation_type": "Thái Lan",
      "ageRating": "T16",
      "release_date": "2026-04-02",
      "posterUrl": "https://d1j8pt39mxlh8d.cloudfront.net/...jpg",
      "trailerUrl": "https://youtube.com/watch?v=zSWdZVtXT7E"
    }
  ],
  "page": 1,
  "size": 2
}
```

---

### Get Movie Detail

GET /api/movies/1

Response

```json
{
  "id": 1,
  "title": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
  "genres": ["Hoạt hình", "Phiêu lưu"],
  "duration_minutes": 101,
  "translation_type": "Nhật Bản",
  "ageRating": "P",
  "director": "Tetsuo Yajima",
  "actors": "Wasabi Mizuta, Megumi Oohara, Yumi Kakazu, Subaru Kimura, Tomokazu Seki,...",
  "release_date": "2026-04-30",
  "synopsis": "Bước vào kì nghỉ hè, Nobita và các bạn tranh cãi chí chóe về địa điểm cắm trại. Theo đề xuất của Doraemon, cả nhóm quyết định cắm trại giữa lòng đại dương! Sử dụng bảo bối thần kì “xe Buggy chạy dưới nước” và “đèn pin thích nghi”, 5 bạn nhỏ tận hưởng chuyến cắm trại dưới đáy biển, gặp gỡ vô vàn sinh vật lí thú trên đường đi. Sau khi phát hiện một chiếc tàu đắm, nhóm bạn đã gặp chàng thanh niên bí ẩn El. Thật bất ngờ, anh ta lại là cư dân đáy biển, sống tại “liên bang Mu”, một vùng",
  "posterUrl": "https://d1j8pt39mxlh8d.cloudfront.net/...jpg",
  "trailerUrl": "https://youtube.com/watch?v=zSWdZVtXT7E"
}
```

---

### Create Movie

POST /api/admin/movies

Request

```json
{
  "title": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
  "genres": ["Hoạt hình", "Phiêu lưu"],
  "duration_minutes": 101,
  "translation_type": "Nhật Bản",
  "ageRating": "P",
  "release_date": "2026-04-30",
  "posterUrl": null,
  "trailerUrl": null
}
```

Response

```json
{
  "id": 3,
  "title": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
  "status": "ACTIVE"
}
```

---

### Update Movie

PATCH /api/admin/movies/3

Request

```json
{
  "duration_minutes": 170,
  "translation_type": "Thái Lan"
}
```

Response

```json
{
  "id": 3,
  "title": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
  "duration_minutes": 170,
  "translation_type": "Thái Lan"
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
    "name": "Cinema Quốc Thành",
    "address": "271 Nguyễn Trãi, phường Cầu Ông Lãnh",
    "city": "TP.HCM"
  },
  {
    "id": 2,
    "name": "Cinema Quận 6",
    "address": "1446 Võ Văn Kiệt, phường Bình Tiên",
    "city": "TP.HCM"
  }
]
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
    "cinemaName": "Cinema Quốc Thành",
    "roomNumber": 1,
    "startTime": "2026-06-01T18:00:00",
    "endTime": "2026-06-01T21:01:00"
  },
  {
    "id": 2,
    "cinemaName": "Cinema Quận 6",
    "roomNumber": 2,
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

### Get Seats By Showtime

GET /api/showtimes/1/seats

Response

```json
[
  {
    "seatId": 1,
    "seatRow": "A",
    "seatNumber": 1,
    "seatType": "SINGLE",
    "dayType": "WEEKDAY",
    "price": 80000,
    "available": true
  },
  {
    "seatId": 2,
    "seatRow": "A",
    "seatNumber": 2,
    "seatType": "COUPLE",
    "dayType": "WEEKEND",
    "price": 200000,
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
  "seatIds": [1, 2]
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

GET /api/bookings/me

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
  ]
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
  "movieTitle": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
  "cinemaName": "Cinema Quốc Thành",
  "roomNumber": 1,
  "startTime": "2026-06-01T18:00:00",
  "seats": [
    {
      "seatRow": "A",
      "seatNumber": 1,
      "price": 80000
    },
    {
      "seatRow": "A",
      "seatNumber": 2,
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

GET /api/admin/users

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
  ]
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
  "status": "ACTIVE",
  "bookingCount": 12,
  "createdAt": "2026-05-01T10:00:00",
  "updatedAt": "2026-05-20T15:30:00"
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

### Movie Performance Analytics

GET /api/admin/dashboard/movie-performance

Purpose

Used to evaluate the performance of currently showing movies and support business decisions such as increasing or reducing showtimes.

Business Rules

- Only movies with status `NOW_SHOWING` are included
- Only movies that have been showing for 5–14 days are analyzed
- Movies showing for too few days may not have enough data
- Movies near the end of their lifecycle may naturally have lower demand

Average Revenue Formula

```text
avgRevenue =
totalRevenue / (daysShowing × showtimeCount)
```

Response

```json
[
  {
    "movieId": 1,
    "movieTitle": "Phim điện ảnh Doraemon: Nobita và lâu đài dưới đáy biển",
    "avgRevenue": 4000000
  },
  {
    "movieId": 2,
    "movieTitle": "Ngôi đền kỳ quái",
    "avgRevenue": 693333
  }
]
```

---

### Get Revenue By Month

GET /api/admin/dashboard/revenue/monthly?year=2026

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
- View dashboard