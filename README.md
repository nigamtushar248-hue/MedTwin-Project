# 🧬 MedTwin AI — Autonomous AI Healthcare Digital Twin

> **MedTwin AI** is a persistent, continuously updated virtual model of a patient's medical state, powered by **Multi-Agent AI orchestration (LangGraph)** and secured by an **Immutable Blockchain Layer (Polygon)**.

🌐 **Live Deployment URL:** [http://13.239.27.137:5173/](http://13.239.27.137:5173/)

## 🚨 The Problem
Rural chronic-care patients struggle to maintain consistent specialist follow-up because their medical history, reports, and health changes remain fragmented across consultations.
1. **Doctors** suffer from alert fatigue and lack unified, actionable patient insights. 
2. **Patients** do not have a real-time, holistic view of their health trajectory.
3. **Data Security** is often compromised, with medical records lacking auditable, tamper-proof history.

## 💡 Our Solution
**MedTwin AI** acts as a true **Digital Twin** for patients. Instead of generic LLM chatbots, we utilize an **explicit, stateful Multi-Agent Pipeline (LangGraph)** that continuously digests new physical lab reports, prescriptions, and wearable vitals to dynamically update the patient's health state. 

To ensure absolute trust and HIPAA/GDPR compliance, raw data remains in a secure, private database. However, a cryptographic **SHA-256 hash of every medical event is permanently stored on the Polygon Blockchain**. This creates an immutable audit trail requiring Doctor cryptographic sign-offs, bridging AI innovation with Web3 security.

---

## ✨ Key Features & Portals

### 🧑‍⚕️ Patient Portal (Real-time Health Tracking)
* **Live Health Score**: A dynamic 0-100 wellness score calculated based on AI-analyzed vitals and lab results.
* **Risk Trajectory Charts**: Interactive historical health data visualization utilizing `Recharts`.
* **Automated Data Entry**: Drag-and-drop OCR pipeline to automatically parse physical blood test reports into structured JSON.

### 🩺 Doctor Portal (Verification & Audit)
* **AI Recommendation Queue**: Doctors review AI-generated risk flags, potential drug interactions, and lifestyle recommendations.
* **One-Click Cryptographic Sign-off**: Doctors approve AI suggestions, signing the transaction directly onto the Polygon blockchain via their Web3 wallet.

### 🧠 Deep Dive: The 5 Autonomous AI Agents (LangGraph)
Our AI layer completely bypasses traditional reactive prompts. We use a LangGraph `StateGraph` where 5 specialized agents operate over a persistent `MedTwinState`:
1. **Medical Report Agent**: Uses OCR to extract raw text from uploaded reports, parses it into structured lab values (e.g., `HbA1c: 6.8%`), and assigns a confidence score.
2. **Health Prediction Agent**: Analyzes the parsed data to output a disease risk score and determines if the patient's trend is improving or worsening.
3. **Medication Agent**: Cross-checks active prescriptions against new OCR data to prevent fatal drug interactions and manages scheduling.
4. **Lifestyle Agent**: Consolidates risk profiles into personalized daily targets (Diet, Sleep, Exercise, Hydration).
5. **Emergency Agent**: Bypasses the queue to alert on real-time vitals threshold breaches (e.g., `Sustained Heart Rate > 140bpm`).

### ⛓️ Deep Dive: Polygon Blockchain Security Layer
Medical records require absolute immutability. Our EVM Smart Contract (`MedTwinTrust.sol`) on the **Polygon Amoy Testnet** handles:
* **Tamper-Proof Hashing**: The backend generates a SHA-256 hash of the medical report. Only this hash is stored on-chain, keeping raw data private.
* **`verifyHash()`**: A function that instantly detects if a database record has been maliciously altered.
* **Doctor Approvals**: Records the exact timestamp and Wallet Address of the physician who approved the AI recommendation.

---

🛠️ Complete Technology Stack
Frontend
React 18 — Interactive Patient, Doctor & Admin portals
Vite — Frontend build and development environment
Tailwind CSS — Responsive UI and Glassmorphism-based design
Recharts — Health-score, risk-trajectory and longitudinal data visualization
Backend
Python 3.11+
FastAPI — High-performance REST API layer
SQLAlchemy — ORM and database management
JWT Authentication — Secure role-based authentication and authorization
REST APIs — Communication between frontend, AI services and backend
Database & Data Layer
PostgreSQL — Persistent storage for users, medical records, reports, symptoms and Digital Twin state
Vector Database — Semantic retrieval of clinically relevant symptom patterns and laboratory investigations
Structured JSON Health State — Maintains the patient's continuously updated Digital Twin
AI / ML Layer
LangGraph — Stateful Multi-Agent AI orchestration
LLMs (Groq / OpenAI APIs) — Medical information analysis and agent reasoning
Lightweight Transformer Model — Generates semantic embeddings from user-entered symptoms
Semantic Vector Search — Matches symptoms against relevant clinical patterns and laboratory investigations
PaddleOCR / Tesseract OCR — Extracts information from uploaded medical reports
Multi-Agent AI Pipeline — Specialized agents analyze different aspects of the patient's health
5 Specialized AI Agents
Medical Report Agent — Extracts and structures laboratory values from medical reports.
Health Prediction Agent — Analyzes health data and identifies changes in risk/trends.
Medication Agent — Analyzes prescriptions and potential medication-related conflicts.
Lifestyle Agent — Generates personalized lifestyle insights based on the patient's health state.
Emergency Agent — Detects potentially critical patterns and triggers appropriate alerts.
Symptom Investigation Engine
Transformer-based embeddings convert free-text symptoms into numerical representations.
Vector similarity search identifies the closest relevant clinical patterns.
Semantic matching connects symptoms with potentially relevant laboratory investigations.
Relevance scoring indicates how closely the user's symptoms match indexed patterns.
Urgency classification highlights potentially concerning symptom combinations.
Designed as an assistive investigation-recommendation system, not a diagnostic tool.
Blockchain & Trust Layer
Polygon Amoy Testnet — Immutable audit trail
Solidity — Smart contract development
Hardhat — Smart contract development and testing
Ethers.js / Web3 — Blockchain interaction
SHA-256 — Cryptographic hashing of medical events
MedTwinTrust.sol — Stores hashes and doctor approval records on-chain
Hash Verification — Detects whether an off-chain medical record has been altered
Infrastructure & DevOps
Docker — Containerized application deployment
Docker Compose — Multi-service local orchestration
AWS EC2 — Cloud deployment
Git & GitHub — Version control and collaboration
Overall Architecture
                    ┌──────────────────────────────┐
                    │        REACT FRONTEND        │
                    │ Patient | Doctor | Admin UI  │
                    └──────────────┬───────────────┘
                                   │
                              REST APIs
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │       FASTAPI BACKEND        │
                    │ Auth | APIs | Orchestration  │
                    └───────┬───────────┬──────────┘
                            │           │
                ┌───────────┘           └────────────┐
                ▼                                    ▼
      ┌──────────────────┐                 ┌──────────────────┐
      │    LANGGRAPH     │                 │   POSTGRESQL     │
      │  Multi-Agent AI  │                 │ Patient Health   │
      │                  │                 │ Digital Twin     │
      │ 5 Specialized    │                 └──────────────────┘
      │ AI Agents        │
      └────────┬─────────┘
               │
       ┌───────┴────────┐
       ▼                ▼
┌──────────────┐  ┌──────────────────┐
│ Transformer  │  │   Vector DB      │
│ Embeddings   │  │ Semantic Search  │
└──────────────┘  └──────────────────┘
               │
               ▼
      Symptom → Clinical
      Pattern → Test
      Recommendation

               +
               │
               ▼
      ┌──────────────────┐
      │ POLYGON BLOCKCHAIN│
      │   Trust Layer     │
      │ SHA-256 Hashes    │
      │ Doctor Sign-offs  │
      └──────────────────┘

---

## 🚀 Step-by-Step Local Setup Guide

### Option 1: One-Click Docker Setup (Recommended)
You can spin up the entire application stack (Frontend, Backend, and Database) with a single command:
```bash
docker compose up --build
```
* **Frontend UI**: `http://localhost:5173`
* **FastAPI Swagger Docs**: `http://localhost:8000/docs`

### Option 2: Manual Setup
#### 1. Backend Setup
```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```
#### 2. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```
