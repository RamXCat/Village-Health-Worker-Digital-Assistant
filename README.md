<div align="center">
  <img src="public/icons.svg" alt="ASHA Saathi Logo" width="120" />
  <h1>ASHA Saathi</h1>
  <p><strong>Village Health Worker Digital Assistant & Real-Time Monitoring Ecosystem</strong></p>
  <p>Empowering Accredited Social Health Activists (ASHAs) with offline-first digital tools and real-time clinical oversight for rural healthcare.</p>

  <p>
    <a href="#-key-features">Key Features</a> •
    <a href="#-system-architecture">System Architecture</a> •
    <a href="#-tech-stack">Tech Stack</a> •
    <a href="#-getting-started">Getting Started</a> •
    <a href="#-api-endpoints">API Reference</a> •
    <a href="#-team--acknowledgments">Team</a>
  </p>

  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
  [![Platform: Android](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)]()
  [![Backend: Node.js](https://img.shields.io/badge/Backend-Node.js-339933?logo=nodedotjs&logoColor=white)]()
  [![Database: SQLite](https://img.shields.io/badge/Database-SQLite-003B57?logo=sqlite&logoColor=white)]()
  [![UI: Jetpack_Compose](https://img.shields.io/badge/UI-Jetpack_Compose-4285F4?logo=jetpackcompose&logoColor=white)]()
</div>

---

## 📖 Overview

**ASHA Saathi** was developed during a hackathon to solve critical challenges faced by frontline health workers (ASHAs) in remote, rural communities. In areas with intermittent or zero internet connectivity, paper-based reporting often causes delays, lost records, and missed high-risk patient follow-ups.

**ASHA Saathi** bridges this gap through a dual-component platform:
1. **Offline-First Android App:** For ASHA workers in the field to log patient registrations, vitals, maternal checks, and immunization records offline.
2. **Doctor & Supervisor Web Dashboard:** A centralized, real-time command portal where supervising medical officers can view clinical alerts, patient trends, and prioritize immediate interventions.

---

## ✨ Key Features

- 📶 **Offline-First Resilience:** Zero internet needed during field visits. Patient forms and health checks are stored securely in local SQLite/Room storage and synchronized in the background via WorkManager when connectivity resumes.
- 🚨 **Automated Clinical Alerts:** Automatically flags critical conditions (e.g., severe maternal anemia, hypertension, high fever in infants, missed immunizations) directly to supervisors.
- 📊 **Doctor & PHC Dashboard:** High-level analytics and granular patient inspection for Primary Health Centre (PHC) doctors, including triage and status management.
- 🔐 **Role-Based Access Control:** Dedicated, secure workflows for field healthcare workers and supervisory medical personnel.
- ⚡ **Lightweight & Portable:** Engineered for low-resource devices and constrained environments with minimal battery and network overhead.

---

## 🏗️ System Architecture

```
                      ┌────────────────────────────────────────┐
                      │          Frontline ASHA Worker         │
                      │         (Field / Rural Areas)          │
                      └──────────────────┬─────────────────────┘
                                         │
                                 [Offline Visits]
                                         │
                                         ▼
                      ┌────────────────────────────────────────┐
                      │       ASHA Saathi Android App          │
                      │  • Kotlin / Jetpack Compose UI         │
                      │  • Local Room SQLite Database          │
                      │  • Retrofit & Background WorkManager   │
                      └──────────────────┬─────────────────────┘
                                         │
                             [Auto Sync when Online]
                                         │
                                         ▼
                      ┌────────────────────────────────────────┐
                      │         Node.js / Express API          │
                      │       (REST Server & Data Sync)        │
                      └──────────────────┬─────────────────────┘
                                         │
                                         ▼
                      ┌────────────────────────────────────────┐
                      │        SQLite Central Database         │
                      │   (Patients, Visits, Vitals, Alerts)   │
                      └──────────────────┬─────────────────────┘
                                         │
                               [Real-Time Inspection]
                                         │
                                         ▼
                      ┌────────────────────────────────────────┐
                      │       Doctor & Admin Dashboard         │
                      │  • Real-time Critical Alerts & Triage  │
                      │  • Patient Management & Analytics      │
                      └────────────────────────────────────────┘
```

---

## 💻 Tech Stack

| Domain | Technologies |
|---|---|
| **Android Client** | Kotlin, Jetpack Compose, Android Architecture Components, Room DB, WorkManager, Retrofit2, Coroutines |
| **Backend & API** | Node.js, Express.js, RESTful Architecture, CORS, bcrypt / auth utilities |
| **Persistence** | SQLite (`ashasaathi.db`) |
| **Web Dashboard** | Responsive HTML5, CSS3 Modern Flex/Grid, Vanilla JavaScript, Charting & Data Tables |

---

## 📂 Repository Structure

```text
├── AshaSaathiAndroid/     # Native Android Application (Kotlin / Jetpack Compose)
│   ├── app/               # Main application source, Room DB, UI screens, network layer
│   └── gradle/            # Gradle build system wrappers
├── backend/               # REST API server & database scripts
│   ├── server.js          # Express server endpoints & synchronization handlers
│   ├── database.js        # SQLite schema initialization and query operations
│   └── ashasaathi.db      # Local SQLite database
├── dashboard/             # Web-based supervisory portal
│   ├── index.html         # Main overview dashboard
│   ├── alerts.html        # Critical alert triage & notifications
│   ├── patients.html      # Patient registry & health histories
│   ├── settings.html      # Configuration & role preferences
│   └── script.js          # Frontend interactivity & REST API integrations
├── public/                # Static assets, branding, and icons
├── CODE_OF_CONDUCT.md     # Community guidelines
├── CONTRIBUTING.md         # Contribution standards and pull request workflows
└── LICENSE                # MIT License
```

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/en/) (v16.x or newer) & `npm`
- [Android Studio](https://developer.android.com/studio) (Giraffe / Hedgehog or newer)
- Java Development Kit (JDK 17)
- Android device or emulator running API Level 26+

---

### 1. Backend Server Setup

```bash
# Navigate to the backend directory
cd backend

# Install dependencies
npm install

# Start the server
npm start
```

The REST API server will run on:
```
http://localhost:3000
```

---

### 2. Supervisory Web Dashboard

The web dashboard is hosted directly by the backend server. Once your backend is running, open your browser and visit:

```
http://localhost:3000/dashboard
```

---

### 3. Android Application Setup

1. Open **Android Studio**.
2. Select **File > Open** and choose the `AshaSaathiAndroid` folder.
3. Allow Gradle to download dependencies and sync the project.
4. Update `BASE_URL` in the network configuration to point to your backend's host machine IP (or `10.0.2.2:3000` for default Android emulator).
5. Build and launch on your connected device or emulator.

---

## 🔌 API Reference

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/patients` | Retrieve all registered patients |
| `POST` | `/api/patients` | Register a new patient |
| `POST` | `/api/sync` | Batch synchronization endpoint for offline-collected field visits |
| `GET` | `/api/alerts` | Fetch active critical clinical alerts for supervisors |
| `POST` | `/api/alerts/:id/resolve` | Mark an urgent alert as resolved |

---

## 👥 Team & Hackathon Story

This project was conceived and built with passion as a hackathon initiative to bring modern, reliable digital healthcare infrastructure to underserved rural communities.

Special thanks to all team members and mentors who contributed to the concept, field workflow designs, and prototype development!

---

## 📄 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.
