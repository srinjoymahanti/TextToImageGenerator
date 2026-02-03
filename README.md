# TextToImageGenerator

A full-stack text-to-image generator with user accounts, credits, and a React UI. The backend uses Express + MongoDB and integrates with the Clipdrop Text-to-Image API. The frontend is a Vite + React app that lets users log in, generate images from prompts, and manage credits.

## Features

- **User auth**: Register and log in with JWT-based sessions.
- **Image generation**: Send prompts to the Clipdrop API and return base64 image results.
- **Credits**: Track and decrement credits per generated image.
- **Responsive UI**: React + Tailwind CSS UI with toast notifications.

## Tech Stack

**Frontend**
- React 18, Vite, Tailwind CSS
- React Router, Axios, React Toastify

**Backend**
- Node.js, Express
- MongoDB + Mongoose
- JWT authentication
- Clipdrop Text-to-Image API

## Project Structure

```
.
├── client/         # React frontend (Vite)
└── server/         # Express API
```

## Getting Started

### Prerequisites

- Node.js 18+ (or newer)
- MongoDB connection string
- Clipdrop API key

### 1) Clone and install dependencies

```bash
# install server deps
cd server
npm install

# install client deps
cd ../client
npm install
```

### 2) Configure environment variables

Create a `.env` file in `server/`:

```bash
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
CLIPDROP_API=your_clipdrop_api_key
PORT=4000
```

Create a `.env` file in `client/`:

```bash
VITE_BACKEND_URL=http://localhost:4000
```

### 3) Run the app

In one terminal, start the server:

```bash
cd server
npm run server
```

In another terminal, start the client:

```bash
cd client
npm run dev
```

Open the app at the URL shown in the Vite output (usually `http://localhost:5173`).

## API Overview

Base URL: `http://localhost:4000`

- `POST /api/user/register` — Register a new user.
- `POST /api/user/login` — Log in and receive a JWT token.
- `GET /api/user/credits` — Get user credit balance (requires `token` header).
- `POST /api/image/generate-image` — Generate an image from a prompt (requires `token` header).

### Example request

```bash
curl -X POST http://localhost:4000/api/image/generate-image \
  -H "Content-Type: application/json" \
  -H "token: <JWT_TOKEN>" \
  -d '{"prompt": "A futuristic city at sunset"}'
```

## Notes

- The backend expects a valid JWT token in the `token` header for protected routes.
- Each image generation decrements the user's credit balance.
- The backend stores users in a MongoDB database named `imagify`.

## Scripts

**Client**
- `npm run dev` — Start Vite dev server
- `npm run build` — Build production assets
- `npm run preview` — Preview production build
- `npm run lint` — Lint frontend

**Server**
- `npm run server` — Start Express server

