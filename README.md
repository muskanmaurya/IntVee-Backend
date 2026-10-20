# ⚙️ AI-Powered Interview Intelligence Engine (Server API)

> **Frontend Client Repository:** [-Full-Stack-Gen-AI-Job-Preparation-Web-Application-Frontend](https://github.com/muskanmaurya/-Full-Stack-Gen-AI-Job-Preparation-Web-Application-Frontend)  
> **API Endpoint:** `https://full-stack-gen-ai-job-preparation-web.onrender.com`

---

## 🛠️ Service Overview

The backend engine powering the AI Interview Intelligence platform. Built with **Node.js**, **Express.js**, and **MongoDB**, this service handles binary document parsing, orchestrates Generative AI structured pipelines via the **Google GenAI SDK**, manages token blacklisting and user security, and runs headless browser automation with **Puppeteer** for PDF compilation.

---

## ⚡ Core Technical Capabilities

* **🤖 GenAI Integration & Structured Outputs:** Leverages Gemini AI (`gemini-2.5-flash`) enforced with Zod schemas (`zod-to-json-schema`) to guarantee strict JSON payloads for match scoring, technical/behavioral question mapping, and preparation plans.
* **📄 Headless PDF Compilation:** Implements Puppeteer browser automation to dynamically compile candidate resumes into ATS-optimized PDF documents. Features automated retries and Linux argument fallbacks for containerized environments.
* **📂 In-Memory PDF Parsing:** Uses `pdf-parse` and `multer.memoryStorage()` to extract raw text from candidate resume uploads without disk persistence.
* **🔐 Security & Authentication:** Implements JWT authentication stored in HTTP-Only, cross-domain cookies (`sameSite: "none", secure: true`), BCrypt password hashing, and token blacklisting for secure logouts.
* **👤 Guest Session State:** Supports stateless guest sessions via `x-guest-token` header interceptors paired with temporary runtime in-memory maps.

---

## 🔌 API Endpoints Summary

### Auth Routes (`/api/auth`)
* `POST /register` - User registration with hashed credentials.
* `POST /login` - User authentication issuing HTTP-only cookie.
* `GET /logout` - Invalidates JWT and adds to blacklist database.
* `GET /get-me` - Fetches active authenticated user session.

### Interview Routes (`/api/interview`)
* `POST /` - Accepts `multipart/form-data` (Resume PDF, Self-Description, Job Description) and returns AI Strategy report.
* `GET /` - Fetches all historical preparation reports for the authenticated user.
* `GET /report/:interviewId` - Fetches a specific interview report by ID.
* `POST /resume/pdf/:interviewReportId` - Generates and returns a downloadable ATS-friendly PDF resume stream.

---

## 🛠️ Backend Tech Stack

* **Runtime:** Node.js (ES Modules)
* **Framework:** Express.js
* **Database:** MongoDB / Mongoose ODM
* **AI & Validation:** Google GenAI SDK (`@google/genai`), Zod
* **PDF Engine:** Puppeteer (Chromium)
* **Authentication:** JSON Web Tokens (JWT), Bcryptjs, Cookie-Parser
* **File Processing:** Multer, pdf-parse
* **Deployment:** Render

---

## 🔧 Local Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/muskanmaurya/Full-Stack-Gen-AI-Job-Preparation-Web-Application-Backend.git
cd Full-Stack-Gen-AI-Job-Preparation-Web-Application-Backend
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory of the project:
```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET_KEY=your_jwt_secret
GOOGLE_GENAI_API_KEY=your_gemini_api_key
```

### 4. Start Server
```bash
npm run dev
```
