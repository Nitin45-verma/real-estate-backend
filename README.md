# 🏠 Nitin Real Estate — Backend

A robust, scalable RESTful API server powering the Nitin Real Estate platform. Built with **Express.js** and **MongoDB**, featuring JWT authentication, Google OAuth, real-time chat via Socket.IO, Razorpay payment integration, AI-powered assistance, and a full admin management system.

---

## ✨ Features

- **RESTful API:** Clean, modular route structure for properties, bookings, leads, inquiries, and more.
- **JWT Authentication:** Secure token-based user authentication with bcrypt password hashing.
- **Google OAuth 2.0:** Server-side verification of Google Sign-In tokens.
- **Admin Panel API:** Full CRUD operations for managing properties, users, leads, bookings, and contacts.
- **Real-Time Chat:** Socket.IO powered buyer-seller messaging with room-based architecture.
- **Razorpay Payments:** Payment order creation and verification for property bookings.
- **AI Chat (Gemini):** Google Generative AI integration for intelligent property assistance.
- **Email Notifications:** Nodemailer-based SMTP email service for alerts and confirmations.
- **File Uploads:** Multer-based image/document upload handling with persistent storage.
- **Health Checks:** Built-in `/ping` and `/health` endpoints for uptime monitoring.
- **Auto Admin Setup:** Automatic admin user creation on first server boot.
- **CORS Configuration:** Flexible cross-origin setup for multi-environment deployments.
- **Compression:** Gzip response compression for optimized API performance.

---

## 🛠️ Tech Stack

| Category          | Technology                                      |
| ----------------- | ----------------------------------------------- |
| **Runtime**       | Node.js 18+                                     |
| **Framework**     | Express.js v5                                   |
| **Database**      | MongoDB (Mongoose ODM v9)                       |
| **Auth**          | JWT + bcryptjs + Google Auth Library             |
| **Real-Time**     | Socket.IO v4                                    |
| **Payments**      | Razorpay Node SDK                               |
| **AI**            | Google Generative AI (Gemini)                    |
| **Email**         | Nodemailer (SMTP)                               |
| **File Upload**   | Multer                                          |
| **Deployment**    | Render / Docker / AWS EC2                        |

---

## 📁 Project Structure

```
backend/
├── controllers/
│   └── authController.js    # Authentication logic (register, login, Google OAuth)
├── middleware/
│   ├── authMiddleware.js    # JWT token verification middleware
│   └── adminMiddleware.js   # Admin role authorization middleware
├── models/
│   ├── User.js              # User schema (name, email, password, role)
│   ├── Property.js          # Property listing schema
│   ├── Booking.js           # Visit booking schema
│   ├── Lead.js              # Sales lead schema
│   ├── Inquiry.js           # Property inquiry schema
│   ├── Contact.js           # Contact form submission schema
│   ├── Message.js           # Chat message schema
│   └── Transaction.js       # Payment transaction schema
├── routes/
│   ├── auth.js              # /api/auth — Register, Login, Google Sign-In
│   ├── properties.js        # /api/properties — CRUD property listings
│   ├── bookings.js          # /api/bookings — Visit booking management
│   ├── leads.js             # /api/leads — Lead tracking & management
│   ├── inquiries.js         # /api/inquiries — Property inquiries
│   ├── contacts.js          # /api/contact — Contact form submissions
│   ├── payment.js           # /api/payment — Razorpay order & verification
│   ├── chat.js              # /api/chat — Chat history & AI responses
│   └── admin.js             # /api/admin — Admin dashboard operations
├── utils/
│   └── emailService.js      # SMTP email sending utility
├── uploads/                 # Uploaded files storage directory
├── public/                  # Static files (admin.html)
├── server.js                # Main entry point — Express app + Socket.IO
├── seedProperties.js        # Database seeder script for sample properties
├── .env.example             # Environment variable template
├── Dockerfile               # Docker container configuration
├── docker-compose.yml       # Local Docker Compose (with MongoDB)
├── package.json             # Dependencies & scripts
└── README.md                # This file
```

---

## 🚀 Getting Started

### 1. Prerequisites

Ensure you have the following installed on your machine:

