E-commerce Checkout System – Microservices (Proof of Concept)
Overview

This project is a microservices-based checkout system designed as part of a one-week challenge.
The goal was to break down a monolithic checkout process into smaller services, then implement a Cart Service with frontend integration.

Architecture
Services Implemented

Auth Service – Handles user sign-up, sign-in, and JWT token generation/verification.

Product Service – Manages the product catalog (fetch product list & details).

Cart Service – Manages cart items (add, edit, delete, view) and validates requests via Auth + Product.

Flow Example: Add to Cart

Frontend calls POST /add-to-cart with JWT token in headers and productId in body.

Cart Service → requests Auth Service to verify token & get user info.

Cart Service → requests Product Service for product details.

Cart Service → saves { userId, productId, quantity } into Cart DB.

Success response returned to frontend.


**Architecture DiagramProduct Service**


**1. Backend Setup (Services)Product Service**

Clone and run each service in a separate terminal:
npm install
npm run dev

Each service requires a .env file (see .env.example) with MongoDB connection string and service port.
e.g
**Auth Service**
PORT
MONGO_URI
JWT_SECRET_KEY
TOKEN_HEADER_KEY

**Product Service**
PORT
MONGO_URI

**Cart Service**
PORT
MONGO_URI

**Frontend Setup**
clone and run
npm install
npm run dev

**API Endpoints**
 Auth Service

POST /api/auth/register → Register new user

POST /api/auth/signin → Login user, returns JWT

GET /api/auth/verify-token → Verify token, return user info

Product Service

GET /api/ → Get all products

GET /products/:id → Get single product details

🛒 Cart Service

POST /add-to-cart

Headers: Authorization: Bearer <token>

Body: { "productId": "123", "quantity": 2 }

GET /get-cart/:userId

PUT /edit-cart/:itemId

DELETE /remove-from-cart/:itemId

