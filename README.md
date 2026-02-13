# 🏥 KidCare Chronicle — Child Immunization Tracker

> A comprehensive web application to digitally track, manage, and monitor children's vaccination records for parents and healthcare providers.

---

## 📋 Table of Contents

1. [Problem Statement](#-problem-statement)
2. [Project Description](#-project-description)
3. [Architecture Diagram](#-architecture-diagram)
4. [End-to-End Flow](#-end-to-end-flow)
5. [Features](#-features)
6. [Tech Stack](#-tech-stack)
7. [Project Structure](#-project-structure)
8. [Getting Started](#-getting-started)
9. [Firebase Configuration](#-firebase-configuration)
10. [Deployment](#-deployment)
11. [Screenshots](#-screenshots)
12. [Future Enhancements](#-future-enhancements)
13. [Contact](#-contact)

---

## ❓ Problem Statement

In many regions, child immunization records are maintained manually on paper-based cards, leading to:

- **Lost or damaged vaccination records** making it difficult to track immunization history
- **Missed vaccination schedules** due to lack of timely reminders
- **Inability to share records** easily with schools, hospitals, or during travel
- **No centralized system** for parents to manage multiple children's vaccination data
- **Healthcare providers lack real-time access** to a child's immunization status

**KidCare Chronicle** solves these problems by providing a **digital, cloud-based platform** that enables parents and healthcare professionals to track, manage, and share vaccination records seamlessly.

---

## 📝 Project Description

**KidCare Chronicle** is a full-stack web application built with **React + TypeScript** on the frontend and **Firebase** (Authentication, Firestore, Storage) on the backend. It provides role-based access for **Parents** and **Healthcare Providers (Doctors)** to manage children's immunization records digitally.

<h3>The public URL version of this project is <a href="https://immunization-tracker-966d8.web.app/">KidCare Chronicle</a> or scan the below QR and visit the site 
</h3>
<p align="center">
  <img width="248" height="248" alt="QR Code" src="https://github.com/user-attachments/assets/7467d12a-8150-4448-8a60-4b352c18c640" />
</p>

### Key Highlights:
- **Role-Based Access**: Parents manage their children; Doctors manage patients
- **Multi-Language Support**: English, Hindi, Telugu, Tamil, and Malayalam
- **QR Code Integration**: Generate and scan QR codes for quick record sharing
- **PDF Reports**: Download vaccination records as professional PDF documents
- **Real-Time Sync**: All data is synced in real-time via Firebase Firestore
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices

---

## 🏗 Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                      CLIENT (Browser)                   │
│  ┌───────────────────────────────────────────────────┐  │
│  │              React + TypeScript + Vite             │  │
│  │  ┌─────────┐ ┌──────────┐ ┌───────────────────┐  │  │
│  │  │  Pages   │ │Components│ │    Contexts        │  │  │
│  │  │Dashboard │ │ChildCard │ │ AuthContext        │  │  │
│  │  │Children  │ │AddChild  │ │ LanguageContext    │  │  │
│  │  │Vaccines  │ │EditChild │ │                    │  │  │
│  │  │Records   │ │QR/PDF    │ │                    │  │  │
│  │  │Education │ │VaccMenu  │ │                    │  │  │
│  │  │Profile   │ │LangToggle│ │                    │  │  │
│  │  └─────────┘ └──────────┘ └───────────────────┘  │  │
│  │                                                    │  │
│  │  ┌─────────────────────────────────────────────┐  │  │
│  │  │              Services Layer                  │  │  │
│  │  │  vaccinationService │ pdfService │ qrService │  │  │
│  │  │  otpService │ reportService                  │  │  │
│  │  └─────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────┘  │
└──────────────────────────┬──────────────────────────────┘
                           │ HTTPS / SDK
                           ▼
┌─────────────────────────────────────────────────────────┐
│                    FIREBASE BACKEND                      │
│  ┌──────────────┐ ┌──────────────┐ ┌─────────────────┐ │
│  │   Firebase    │ │  Cloud       │ │   Firebase      │ │
│  │   Auth        │ │  Firestore   │ │   Storage       │ │
│  │               │ │              │ │                  │ │
│  │ • Email/Pass  │ │ • users      │ │ • Profile Imgs  │ │
│  │ • Role-based  │ │ • children   │ │ • Documents     │ │
│  │   access      │ │ • vaccines   │ │                  │ │
│  │               │ │ • records    │ │                  │ │
│  └──────────────┘ └──────────────┘ └─────────────────┘ │
│                                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │              Firebase Hosting (Deployment)        │  │
│  │         immunization-tracker-966d8.web.app        │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

---

## 🔄 End-to-End Flow

```
┌──────────┐     ┌───────────┐     ┌──────────────┐     ┌──────────────┐
│  User     │────▶│  Auth     │────▶│  Role Check  │────▶│  Dashboard   │
│  Opens App│     │  Login/   │     │  Parent or   │     │  (Role-based)│
│           │     │  Signup   │     │  Doctor      │     │              │
└──────────┘     └───────────┘     └──────────────┘     └──────┬───────┘
                                                               │
                      ┌────────────────────────────────────────┘
                      │
          ┌───────────┼───────────────┬──────────────┬──────────────┐
          ▼           ▼               ▼              ▼              ▼
   ┌────────────┐ ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌──────────┐
   │  Manage    │ │ Track    │ │  View     │ │ Education│ │ Profile  │
   │  Children  │ │ Vaccines │ │  Records  │ │ Resources│ │ Settings │
   │            │ │          │ │           │ │          │ │          │
   │ • Add      │ │ • Status │ │ • History │ │ • Articles│ │ • Info  │
   │ • Edit     │ │ • Update │ │ • PDF     │ │ • Tips   │ │ • Lang  │
   │ • Delete   │ │ • Schedule│ │ • QR Code│ │ • FAQs   │ │ • Pass  │
   └────────────┘ └──────────┘ └───────────┘ └──────────┘ └──────────┘
                       │              │
                       ▼              ▼
               ┌──────────────────────────┐
               │   Generate & Share       │
               │  • PDF Download          │
               │  • QR Code Generation    │
               │  • QR Code Scanning      │
               └──────────────────────────┘
```

### Detailed User Flow:

1. **Authentication**: User signs up / logs in with email & password via Firebase Auth
2. **Role Selection**: User registers as either a **Parent** or **Doctor**
3. **Dashboard**: Role-specific dashboard displays relevant statistics and quick actions
4. **Child Management**: Parents add children with details (name, DOB, blood group, allergies)
5. **Vaccination Tracking**: Track vaccination status (Pending → Scheduled → Completed)
6. **Records & Reports**: View history, generate PDF reports, create/scan QR codes
7. **Multi-Language**: Switch interface language anytime via the language toggle
8. **Profile Management**: Update personal info, change password, set preferred language

---

## ✨ Features

### 👨‍👩‍👧 For Parents
| Feature | Description |
|---------|-------------|
| 📝 **Child Registration** | Add multiple children with complete health profiles |
| 💉 **Vaccination Tracking** | Monitor vaccination status with visual indicators |
| 📊 **Dashboard Analytics** | Overview of vaccination progress and upcoming schedules |
| 📄 **PDF Reports** | Download professional vaccination certificates |
| 📱 **QR Code Sharing** | Generate QR codes for instant record sharing |
| 🌐 **Multi-Language** | Switch between English, Hindi, Telugu, Tamil, Malayalam |
| 🔔 **Notifications** | Get reminders for upcoming vaccinations |

### 👨‍⚕️ For Healthcare Providers (Doctors)
| Feature | Description |
|---------|-------------|
| 🏥 **Patient Management** | View and manage assigned patients |
| 📋 **Vaccination Updates** | Update vaccination status for patients |
| 📊 **Reports Generation** | Generate detailed immunization reports |
| 🔍 **QR Scanner** | Scan patient QR codes for quick access |

### 🔧 General Features
| Feature | Description |
|---------|-------------|
| 🔐 **Secure Authentication** | Firebase Auth with email/password |
| 📱 **Responsive Design** | Fully responsive across all devices |
| 🎨 **Modern UI** | Built with shadcn/ui components |
| ⚡ **Real-Time Sync** | Firestore real-time data synchronization |
| 🔄 **OTP Verification** | Secure account verification |

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 18, TypeScript, Vite |
| **Styling** | Tailwind CSS, shadcn/ui, Lucide Icons |
| **State Management** | React Context API, TanStack React Query |
| **Routing** | React Router DOM v7 |
| **Authentication** | Firebase Authentication |
| **Database** | Cloud Firestore (NoSQL) |
| **File Storage** | Firebase Storage |
| **Hosting/Deployment** | Firebase Hosting |
| **PDF Generation** | jsPDF, jspdf-autotable |
| **QR Code** | qrcode (generation), qr-scanner (scanning) |
| **Form Handling** | React Hook Form, Zod validation |
| **Animations** | Tailwind CSS Animate |
| **Charts** | Recharts |

---

## 📁 Project Structure

```
kidcare-chronicle/
├── public/
│   ├── kidcare.png              # App logo
│   ├── placeholder.svg          # Placeholder image
│   └── robots.txt               # SEO robots file
├── src/
│   ├── assets/                  # Static assets (images)
│   ├── components/
│   │   ├── auth/                # Authentication components
│   │   │   ├── AuthLayout.tsx
│   │   │   ├── LoginForm.tsx
│   │   │   ├── SignupForm.tsx
│   │   │   ├── ChangePasswordDialog.tsx
│   │   │   └── OTPVerificationDialog.tsx
│   │   ├── children/            # Child management components
│   │   │   ├── AddChildDialog.tsx
│   │   │   ├── ChildCard.tsx
│   │   │   └── EditChildDialog.tsx
│   │   ├── common/              # Shared components
│   │   │   └── LanguageToggle.tsx
│   │   ├── dashboard/           # Dashboard layout
│   │   │   └── DashboardLayout.tsx
│   │   ├── layout/              # Layout components
│   │   │   └── Footer.tsx
│   │   ├── patient/             # Patient-related components
│   │   │   └── PatientDetailsModal.tsx
│   │   ├── profile/             # Profile components
│   │   │   └── UserProfileModal.tsx
│   │   ├── ui/                  # shadcn/ui components
│   │   └── vaccinations/        # Vaccination components
│   │       └── VaccinationStatusMenu.tsx
│   ├── contexts/                # React Context providers
│   │   ├── AuthContext.tsx       # Authentication state
│   │   └── LanguageContext.tsx   # Multi-language support
│   ├── hooks/                   # Custom React hooks
│   ├── lib/                     # Library configurations
│   │   ├── firebase.ts          # Firebase initialization
│   │   └── utils.ts             # Utility functions
│   ├── pages/                   # Route pages
│   │   ├── Auth.tsx
│   │   ├── Children.tsx
│   │   ├── Dashboard.tsx
│   │   ├── Education.tsx
│   │   ├── Index.tsx
│   │   ├── Profile.tsx
│   │   ├── Records.tsx
│   │   └── Vaccinations.tsx
│   ├── services/                # Business logic services
│   │   ├── otpService.ts
│   │   ├── pdfService.ts
│   │   ├── qrService.ts
│   │   ├── reportService.ts
│   │   └── vaccinationService.ts
│   ├── types/                   # TypeScript type definitions
│   │   └── index.ts
│   ├── App.tsx                  # Main app component
│   ├── App.css                  # Global styles
│   ├── index.css                # Tailwind directives
│   └── main.tsx                 # Entry point
├── firebase.json                # Firebase hosting config
├── .firebaserc                  # Firebase project config
├── tailwind.config.ts           # Tailwind configuration
├── vite.config.ts               # Vite configuration
├── tsconfig.json                # TypeScript configuration
└── package.json                 # Dependencies & scripts
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** (v18 or higher) — [Download](https://nodejs.org/)
- **npm** or **bun** (package manager)
- **Git** — [Download](https://git-scm.com/)
- **Firebase CLI** — Install globally:
  ```bash
  npm install -g firebase-tools
  ```

### Clone the Repository

```bash
# Clone the repo
git clone https://github.com/KowshikSuggala25/kidcare-chronicle.git

# Navigate to the project directory
cd kidcare-chronicle

# Install dependencies
npm install

# Start the development server
npm run dev
```

The app will be running at `http://localhost:5173`

---

## 🔥 Firebase Configuration

### 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add Project"** and follow the setup wizard
3. Enable **Google Analytics** (optional)

### 2. Enable Firebase Services

- **Authentication**: Go to Authentication → Sign-in method → Enable **Email/Password**
- **Firestore**: Go to Firestore Database → Create database → Start in **test mode**
- **Storage**: Go to Storage → Get started

### 3. Get Firebase Config

1. Go to Project Settings → General → Your apps → Web app
2. Copy the Firebase config object
3. Replace the config in `src/lib/firebase.ts`:

```typescript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### 4. Firestore Collections Structure

```
firestore/
├── users/                    # User profiles
│   └── {userId}/
│       ├── name: string
│       ├── email: string
│       ├── role: "parent" | "doctor"
│       ├── language: string
│       └── ...
├── children/                 # Children records
│   └── {childId}/
│       ├── name: string
│       ├── dateOfBirth: timestamp
│       ├── parentId: string
│       ├── bloodGroup: string
│       ├── allergies: string[]
│       └── ...
└── vaccinations/             # Vaccination records
    └── {vaccinationId}/
        ├── childId: string
        ├── vaccineName: string
        ├── status: "pending" | "scheduled" | "completed"
        ├── dateAdministered: timestamp
        └── ...
```

---

## 🚢 Deployment

This project is deployed on **Firebase Hosting**.

### Deploy to Firebase

```bash
# Login to Firebase
firebase login

# Initialize Firebase (if not already done)
firebase init hosting

# Build the project
npm run build

# Deploy to Firebase
firebase deploy
```

---

## 🔮 Future Enhancements

- [ ] Push notifications for vaccination reminders
- [ ] Integration with government immunization databases
- [ ] AI-powered vaccination schedule recommendations
- [ ] Offline mode with service workers
- [ ] Export records to government health portals
- [ ] Family sharing and multi-parent access
- [ ] Doctor appointment scheduling
- [ ] Vaccination center locator with maps

---

## 📞 Contact

**Developer:** Sai Kowshik Suggala

| Platform | Link |
|----------|------|
| 📧 **Email** | [saikowshiksuggala9390@gmail.com](mailto:saikowshiksuggala9390@gmail.com) |
| 🌐 **Portfolio** | [kowshiksuggala.vercel.app](https://kowshiksuggala.vercel.app) |
| 💻 **GitHub** | [github.com/KowshikSuggala25](https://github.com/KowshikSuggala25) |

---

<p align="center">
  <b>⭐ If you found this project helpful, please give it a star on GitHub! ⭐</b>
</p>

<p align="center">
  Made with ❤️ by Kowshik Suggala
</p>

