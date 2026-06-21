# Technical Specification Document

# Basic Airline Reservation System

## Document Information

| Item            | Value                            |
| --------------- | -------------------------------- |
| Project Name    | Basic Airline Reservation System |
| Version         | 1.0                              |
| Author          | Technical Specification          |
| Target Audience | Bootcamp Students                |
| Document Type   | Technical Specification Document |

---

# 1. Introduction

## 1.1 Purpose

The purpose of this system is to allow customers to search for flights, book seats, manage reservations, and view booking details.

The system will provide a simple and beginner-friendly implementation of an airline reservation platform.

## 1.2 Scope

The system includes:

* User registration and login
* Flight management
* Flight search
* Flight booking
* Reservation management
* Booking cancellation
* Basic reporting

The system does not include:

* Online payment integration
* Multi-airline support
* Loyalty programs
* Dynamic pricing
* Real-time flight tracking

---

# 2. Business Requirements

## 2.1 User Roles

### Customer

Can:

* Register an account
* Login
* Search flights
* Book flights
* View reservations
* Cancel reservations

### Administrator

Can:

* Manage flights
* View all reservations
* Update flight schedules
* Generate reports

---

# 3. Functional Requirements

## 3.1 User Management

### FR-001 Register User

**Description**

Users can create an account.

**Input**

* First Name
* Last Name
* Email
* Password

**Output**

* User account created successfully

---

### FR-002 Login

**Description**

Users can login using email and password.

**Input**

* Email
* Password

**Output**

* Authentication token/session

---

## 3.2 Flight Management

### FR-003 Create Flight

**Actor**

Administrator

**Input**

* Flight Number
* Origin
* Destination
* Departure Time
* Arrival Time
* Total Seats

**Output**

* Flight record created

---

### FR-004 Update Flight

**Actor**

Administrator

**Output**

* Flight details updated

---

### FR-005 Delete Flight

**Actor**

Administrator

**Output**

* Flight removed from system

---

## 3.3 Flight Search

### FR-006 Search Flights

**Actor**

Customer

**Input**

* Origin
* Destination
* Departure Date

**Output**

List of available flights:

* Flight Number
* Origin
* Destination
* Departure Time
* Available Seats

---

## 3.4 Reservation Management

### FR-007 Book Flight

**Actor**

Customer

**Input**

* Flight ID
* Passenger Name

**Validation**

* Flight exists
* Available seats > 0

**Output**

* Reservation created
* Reservation Number generated

---

### FR-008 View Reservation

**Actor**

Customer

**Input**

* Reservation Number

**Output**

Reservation details

---

### FR-009 Cancel Reservation

**Actor**

Customer

**Validation**

* Reservation exists

**Output**

* Reservation status updated to Cancelled
* Seat returned to flight inventory

---

# 4. Non-Functional Requirements

## 4.1 Performance

* Search results returned within 3 seconds
* Booking completed within 5 seconds

## 4.2 Security

* Passwords must be hashed
* Authenticated endpoints require login
* Input validation required

## 4.3 Availability

* System uptime target: 99%

## 4.4 Scalability

* Support up to 1,000 users
* Support up to 500 flights

---

# 5. System Architecture

## 5.1 High-Level Architecture

```text
+-------------+
|   Frontend  |
+------+------+
       |
       v
+-------------+
|   Backend   |
| REST API    |
+------+------+
       |
       v
+-------------+
|  Database   |
+-------------+
```

---

## 5.2 Components

### Frontend

Responsibilities:

* Display user interface
* Submit requests to backend
* Show booking results

Example Technologies:

* React
* Vue
* Angular

---

### Backend

Responsibilities:

* Business logic
* Authentication
* Flight management
* Reservation management

Example Technologies:

* Node.js
* Express
* Java Spring Boot
* ASP.NET

---

### Database

Responsibilities:

* Store users
* Store flights
* Store reservations

Example Databases:

* PostgreSQL
* MySQL
* SQL Server

---

# 6. Database Design

## 6.1 Users Table

