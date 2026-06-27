# API Documentation

## User Registration Endpoint

### Endpoint
```
POST /users/register
```

### Description
This endpoint allows users to create a new account by providing their personal information and credentials. The endpoint validates the input data, checks for existing users, hashes the password, and returns an authentication token upon successful registration.

---

## Request Details

### HTTP Method
`POST`


### Request Body
The request body must be a JSON object with the following structure:

```json
{
  "fullname": {
    "firstname": "string (required)",
    "lastname": "string (optional)"
  },
  "email": "string (required)",
  "password": "string (required)"
}
```

### Request Body Parameters

| Parameter | Type | Required | Constraints | Description |
|-----------|------|----------|-------------|-------------|
| `fullname.firstname` | string | Yes | Minimum 3 characters | User's first name |
| `fullname.lastname` | string | No | Minimum 3 characters | User's last name |
| `email` | string | Yes | Valid email format | User's email address (must be unique) |
| `password` | string | Yes | Minimum 6 characters | User's password (will be hashed) |

### Example Request

```bash
curl -X POST http://localhost:3000/users/register \
  -H "Content-Type: application/json" \
  -d '{
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "password": "securepassword123"
  }'
```

---

## Response Details

### Success Response

**Status Code:** `201 Created`

**Response Body:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "_id": "65a1f2e8c3d4e5f6g7h8i9j0",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "socketId": null
  }
}
```

**Response Details:**
- `token`: JWT authentication token (valid for 24 hours)
- `user`: Registered user object with ID and profile information

---
## User Login Endpoint

### Endpoint
```
POST /users/login
```

### Description
This endpoint allows users to authenticate using their email and password. The endpoint validates the input data, verifies the user's credentials, and returns an authentication token upon successful login.

---

## Login Request Details

### HTTP Method
`POST`

### Request Body
The request body must be a JSON object with the following structure:

```json
{
  "email": "string (required)",
  "password": "string (required)"
}
```

### Request Body Parameters

| Parameter | Type | Required | Constraints | Description |
|-----------|------|----------|-------------|-------------|
| `email` | string | Yes | Valid email format | User's email address |
| `password` | string | Yes | Minimum 6 characters | User's password |

### Example Request

```bash
curl -X POST http://localhost:3000/users/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john.doe@example.com",
    "password": "securepassword123"
  }'
```

---

## Login Response Details

### Success Response

**Status Code:** `200 OK`

**Response Body:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "_id": "65a1f2e8c3d4e5f6g7h8i9j0",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "socketId": null
  }
}
```
**Response Details:**
- `token`: JWT authentication token (valid for 24 hours)
- `user`: Authenticated user object with ID and profile information

---

## Status Codes Summary

| Status Code | Meaning | Scenario |
|-------------|---------|----------|
| `201` | Created | User successfully registered |
| `200` | OK | User successfully logged in |
| `400` | Bad Request | Validation failed or user already exists |
| `401` | Unauthorized | Invalid login credentials |
| `500` | Internal Server Error | Server-side error (missing required fields) |

---
# 🚖 Captain Registration API

This API provides endpoints for captain registration with validation, password hashing, and JWT-based authentication.

---

## 🚀 Endpoints

### 1. Register Captain  
**POST** `/captains/register`

Registers a new captain with vehicle details.

**Request Body (JSON):**
```json
{
  "fullname": {
    "firstname": "captain_firstname",
    "lastname": "captain_lastname"
  },
  "email": "captain@gmail.com",
  "password": "test_captain",
  "vehicle": {
    "plate": "UP 15 CX 2000",
    "capacity": 3,
    "vehicleType": "car",
    "color": "white"
  }
}
```
### 2. Captain Login  
**POST** `/captains/login`

Authenticates a captain using email and password credentials.

**Request Body (JSON):->response gives token**
```json
{
  "email": "captain@gmail.com",
  "password": "test_captain"
}
```
---
### 3. Get Captain Profile  
**GET** `/captains/profile`

Retrieves the authenticated captain's profile information.
**Authentication:** Required (Bearer Token)
**Headers:**
```
Authorization: Bearer <token>
```
Response is token
**Response Body:**
---

### 4. Captain Logout  
**GET** `/captains/logout`

Logs out the authenticated captain by invalidating their token.

**Authentication:** Required (Bearer Token)
**Headers:**
```
Authorization: Bearer <token>
```
**Response Body:**
```json
{
  "message": "Logout successfully"
}
---


