# 🎪 EventPulse — Next-Gen Cybernetic Event Management & Ticketing System

EventPulse is a premium, full-stack Event Management and Ticketing Platform designed with a Web3-inspired cybernetic "Wallet Tech" aesthetic. Built using the **MERN Stack** (MongoDB, Express, React, Node.js), it features secure user authentication, email OTP verification, dynamic UPI payment processing with manual UTR verification, real-time ticket generation with custom QR codes, automated email receipts, and a powerful organizer administration panel.

> 🎓 **Internship Project Submission**  
> A production-ready, security-hardened event registration and ticketing portal built as a capstone internship project. 

---

## 🎨 Design & Aesthetic: Cybernetic Wallet Tech
The platform features an immersive, dark-mode design system with:
- **Deep Space Palette:** Rich space navy (`#040914`) and metallic dark blue (`#0A1128`) background layers.
- **Cybernetic Grids:** Low-opacity background grid lines and interactive radial neon glows.
- **Glassmorphism:** Sheer frosted cards with heavy backdrop blur (`24px`) and thin, high-contrast borders.
- **Premium Micro-interactions:** Pill-shaped buttons with glowing border overflows and smooth hardware-accelerated HMR hover states.

---

## ⚡ Core Features & Implementation Details

### 1. 🔐 Authentication & Email OTP Verification
- Secure signup/login system utilizing **bcryptjs** for credential hashing and **JWT** (JSON Web Tokens) for stateless sessions.
- Integrated **Nodemailer** with Gmail SMTP to trigger secure, high-delivery OTP emails during registration to verify user identity.

### 2. 💳 Smart UPI Payment Portal (UTR-Verified Gateway)
- Replaced traditional payment processors with a direct **UPI QR Code Gateway** configured to route funds to the organizer's UPI ID (`biraj7507@oksbi`).
- Generated scannable QR codes dynamically on checkout containing deep-linked merchant data.
- User submits the **12-digit UTR (Transaction Reference) Number** to place their booking in a `pending` state.
- **Security Hardening:** 
  - Prevents duplicate UTR submission (double-spending protection).
  - Restricts organizers from booking/purchasing tickets for their own events to prevent self-approval exploits.

### 3. 📊 Organizer & Manual Verification Dashboard
- Organizers get a dedicated verification portal showing all incoming booking requests, attendee details, and UTR numbers.
- One-click approval updates ticket status to `confirmed` and auto-increments event ticket sales metrics.
- Integrated **Recharts** dashboard showing detailed analytics on revenue, ticket sales distribution, check-in rates, and attendee count.

### 4. 📱 QR Code Ticket & Check-in System
- Upon verification, the system generates a secure, unique QR code for the attendee.
- Attendees can view their live tickets and scannable QR codes inside the **My Tickets** wallet.
- Organizers can scan the ticket QR code at the venue door via the `/checkin/:ticketId` API to instantly validate and log the check-in time.

### 5. ✉️ Automatic Email Receipts
- Once the organizer approves a ticket, an automated HTML email receipt is dispatched to the user, containing the ticket ID, confirmation status, pricing details, and instructions to download the QR code.

---

## 🛠️ Tech Stack & Architecture

### Frontend
- **React 18** (Vite-powered SPA)
- **React Router Dom v6** for client-side routing
- **Lucide React** for cybernetic icons
- **Recharts** for analytics and data visualization
- **React Hot Toast** for elegant toast notifications

### Backend
- **Node.js** & **Express** REST API
- **MongoDB** & **Mongoose** for data modeling
- **Nodemailer** for email delivery pipelines
- **QR Code** API generator for ticket rendering

---

## 🚀 Local Installation & Setup

### Prerequisites
- **Node.js** (v18+)
- **MongoDB** (Local instance or MongoDB Atlas Connection URI)

### 1. Backend Setup
1. Navigate to the server folder:
   ```bash
   cd server
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create a `.env` file inside `/server` with the following variables:
   ```env
   PORT=5000
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret_key
   JWT_EXPIRE=7d
   EMAIL_USER=your_gmail_username@gmail.com
   EMAIL_PASS=your_gmail_app_password
   ```
4. Seed the database with mock events:
   ```bash
   node seedEvents.js
   ```
5. Start the development server:
   ```bash
   npm run dev
   ```

### 2. Frontend Setup
1. Navigate to the client folder:
   ```bash
   cd client
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```
4. Access the portal at **http://localhost:5173**

---

## 🌍 Deployment Guide

### Deploying the Frontend (Vercel)
1. Push your project to a GitHub repository.
2. Go to **Vercel** and click **Add New Project**.
3. Import your GitHub repository.
4. Set the **Root Directory** to `client`.
5. Under **Build & Development Settings**, leave them as default (Vite settings).
6. Set Environment Variables (if any are used in the client, such as a backend API URL like `VITE_API_URL`).
7. Click **Deploy**.

### Deploying the Backend (Render / Railway)
1. Create a new service on **Render.com**.
2. Connect your GitHub repository.
3. Set the **Root Directory** to `server`.
4. Set the **Build Command** to `npm install`.
5. Set the **Start Command** to `npm start`.
6. Add your Environment Variables (`MONGODB_URI`, `JWT_SECRET`, `EMAIL_USER`, `EMAIL_PASS`, etc.) in the **Environment** settings.
7. Deploy the service and copy the live URL. Update your frontend's backend API endpoint config with this new URL.