- **Node.js** v18+ → [Download](https://nodejs.org/)
- **npm** v9+ (comes with Node.js)
- **MongoDB** (local) or a **MongoDB Atlas** account → [Atlas](https://www.mongodb.com/atlas)

### 2. Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/Nitin45-verma/Nitin-Real-State.git
cd Nitin-Real-State/backend
npm install
```

### 3. Environment Setup

Create a `.env` file in the `backend/` directory using the template:

```bash
cp .env.example .env
```

Update the following variables:

```env
# Server Configuration
PORT=5000
BACKEND_URL=http://localhost:5000
FRONTEND_URL=http://localhost:5173

# MongoDB Database URI
MONGO_URI=mongodb://127.0.0.1:27017/nitin-real-estate

# JWT Authentication Secret
JWT_SECRET=your_secure_jwt_secret_key_here

# System Admin Credentials
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=your_secure_admin_password

# SMTP Email Configuration
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_gmail_app_password

# Google OAuth Client ID
GOOGLE_CLIENT_ID=your_google_oauth_client_id.apps.googleusercontent.com

# Razorpay Configuration
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret

# Gemini AI API Key
GEMINI_API_KEY=your_gemini_api_key_here
```

### 4. Run Development Server

```bash
npm run dev
```

The server will start at **http://localhost:5000** with Nodemon auto-restart on file changes.

### 5. Run Production Server

```bash
npm start
```

### 6. Seed Sample Data (Optional)

Populate the database with sample property listings:

```bash
node seedProperties.js
```

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint                  | Description               |
| ------ | ------------------------- | ------------------------- |
| POST   | `/api/auth/register`      | Register a new user       |
| POST   | `/api/auth/login`         | Login with email/password |
| POST   | `/api/auth/google`        | Google OAuth sign-in      |

### Properties
| Method | Endpoint                  | Description                  |
| ------ | ------------------------- | ---------------------------- |
| GET    | `/api/properties`         | List all properties          |
| GET    | `/api/properties/:id`     | Get property details         |
| POST   | `/api/properties`         | Create a new property        |
| PUT    | `/api/properties/:id`     | Update a property            |
| DELETE | `/api/properties/:id`     | Delete a property            |

### Bookings
| Method | Endpoint                  | Description                  |
| ------ | ------------------------- | ---------------------------- |
| GET    | `/api/bookings`           | List all bookings            |
| POST   | `/api/bookings`           | Create a new booking         |

### Leads
| Method | Endpoint                  | Description                  |
| ------ | ------------------------- | ---------------------------- |
| GET    | `/api/leads`              | List all leads               |
| POST   | `/api/leads`              | Create a new lead            |

### Payments
| Method | Endpoint                      | Description                  |
| ------ | ----------------------------- | ---------------------------- |
| POST   | `/api/payment/create-order`   | Create Razorpay order        |
| POST   | `/api/payment/verify`         | Verify payment signature     |

### Chat
| Method | Endpoint                  | Description                  |
| ------ | ------------------------- | ---------------------------- |
| GET    | `/api/chat/messages`      | Get chat message history     |
| POST   | `/api/chat/ai`            | AI-powered chat response     |

### Admin
| Method | Endpoint                  | Description                  |
| ------ | ------------------------- | ---------------------------- |
| GET    | `/api/admin/dashboard`    | Dashboard stats & analytics  |
| GET    | `/api/admin/users`        | List all users               |
| GET    | `/api/admin/properties`   | List all properties (admin)  |

### Health
| Method | Endpoint                      | Description              |
| ------ | ----------------------------- | ------------------------ |
| GET    | `/ping` `/health`             | Server health check      |
| GET    | `/api/ping` `/api/health`     | API health check         |
| GET    | `/api/test`                   | API test endpoint        |

---

## 🐳 Docker Deployment

### Standalone

```bash
docker build -t nitin-realestate-backend .
docker run -p 5000:5000 --env-file .env nitin-realestate-backend
```

### With Docker Compose (includes MongoDB)

```bash
docker-compose up --build
```

This spins up:
- **Backend** on port `5000`
- **MongoDB 7** on port `27017` with persistent volume

### Full Stack (from project root)

```bash
cd ..
docker-compose up --build
```

Starts frontend (port 80), backend (port 5000), and MongoDB (port 27017).

---

## ☁️ Cloud Deployment

### Render

1. Connect your GitHub repository to [Render](https://render.com).
2. Create a new **Web Service** pointing to the `backend/` directory.
3. Set **Build Command** to `npm install` and **Start Command** to `npm start`.
4. Add all environment variables from `.env.example` in Render's dashboard.
5. Deploy.

### AWS EC2

1. SSH into your EC2 instance.
2. Clone the repo and install dependencies.
3. Set up environment variables.
4. Use **PM2** or **systemd** to keep the server running:
   ```bash
   npx pm2 start server.js --name nitin-backend
   ```

---

## 🔌 WebSocket Events

The server uses Socket.IO for real-time communication:

| Event             | Direction       | Description                                  |
| ----------------- | --------------- | -------------------------------------------- |
| `join_room`       | Client → Server | Join a chat room (property + buyer + seller)  |
| `send_message`    | Client → Server | Send a chat message                          |
| `receive_message` | Server → Client | Broadcast received message to room members   |

---

## 📜 Available Scripts

| Command         | Description                                  |
| --------------- | -------------------------------------------- |
| `npm start`     | Start production server (`node server.js`)   |
| `npm run dev`   | Start dev server with Nodemon auto-reload    |

---

## 🔗 Related

- **Frontend:** See [`../frontend/README.md`](../frontend/README.md) for the React web app documentation.
- **Live API:** [real-state-backend-g6nt.onrender.com](https://real-state-backend-g6nt.onrender.com)
- **Live Demo:** [nitin-real-state.vercel.app](https://nitin-real-state.vercel.app)

---

## 📄 License

This project is open source and available under the [ISC License](../LICENSE).