| Column        | Type     |
| ------------- | -------- |
| id            | UUID     |
| first_name    | VARCHAR  |
| last_name     | VARCHAR  |
| email         | VARCHAR  |
| password_hash | VARCHAR  |
| created_at    | DATETIME |

---

## 6.2 Flights Table

| Column          | Type     |
| --------------- | -------- |
| id              | UUID     |
| flight_number   | VARCHAR  |
| origin          | VARCHAR  |
| destination     | VARCHAR  |
| departure_time  | DATETIME |
| arrival_time    | DATETIME |
| total_seats     | INTEGER  |
| available_seats | INTEGER  |
| created_at      | DATETIME |

---

## 6.3 Reservations Table

| Column             | Type     |
| ------------------ | -------- |
| id                 | UUID     |
| reservation_number | VARCHAR  |
| user_id            | UUID     |
| flight_id          | UUID     |
| passenger_name     | VARCHAR  |
| status             | VARCHAR  |
| booking_date       | DATETIME |

---

# 7. Entity Relationship Diagram (ERD)

```text
+--------+
| Users  |
+--------+
| id     |
+--------+
    |
    | 1
    |
    | N
+-------------+
|Reservation  |
+-------------+
| id          |
| user_id     |
| flight_id   |
+-------------+
    |
    | N
    |
    | 1
+---------+
| Flights |
+---------+
| id      |
+---------+
```

---

# 8. API Specification

## Authentication

### Register User

```http
POST /api/auth/register
```

Request

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@email.com",
  "password": "password123"
}
```

Response

```json
{
  "message": "User registered successfully"
}
```

---

### Login

```http
POST /api/auth/login
```

Request

```json
{
  "email": "john@email.com",
  "password": "password123"
}
```

Response

```json
{
  "token": "jwt-token"
}
```

---

## Flights

### Search Flights

```http
GET /api/flights
```

Query Parameters

```text
origin=Manila
destination=Cebu
date=2026-06-01
```

Response

```json
[
  {
    "flightId": "123",
    "flightNumber": "PR101",
    "origin": "Manila",
    "destination": "Cebu",
    "availableSeats": 50
  }
]
```

---

## Reservations

### Create Reservation

```http
POST /api/reservations
```

Request

```json
{
  "flightId": "123",
  "passengerName": "John Doe"
}
```

Response

```json
{
  "reservationNumber": "RES-001",
  "status": "Confirmed"
}
```

---

### Cancel Reservation

```http
DELETE /api/reservations/{id}
```

Response

```json
{
  "message": "Reservation cancelled"
}
```

---

# 9. Validation Rules

## User

* Email must be unique
* Password minimum 8 characters

## Flight

* Arrival time must be after departure time
* Total seats must be greater than 0

## Reservation

* Passenger name required
* Flight must have available seats

---

# 10. Error Handling

| Error Code | Description           |
| ---------- | --------------------- |
| 400        | Bad Request           |
| 401        | Unauthorized          |
| 404        | Resource Not Found    |
| 409        | Conflict              |
| 500        | Internal Server Error |

Example:

```json
{
  "error": "Flight not found"
}
```

---

# 11. Assumptions

* One reservation equals one passenger.
* Seat numbers are not assigned.
* Payment processing is outside project scope.
* Flights belong to a single airline.
* Email notifications are not implemented.

---

# 12. Future Enhancements

Possible future improvements:

* Online payment gateway
* Seat selection
* Multi-passenger booking
* Boarding pass generation
* Email notifications
* Flight status tracking
* Loyalty rewards system
* Multi-airline integration

---

# 13. Success Criteria

The system is considered successful when users can:

1. Register and login.
2. Search available flights.
3. Create reservations.
4. View reservations.
5. Cancel reservations.
6. Administrators can manage flights.

---

# Appendix A - Suggested Tech Stack

## Frontend

* React
* TypeScript
* Tailwind CSS

## Backend

* Node.js
* Express.js

## Database

* PostgreSQL

## Authentication

* JWT (JSON Web Token)

## Deployment

* Docker
* Render
* Railway
* AWS

---

End of Document
