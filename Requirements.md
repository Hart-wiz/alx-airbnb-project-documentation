# **technical and functional Requirement specifications** for :

- **i. User Authentication**
- **ii. Property Management**
- **iii. Booking System**

  **ALX Airbnb clone project**:

---

## ✅ 1. **User Authentication**

### 🔧 **Functional Requirements**

- Allow users to register with email and password.
- Allow users to log in and receive an access token.
- Passwords must be securely hashed.
- Token-based authentication using JWT.

### 🌐 **API Endpoints**

#### `POST /api/v1/auth/register`

- **Description**: Register a new user.
- **Input (JSON)**:

```json
{
  "username": "wizzy",
  "email": "wizzy@mail.com",
  "password": "StrongPass@123"
}
```

- **Validation Rules**:

  - Email must be valid and unique.
  - Password must be at least 8 characters.

- **Output**:

```json
{
  "message": "User registered successfully",
  "token": "<jwt_token>"
}
```

#### `POST /api/v1/auth/login`

- **Description**: Authenticate existing user and return token.
- **Input (JSON)**:

```json
{
  "email": "wizzy@mail.com",
  "password": "StrongPass@123"
}
```

- **Validation Rules**:

  - Email and password must match existing user.

- **Output**:

```json
{
  "message": "Login successful",
  "token": "<jwt_token>"
}
```

### ⚙️ **Performance Criteria**

- Response time < 500ms.
- Token expiration set (e.g., 1 hour).
- Rate limiting: Max 5 login attempts per minute.

---

## ✅ 2. **Property Management**

### 🔧 **Functional Requirements**

- Authenticated users can list properties.
- Properties can include title, description, price, location, and availability.
- Users can update or delete their properties.

### 🌐 **API Endpoints**

#### `POST /api/v1/properties`

- **Description**: Create a new property listing.
- **Input (JSON)**:

```json
{
  "title": "2-bedroom apartment",
  "description": "Spacious apartment in Lekki",
  "price": 100,
  "location": "Lagos",
  "availability": true
}
```

- **Validation Rules**:

  - Title and location are required.
  - Price must be a positive number.

- **Output**:

```json
{
  "message": "Property created",
  "propertyId": "123abc"
}
```

#### `GET /api/v1/properties`

- **Description**: Retrieve list of all available properties.
- **Output**:

```json
[
  {
    "id": "123abc",
    "title": "2-bedroom apartment",
    "location": "Lagos",
    "price": 100
  }
]
```

#### `PUT /api/v1/properties/:id`

- **Description**: Update a property (only owner).
- **Input**: Updated fields
- **Validation**: Only owner can update

### ⚙️ **Performance Criteria**

- Filter by location and price range.
- Paginate with max 20 results per page.
- Avg response time < 800ms.

---

## ✅ 3. **Booking System**

### 🔧 **Functional Requirements**

- Authenticated users can book a property.
- Bookings must not overlap.
- Booking details include check-in, check-out dates, and total cost.

### 🌐 **API Endpoints**

#### `POST /api/v1/bookings`

- **Description**: Book a property.
- **Input (JSON)**:

```json
{
  "propertyId": "123abc",
  "checkIn": "2025-06-01",
  "checkOut": "2025-06-05"
}
```

- **Validation Rules**:

  - Check-in < Check-out
  - Property must be available

- **Output**:

```json
{
  "message": "Booking confirmed",
  "bookingId": "b789xy"
}
```

#### `GET /api/v1/bookings/:userId`

- **Description**: Retrieve all bookings made by a user.

### ⚙️ **Performance Criteria**

- Conflict check must complete in < 200ms.
- Booking confirmation in < 700ms.
- Return up to 10 bookings per user page (pagination).

---
