# Technical Specification Document
# Basic Airline Reservation System

## Document Information

| Item | Value |
|--------|--------|
| Project Name | Basic Airline Reservation System |
| Version | 1.0 |
| Author | Technical Specification |
| Target Audience | Bootcamp Students |
| Document Type | Technical Specification Document |

---

# 1. Introduction

## 1.1 Purpose

The purpose of this system is to allow customers to search for flights, book seats, manage reservations, and view booking details.

The system will provide a simple and beginner-friendly implementation of an airline reservation platform.

## 1.2 Scope

The system includes:

- User registration and login
- Flight management
- Flight search
- Flight booking
- Reservation management
- Booking cancellation
- Basic reporting

The system does not include:

- Online payment integration
- Multi-airline support
- Loyalty programs
- Dynamic pricing
- Real-time flight tracking

---

# 2. Business Requirements

## 2.1 User Roles

### Customer

Can:

- Register an account
- Login
- Search flights
- Book flights
- View reservations
- Cancel reservations

### Administrator

Can:

- Manage flights
- View all reservations
- Update flight schedules
- Generate reports

---

# 3. Functional Requirements

## 3.1 User Management

### FR-001 Register User

Users can create an account.

**Input**
- First Name
- Last Name
- Email
- Password

**Output**
- User account created successfully

---

### FR-002 Login

Users can login using email and password.

**Input**
- Email
- Password

**Output**
- Authentication token/session

---

## 3.2 Flight Management

### FR-003 Create Flight

Actor: Administrator

**Input**
- Flight Number
- Origin
- Destination
- Departure Time
- Arrival Time
- Total Seats

**Output**
- Flight record created

---

### FR-004 Update Flight

Actor: Administrator

**Output**
- Flight details updated

---

### FR-005 Delete Flight

Actor: Administrator

**Output**
- Flight removed from system

---

## 3.3 Flight Search

### FR-006 Search Flights

Actor: Customer

**Input**
- Origin
- Destination
- Departure Date

**Output**
- List of available flights

---

## 3.4 Reservation Management

### FR-007 Book Flight

Actor: Customer

**Input**
- Flight ID
- Passenger Name

**Validation**
- Flight exists
- Available seats > 0

**Output**
- Reservation created
- Reservation Number generated

---

### FR-008 View Reservation

Actor: Customer

**Input**
- Reservation Number

**Output**
- Reservation details

---

### FR-009 Cancel Reservation

Actor: Customer

**Validation**
- Reservation exists

**Output**
- Reservation status updated to Cancelled

---

# 4. Non-Functional Requirements

## 4.1 Performance
- Search results within 3 seconds
- Booking within 5 seconds

## 4.2 Security
- Passwords must be hashed
- Authentication required
- Input validation required

## 4.3 Availability
- 99% uptime target

## 4.4 Scalability
- Up to 1,000 users
- Up to 500 flights

---

# 5. System Architecture

```text
Frontend -> Backend -> Database
```

---

# 6. Database Design

## Users Table
- id (UUID)
- first_name
- last_name
- email
- password_hash
- created_at

## Flights Table
- id (UUID)
- flight_number
- origin
- destination
- departure_time
- arrival_time
- total_seats
- available_seats

## Reservations Table
- id (UUID)
- reservation_number
- user_id
- flight_id
- passenger_name
- status
- booking_date

---

# 7. API Specification

## Register
POST /api/auth/register

## Login
POST /api/auth/login

## Search Flights
GET /api/flights

## Create Reservation
POST /api/reservations

## Cancel Reservation
DELETE /api/reservations/{id}

---

# 8. Error Handling

- 400 Bad Request
- 401 Unauthorized
- 404 Not Found
- 409 Conflict
- 500 Internal Server Error

---

# 9. Future Enhancements

- Payment integration
- Seat selection
- Email notifications
- Multi-airline support
