# Backend API - Fiverr Clone

Backend REST API built with **Node.js**, **Express**, and **MongoDB (Mongoose)**, providing authentication, data persistence, and Stripe payment processing.

## Scripts

```bash
npm install     # Install dependencies
npm start       # Run server with nodemon
```

## Environment Variables (`.env`)

```env
PORT=8800
MONGO=mongodb+srv://<username>:<password>@<cluster>.mongodb.net
JWT_KEY=your_jwt_secret
STRIPE=sk_test_your_stripe_secret_key
```

## Features

- **Authentication**: JWT stored in `httpOnly` secure cookies. Password encryption with `bcrypt`.
- **Controllers & Routes**:
  - `auth`: `/api/auth` (register, login, logout)
  - `users`: `/api/users` (get, delete)
  - `gigs`: `/api/gigs` (CRUD, filter by category/price/search)
  - `reviews`: `/api/reviews` (create review, calculate average rating)
  - `orders`: `/api/orders` (Stripe payment intent creation & order status)
  - `conversations`: `/api/conversations` (chat channels between buyers & sellers)
  - `messages`: `/api/messages` (direct chat messaging)
