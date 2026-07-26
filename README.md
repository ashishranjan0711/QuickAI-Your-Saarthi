# QuickAI-Your Saarthi — Full Stack AI SaaS App

QuickAI is a full-stack AI-powered SaaS application built with the **PERN stack** (PostgreSQL, Express, React, Node.js). It offers a suite of AI tools behind a subscription-based access model, letting users generate content, process images, and analyze documents through a clean, responsive dashboard.

## ✨ Features

- 🔐 **Authentication & Billing** — User sign up, login, and subscription management via [Clerk](https://clerk.com/)
- ✍️ **Article Generator** — AI-generated long-form articles from a prompt
- 📝 **Blog Title Generator** — Quick AI-generated blog title suggestions
- 🖼️ **AI Image Generation** — Generate images from text prompts
- 🧹 **Background Remover** — Remove image backgrounds automatically
- ✂️ **Object Remover** — Remove unwanted objects from images
- 📄 **Resume Analyzer** — AI-powered resume review and feedback
- 🌐 **Community Page** — Browse and explore content published by other users
- 💳 **Subscription Plans** — Usage limits and premium features gated behind billing tiers
- 📱 **Responsive UI** — Works seamlessly across desktop and mobile

## 🛠️ Tech Stack

**Frontend**
- React (Vite)
- Tailwind CSS

**Backend**
- Node.js + Express
- PostgreSQL (hosted via [Neon](https://neon.tech/))
- Clerk (`@clerk/express`) — authentication, middleware & billing
- Google Gemini API — AI content generation
- Cloudinary — image storage & processing

**Deployment**
- Vercel / VPS (frontend & backend deployed separately)

## 📁 Project Structure

```
quickai/
├── client/                 # React frontend (Vite)
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── pages/
│   │   └── App.jsx
│   ├── .env
│   ├── vite.config.js
│   └── vercel.json
│
├── server/                 # Express backend
│   ├── configs/            # DB, Cloudinary, and other service configs
│   ├── controllers/        # Route handler logic (AI tools, user features)
│   ├── middlewares/        # Auth & other Express middleware
│   ├── routes/             # API route definitions
│   ├── .env
│   ├── server.js            # Express app entry point
│   └── vercel.json
│
└── README.md
```

## 🔑 Environment Variables

### `server/.env`

```env
PORT=3000
# Database
DATABASE_URL=your_neon_database_url

# Clerk Authentication
CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key

# AI APIs
GEMINI_API_KEY=your_gemini_api_key

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
```

### `client/.env`

```env
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
VITE_BASE_URL=your_backend_url
```

> ⚠️ Never commit `.env` files to version control. Make sure they're listed in `.gitignore`.

## 🗄️ Database Schema

```sql
CREATE TABLE creations (
    id SERIAL PRIMARY KEY,
    user_id VARCHAR(255) NOT NULL,
    prompt TEXT NOT NULL,
    content TEXT NOT NULL,
    type VARCHAR(50) NOT NULL,
    publish BOOLEAN DEFAULT FALSE,
    likes TEXT[] DEFAULT '{}',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v18+ recommended)
- A Neon (PostgreSQL) database
- Clerk account (for authentication & billing keys)
- Google Gemini API key
- Cloudinary account (for image upload/processing keys)

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd quickai
```

### 2. Set up the backend
```bash
cd server
npm install
# add your environment variables to a .env file (see above)
# run the SQL above against your Neon database to create the `creations` table
npm run dev
```
The server runs on `http://localhost:3000` by default.

### 3. Set up the frontend
```bash
cd client
npm install
# add your environment variables to a .env file (see above)
npm run dev
```
The client runs on `http://localhost:5173` by default (Vite's default port).

## ☁️ Deployment

**Server** — deploy as a Node/Express app (Vercel serverless or a VPS):
- If deploying to Vercel, make sure `server.js` exports the Express app (`export default app`) so it can be wrapped as a serverless function, and set the **Root Directory** to `server`.
- Add all backend environment variables under **Project Settings → Environment Variables**.

**Client** — deployed as a standard Vite/React static build, with `VITE_BASE_URL` pointing to the deployed server URL.

## 📚 API Overview

| Route              | Description                                  |
|---------------------|-----------------------------------------------|
| `/api/user`         | User account, subscription & usage operations |
| `/api/ai`           | Article, blog title, image & resume AI tools  |
| `/api/community`    | Fetch and interact with published creations   |

## 📄 License

This project is for educational purposes. Feel free to fork and customize it for your own learning.
