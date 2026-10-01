# Full-Stack Fiverr Freelance Marketplace Clone

A modern, full-stack freelance service marketplace application inspired by Fiverr. Built with a **React + Vite** frontend and an **Express + Node.js + MongoDB** backend, featuring authentication, gig creation, category filtering, interactive messaging, review management, and Stripe payment integration.

---

## Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
  - [Client (Frontend)](#client-frontend)
  - [API (Backend)](#api-backend)
- [Key Features](#key-features)
- [Project Architecture & Structure](#project-architecture--structure)
- [Environment Variables Setup](#environment-variables-setup)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Backend Setup (`/api`)](#backend-setup-api)
  - [Frontend Setup (`/client`)](#frontend-setup-client)
- [API Endpoints Reference](#api-endpoints-reference)

---

## Overview

This project consists of two decoupled sub-applications:
1. **`api`**: RESTful API service managing users, gigs, reviews, orders, real-time-like conversations, messages, and Stripe payment intents.
2. **`client`**: Responsive Single Page Application (SPA) providing an intuitive UI for buyers and sellers to discover services, message each other, place orders, and manage gigs.

---

## Tech Stack

### Client (Frontend)
- **Framework**: [React 18](https://react.dev/) + [Vite](https://vitejs.dev/)
- **Styling**: SCSS (Sass)
- **State Management & Data Fetching**: [@tanstack/react-query](https://tanstack.com/query/latest) & [Axios](https://axios-http.com/)
- **Routing**: [React Router v6](https://reactrouter.com/)
- **Payment Processing**: [@stripe/react-stripe-js](https://stripe.com/docs/stripe-js/react) & [@stripe/stripe-js](https://stripe.com/docs/js)
- **Carousels & UI**: `infinite-react-carousel`, `moment`
- **Asset Uploads**: Cloudinary REST API integration

### API (Backend)
- **Runtime**: [Node.js](https://nodejs.org/) (ES Modules)
- **Framework**: [Express 4](https://expressjs.com/)
- **Database**: [MongoDB](https://www.mongodb.com/) via [Mongoose 6](https://mongoosejs.com/)
- **Authentication**: JWT (JSON Web Tokens) with `httpOnly` secure cookies & `bcrypt` password hashing
- **Payments**: Stripe API SDK (`stripe`)
- **Development Tooling**: Nodemon, Dotenv, CORS, Cookie-Parser

---

## Key Features

- **Authentication & Roles**:
  - Secure registration and login with encrypted passwords.
  - Distinguishes between standard buyers and seller accounts (`isSeller`).
  - JWT tokens stored in `httpOnly` cookies for XSS mitigation.
- **Gigs & Marketplace**:
  - Browse gigs categorized by design, development, marketing, etc.
  - Filter and sort by budget (`min`, `max`), category (`cat`), search terms, and sort orders (`createdAt`, `sales`).
  - Sellers can add, view, and delete their own service offerings.
- **Reviews & Rating System**:
  - Buyers can submit 1–5 star reviews with comments on specific gigs.
  - Aggregated ratings automatically calculate total stars and star averages.
- **Orders & Stripe Payments**:
  - End-to-end checkout flow using Stripe PaymentIntents and Stripe Elements.
  - Order verification and confirmation upon payment completion.
- **Messaging System**:
  - Direct 1-on-1 conversations between buyer and seller per gig.
  - Message exchange thread with read/unread tracking.
- **Media Upload**:
  - Direct image and portfolio uploads using Cloudinary.

---

## Project Architecture & Structure

```text
youtube23-1/
├── api/                             # Backend Express API
│   ├── controllers/                 # Route handler functions
│   │   ├── auth.controller.js       # Register, login, logout
│   │   ├── conversation.controller.js
│   │   ├── gig.controller.js        # Gig CRUD and filtering
│   │   ├── message.controller.js    # Send and read messages
│   │   ├── order.controller.js      # Stripe payment intent & orders
│   │   ├── review.controller.js     # Gig reviews
│   │   └── user.controller.js       # User profile actions
│   ├── middleware/
│   │   └── jwt.js                   # JWT authentication guard
│   ├── models/                      # Mongoose data schemas
│   │   ├── conversation.model.js
│   │   ├── gig.model.js
│   │   ├── message.model.js
│   │   ├── order.model.js
│   │   ├── review.model.js
│   │   └── user.model.js
│   ├── routes/                      # API endpoint definitions
│   ├── utils/                       # Error handling helper
│   ├── .env                         # Backend environment variables
│   ├── package.json
│   └── server.js                    # Express entry point & DB connect
│
└── client/                          # Frontend React + Vite application
    ├── public/                      # Static icons and image assets
    ├── src/
    │   ├── components/              # Reusable UI components
    │   │   ├── catCard/             # Category carousel cards
    │   │   ├── checkoutForm/        # Stripe payment element
    │   │   ├── featured/            # Hero section with search
    │   │   ├── footer/
    │   │   ├── gigCard/             # Gig preview card
    │   │   ├── navbar/              # Sticky navbar with auth state
    │   │   ├── projectCard/
    │   │   ├── review/              # Single review card
    │   │   ├── reviews/             # Review list & submission form
    │   │   ├── slide/               # Infinite carousel wrapper
    │   │   └── trustedBy/
    │   ├── pages/                   # Application views
    │   │   ├── add/                 # Create new gig (Sellers only)
    │   │   ├── gig/                 # Gig detail & pricing view
    │   │   ├── gigs/                # Search/filter marketplace page
    │   │   ├── home/                # Landing page
    │   │   ├── login/
    │   │   ├── message/             # Active chat thread view
    │   │   ├── messages/            # Inbox conversations list
    │   │   ├── myGigs/              # Seller gig management
    │   │   ├── orders/              # User orders list
    │   │   ├── pay/                 # Stripe checkout container
    │   │   ├── register/
    │   │   └── success/             # Stripe redirect confirmation
    │   ├── reducers/
    │   │   └── gigReducer.js        # State reducer for adding new gigs
    │   ├── utils/
    │   │   ├── getCurrentUser.js    # LocalStorage user helper
    │   │   ├── newRequest.js        # Axios instance with credentials
    │   │   └── upload.js            # Cloudinary upload utility
    │   ├── App.jsx                  # React Router configuration
    │   ├── main.jsx                 # Vite root bootstrap
    │   └── app.scss                 # Global style definitions
    ├── .env                         # Frontend environment variables
    ├── index.html
    ├── package.json
    └── vite.config.js
```

---

## Environment Variables Setup

### 1. Backend (`/api/.env`)
Create or edit `api/.env`:
```env
PORT=8800
MONGO=your_mongodb_connection_string
JWT_KEY=your_secure_jwt_secret_key
STRIPE=sk_test_your_stripe_secret_key
```

### 2. Frontend (`/client/.env`)
Create or edit `client/.env`:
```env
VITE_UPLOAD_LINK=https://api.cloudinary.com/v1_1/<your_cloudinary_cloud_name>/image/upload
```

---

## Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v16+ or v18+ recommended)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- A running [MongoDB](https://www.mongodb.com/) instance (local or Atlas)
- A [Stripe](https://stripe.com/) account for test payment keys
- A [Cloudinary](https://cloudinary.com/) account for image storage

---

### Backend Setup (`/api`)

1. Open a terminal and navigate to the `api` folder:
   ```bash
   cd api
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Configure your `.env` file as shown above.
4. Start the backend development server:
   ```bash
   npm start
   ```
   *The server runs by default on `http://localhost:8800`.*

---

### Frontend Setup (`/client`)

1. Open a separate terminal and navigate to the `client` folder:
   ```bash
   cd client
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Configure your `.env` file with your Cloudinary upload URL.
4. Start the Vite development server:
   ```bash
   npm run dev
   ```
5. Open your browser and visit `http://localhost:5173` (or the URL displayed by Vite).

---

## API Endpoints Reference

| Module | Method | Endpoint | Description | Auth Required |
|---|---|---|---|---|
| **Auth** | `POST` | `/api/auth/register` | Register a new user | No |
| **Auth** | `POST` | `/api/auth/login` | Log in and receive JWT cookie | No |
| **Auth** | `POST` | `/api/auth/logout` | Clear auth cookie | Yes |
| **Users** | `DELETE`| `/api/users/:id` | Delete account | Yes |
| **Users** | `GET` | `/api/users/:id` | Get user details | Yes |
| **Gigs** | `POST` | `/api/gigs` | Create a new gig | Yes (Seller) |
| **Gigs** | `DELETE`| `/api/gigs/:id` | Delete seller's gig | Yes (Seller) |
| **Gigs** | `GET` | `/api/gigs/single/:id`| Fetch gig details | No |
| **Gigs** | `GET` | `/api/gigs` | Search & filter gigs | No |
| **Reviews**| `POST` | `/api/reviews` | Post a review | Yes |
| **Reviews**| `GET` | `/api/reviews/:gigId` | Get all reviews for a gig | No |
| **Orders** | `GET` | `/api/orders` | Fetch orders for user | Yes |
| **Orders** | `POST` | `/api/orders/create-payment-intent/:id` | Initialize Stripe Payment Intent | Yes |
| **Orders** | `PUT` | `/api/orders` | Confirm order upon payment | Yes |
| **Conversations** | `GET` | `/api/conversations` | Get user conversations | Yes |
| **Conversations** | `POST`| `/api/conversations` | Start a new conversation | Yes |
| **Conversations** | `GET` | `/api/conversations/single/:id` | Get single conversation | Yes |
| **Conversations** | `PUT` | `/api/conversations/:id` | Mark conversation as read | Yes |
| **Messages** | `POST` | `/api/messages` | Send message in conversation | Yes |
| **Messages** | `GET` | `/api/messages/:id` | Get messages in conversation | Yes |
