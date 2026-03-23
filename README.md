# 🏥 HealthCare Plus — MERN Stack Doctor Appointment App

A full-stack MERN (MongoDB, Express, React, Node.js) doctor appointment system with:

- Patient portal: book appointments, view medical history, AI chatbot
- Doctor portal: manage appointments, create medical records, prescriptions
- JWT authentication with role-based access (patient / doctor)
- Clean, modern UI built with React + Tailwind CSS

---

## 📁 Project Structure

```
mern-doctor-app/
├── backend/                     # Express + MongoDB API
│   ├── config/
│   │   └── db.js                # MongoDB connection utility
│   ├── controllers/
│   │   ├── authController.js    # Register, Login, GetMe
│   │   ├── appointmentController.js
│   │   ├── medicalRecordController.js
│   │   └── userController.js
│   ├── middleware/
│   │   └── authMiddleware.js    # JWT protect + role authorize
│   ├── models/
│   │   ├── User.js              # Patient & Doctor schema
│   │   ├── Appointment.js
│   │   └── MedicalRecord.js     # Includes Prescription sub-schema
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── appointmentRoutes.js
│   │   ├── medicalRecordRoutes.js
│   │   └── userRoutes.js
│   ├── .env.example             # ← Copy to .env and fill in values
│   ├── server.js                # Main entry point
│   └── package.json
│
└── frontend/                    # React + Vite + Tailwind
    ├── src/
    │   ├── components/
    │   │   ├── layout/
    │   │   │   ├── PatientLayout.jsx   # Sidebar shell for patients
    │   │   │   └── DoctorLayout.jsx    # Sidebar shell for doctors
    │   │   └── shared/
    │   │       ├── LoadingScreen.jsx
    │   │       ├── StatusBadge.jsx
    │   │       └── EmptyState.jsx
    │   ├── context/
    │   │   └── AuthContext.jsx         # Global auth state
    │   ├── pages/
    │   │   ├── auth/
    │   │   │   ├── LoginPage.jsx
    │   │   │   └── RegisterPage.jsx
    │   │   ├── patient/
    │   │   │   ├── PatientDashboard.jsx
    │   │   │   ├── BookAppointment.jsx
    │   │   │   ├── MedicalHistory.jsx
    │   │   │   └── Chatbot.jsx
    │   │   ├── doctor/
    │   │   │   ├── DoctorDashboard.jsx
    │   │   │   └── PatientRecords.jsx
    │   │   └── NotFound.jsx
    │   ├── services/
    │   │   └── api.js            # Axios instance with JWT interceptor
    │   ├── App.jsx               # Routes + auth guards
    │   ├── main.jsx
    │   └── index.css             # Tailwind + design tokens
    ├── index.html
    ├── vite.config.js
    ├── tailwind.config.js
    └── package.json
```

---

## 🚀 Getting Started

### 1. Clone / extract project

```bash
cd mern-doctor-app
```

### 2. Set up the Backend

```bash
cd backend
npm install

# Copy env example and fill in your values
cp .env.example .env
# Edit .env:
#   MONGO_URI=mongodb://localhost:27017/doctor_appointment_db
#   JWT_SECRET=your_strong_random_secret
#   CLIENT_URL=http://localhost:5173

npm run dev        # starts on http://localhost:5000
```

### 3. Set up the Frontend

```bash
cd frontend
npm install
npm run dev        # starts on http://localhost:5173
```

Open `http://localhost:5173` in your browser.

---

## 🔑 API Endpoints

### Auth
| Method | Route            | Access  | Description          |
|--------|------------------|---------|----------------------|
| POST   | /api/auth/register | Public | Register user        |
| POST   | /api/auth/login    | Public | Login & get token    |
| GET    | /api/auth/me       | Auth   | Get current user     |

### Appointments
| Method | Route                          | Access        | Description              |
|--------|--------------------------------|---------------|--------------------------|
| GET    | /api/appointments              | Auth          | Get my appointments      |
| POST   | /api/appointments              | Patient only  | Book appointment         |
| PATCH  | /api/appointments/:id/status   | Auth          | Update status            |
| DELETE | /api/appointments/:id          | Patient only  | Delete appointment       |

### Medical Records
| Method | Route                    | Access       | Description           |
|--------|--------------------------|--------------|-----------------------|
| GET    | /api/medical-records     | Auth         | Get records           |
| POST   | /api/medical-records     | Doctor only  | Create record         |
| GET    | /api/medical-records/:id | Auth         | Get single record     |
| PUT    | /api/medical-records/:id | Doctor only  | Update record         |

### Users
| Method | Route                    | Access       | Description           |
|--------|--------------------------|--------------|-----------------------|
| GET    | /api/users/doctors       | Public       | List all doctors      |
| GET    | /api/users/patients      | Doctor only  | List patients         |
| GET    | /api/users/profile       | Auth         | Get my profile        |
| PUT    | /api/users/profile       | Auth         | Update my profile     |
| PUT    | /api/users/change-password | Auth       | Change password       |

---

## 🔧 TODO / Where to Work

Search the codebase for `// TODO:` comments. Key areas:

| File | What to implement |
|------|-------------------|
| `backend/.env` | Fill in MONGO_URI, JWT_SECRET |
| `models/User.js` | Add profile image upload (Cloudinary/S3) |
| `appointmentController.js` | Add time-slot conflict detection |
| `authController.js` | Add refresh token support |
| `pages/patient/Chatbot.jsx` | Connect real AI API (OpenAI, Gemini, etc.) |
| `components/layout/PatientLayout.jsx` | Wire up real notifications |
| `pages/patient/MedicalHistory.jsx` | Add PDF download button |
| All pages | Add pagination for long lists |

---

## 🛠️ Tech Stack

**Backend:** Node.js, Express, MongoDB, Mongoose, JWT, bcryptjs  
**Frontend:** React 18, React Router v6, Axios, Tailwind CSS, Vite, react-hot-toast, lucide-react, date-fns
