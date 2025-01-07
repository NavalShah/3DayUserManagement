# User Management System

## **Overview**

This project is a basic **User Management System** built using **Node.js**, **Express.js**, and **MongoDB**, featuring JWT-based authentication. It allows users to register, log in, and view their profiles. Sensitive information is securely stored using environment variables. The project implements basic CRUD operations and follows a modular structure for scalability and maintainability.

---

## **Features**

### **1. User Registration**

- **Endpoint**: `POST /api/users/register`
- Allows new users to register with their name, email, and password.
- Passwords are hashed using `bcryptjs` before being stored in the database.
- Ensures unique email validation to prevent duplicate accounts.
- Returns a JWT token upon successful registration.

### **2. User Login**

- **Endpoint**: `POST /api/users/login`
- Authenticates users by verifying their email and password.
- Generates a JWT token for secure, stateless authentication.
- Returns user details and a JWT token upon successful login.

### **3. View Profile**

- **Endpoint**: `GET /api/users/profile`
- A protected route that requires a valid JWT token in the `Authorization` header.
- Retrieves the authenticated user's profile information (ID, name, and email).

### **4. Security**

- Sensitive information, such as the MongoDB URI and JWT secret, is stored in a `.env` file.
- Passwords are hashed using `bcryptjs`.
- Authentication is implemented using JWT tokens, which are verified before granting access to protected routes.

---

## **File Structure**

user-management ├── /routes │ └── userRoutes.js # API endpoints (register, login, profile) ├── /models │ └── User.js # User schema and model ├── /utils │ └── getSecrets.js # Placeholder for fetching AWS Secrets (if needed) ├── server.js # Main application entry point ├── package.json # Project dependencies and scripts ├── .env # Environment variables (e.g., MongoDB URI, JWT secret)

---

## **Testing the Web Server**

1. Start the server locally using:

   ```bash
   node server.js

   ```

2. Use Postman or Curl to test the API endpoints.

---

## Testing API Endpoints

### Register

Endpoint: POST /api/users/register

Request Body

    {
        "name": "John Doe",
        "email": "john@example.com",
        "password": "password123"
    }

Expected Response

```bash
{
"\_id": "user_id",
"name": "John Doe",
"email": "john@example.com",
"token": "jwt_token"
}
```

Edge Cases:
Registering with an existing email should return a 400 Bad Request error.
Missing or invalid fields should return appropriate validation errors.

### User Login

POST /api/users/login
Allows an existing user to log in by verifying their email and password.

```
{
"email": "john@example.com",
"password": "password123"
}
```

Expected Reponse

```
{
  "_id": "user_id",
  "name": "John Doe",
  "email": "john@example.com",
  "token": "jwt_token"
}
```

Edge Cases: Incorrect Password, Output: "message": "Invalid credentials"

### View Profile

GET /api/users/profile
Retrieves the authenticated user's profile information. Requires a valid JWT toke

```
Authorization: Bearer <jwt_token>

```

Expected Response

```
{
  "_id": "user_id",
  "name": "John Doe",
  "email": "john@example.com"
}

```

Edge Cases: Missing Token, Output: "message": "Not authorized, no token"

I used Postman to test out each new request for individual endpoints

Results
Successfully registered users with valid inputs.
Blocked duplicate user registrations and invalid input.
Successfully authenticated users with valid credentials.
Prevented login attempts with incorrect passwords or non-existent accounts.
Restricted access to the profile route for unauthorized users.
Allowed access only to users with a valid JWT token.

Tech Stack

Backend: Node.js, Express.js <br/>
Database: MongoDB (with Mongoose ODM)<br/>
Authentication: JSON Web Tokens (JWT)<br/>
Environment Management: dotenv<br/>
Tools: Postman, MongoDB Compass<br/>

## How to Run

1. Clone the repo

2. Install dependencies

```bash
npm install
```

3. Create a .env file in the root directory with the following

```bash
MONGO_URI=mongodb://localhost:27017/userManagement
JWT_SECRET=your_jwt_secret_key

```

4. Start the server

```
node server.js
```

5. Use Postman to test the API at http://localhost:5000.
