# Subscription Tracker API

A production-ready RESTful API for managing user subscriptions — built with Node.js, Express, and MongoDB. Handles real users, real money, and real business logic with JWT authentication, advanced rate limiting, automated email reminders, and a scalable, modular architecture.

## Tech Stack

- **Runtime:** Node.js with Express.js
- **Database:** MongoDB with Mongoose ODM
- **Authentication:** JSON Web Tokens (JWT)
- **Security:** Arcjet (rate limiting & bot protection)
- **Workflows:** Upstash (automated email reminders)
- **Linting:** ESLint

## Features

- **JWT Authentication** — Secure sign-up, sign-in, and token-based session management for all protected routes.
- **Database Modeling** — Mongoose schemas with validation, relationships, auto-calculated fields (e.g. renewal dates), and pre-save hooks.
- **Subscription CRUD** — Create, read, update, cancel, and delete subscriptions with per-user scoping and status tracking (active, cancelled, expired).
- **Advanced Rate Limiting & Bot Protection** — Arcjet integration to guard against abuse, brute-force attacks, and automated bots.
- **Automated Email Reminders** — Upstash workflow-driven reminders for upcoming subscription renewals.
- **Global Error Handling** — Centralized error middleware with consistent JSON error responses and input validation.
- **Logging** — Structured logging for debugging and monitoring in development and production.
- **Scalable Architecture** — Clean separation of concerns across controllers, models, routes, middlewares, and config.

## Project Structure

```
subscription-web-api/
├── config/          # Environment variables and service configuration (Arcjet, Upstash)
├── controllers/     # Route handler logic (auth, subscriptions)
├── database/        # MongoDB connection setup
├── middlewares/      # Auth middleware, error handling, Arcjet rate limiting
├── models/          # Mongoose schemas (User, Subscription)
├── routes/          # Express route definitions
├── utils/           # Helper utilities
├── app.js           # Application entry point
├── eslint.config.js # Linting configuration
└── package.json
```

## Getting Started

### Prerequisites

- Node.js (v18+)
- MongoDB instance (local or Atlas)
- Arcjet account (for rate limiting)
- Upstash account (for email workflows)

### Installation

```bash
git clone https://github.com/archerzou/subscription-web-api.git
cd subscription-web-api
npm install
```

### Environment Variables

Create a `.env.development.local` file in the root directory:

check env.example file

### Running the Server

```bash
# Development
npm run dev

# Production
npm start
```

## API Endpoints

### Authentication

| Method | Endpoint              | Description       | Auth |
|--------|-----------------------|-------------------|------|
| POST   | `/api/v1/auth/sign-up` | Register a user   | No   |
| POST   | `/api/v1/auth/sign-in` | Sign in a user    | No   |
| POST   | `/api/v1/auth/sign-out`| Sign out a user   | Yes  |

### Subscriptions

| Method | Endpoint                              | Description                  | Auth |
|--------|---------------------------------------|------------------------------|------|
| GET    | `/api/v1/subscriptions`               | Get all subscriptions        | No   |
| GET    | `/api/v1/subscriptions/:id`           | Get subscription by ID       | No   |
| POST   | `/api/v1/subscriptions`               | Create a subscription        | Yes  |
| PUT    | `/api/v1/subscriptions/:id`           | Update a subscription        | Yes  |
| DELETE | `/api/v1/subscriptions/:id`           | Delete a subscription        | Yes  |
| GET    | `/api/v1/subscriptions/user/:id`      | Get user's subscriptions     | Yes  |
| PUT    | `/api/v1/subscriptions/:id/cancel`    | Cancel a subscription        | Yes  |
| GET    | `/api/v1/subscriptions/upcoming-renewals` | Get upcoming renewals    | Yes  |

### Workflows

| Method | Endpoint                                          | Description               |
|--------|---------------------------------------------------|---------------------------|
| POST   | `/api/v1/workflows/subscription/reminder`         | Trigger renewal reminder  |


## License

This project is open source and available under the [MIT License](LICENSE).
