# 🤖 HireFlowAI - AI Hiring Automation System

> Fully automated **AI-powered hiring pipeline built in n8n** that screens candidates, evaluates resumes using LLMs, manages interview scheduling, and handles candidate communication automatically.

---

## 🎥 Workflow Preview

### 🔹 Workflow 1 — Candidate Ingestion & AI Screening

![Workflow 1](images/workflow1.png)

### 🔹 Workflow 2 — Communication & Interview Scheduling

![Workflow 2](images/workflow2.png)

---

## 📌 What is HireFlowAI?

HireFlowAI is an **end-to-end recruitment automation workflow** designed to eliminate repetitive hiring tasks and speed up candidate processing.

Instead of manually reviewing resumes, sending emails, and scheduling interviews, this system automates the entire flow using **n8n + AI + Supabase + Google Services**.

The workflow continuously monitors job applications, extracts and analyzes resumes using AI, classifies candidates, stores evaluations in a database, and automatically communicates hiring decisions.

---

## 🚀 Project Summary

This project automates hiring for **multiple job roles** including:

* 💻 Software Engineer (SWE)
* 📈 Business Development Manager (BDM)

Applications are collected through **Google Forms**, processed through **AI-powered resume screening**, stored in **Supabase**, and routed through intelligent hiring logic.

The system:

* Reads applications automatically
* Prevents duplicate processing
* Downloads and extracts resumes
* Uses AI to evaluate candidates
* Scores and classifies applicants
* Books interviews automatically
* Sends professional emails
* Maintains full hiring records

All without manual intervention.

---

## ⚙️ Features

* 📥 **Google Forms + Sheets Integration** – collect applications automatically
* 🧹 **Data Normalization** – unify different role forms into one schema
* 🔁 **Duplicate Detection** – avoid processing same candidate twice
* 📄 **Resume Download + PDF Extraction** – fetch resumes from Google Drive
* 🤖 **AI Resume Screening** – evaluate candidates using LLMs
* 🧠 **Gemini + Groq Fallback** – resilient AI pipeline
* 🛢 **Supabase Database** – central candidate storage
* 📅 **Interview Scheduling** – auto-book interview slots
* 📧 **Automated Emails** – acknowledgement, interview, review & rejection
* 🔄 **Decoupled Workflows** – ingestion and communication run independently
* 🚀 **Fully Automated Hiring Pipeline**

---

## 🧰 Tech Stack

| Component            | Tool / Service               |
| -------------------- | ---------------------------- |
| Automation Engine    | n8n                          |
| Forms & Responses    | Google Forms + Google Sheets |
| Resume Storage       | Google Drive                 |
| AI Screening         | Google Gemini                |
| AI Fallback          | Groq (Qwen)                  |
| Database             | Supabase PostgreSQL          |
| Interview Scheduling | Google Calendar              |
| Emails               | Gmail API                    |

---

## 🗂 Folder Structure

```bash
HireFlowAI/
├── images/
│   ├── workflow1.png
│   └── workflow2.png
│
├── workflow/
│   └── Hiring Automation.json
│
├── database_setup/
│   └── db_query.sql
│
└── README.md
```

---

# 🔄 How the Workflow Works

The automation is divided into **two independent workflows**.

This separation improves:

* Reliability
* Fault isolation
* Easier debugging
* Better scalability
* Human review flexibility

---

## 🚀 Workflow 1 — Candidate Ingestion & AI Screening

**Runs Every:** 2 Hours

### Flow

```text
Google Forms / Sheets
        ↓
Data Cleaning & Mapping
        ↓
Duplicate Check (Supabase)
        ↓
Resume Download (Drive)
        ↓
PDF Text Extraction
        ↓
AI Screening (Gemini → Groq)
        ↓
Store Candidate Record
        ↓
Confirmation Email
```

### What Happens?

1. Reads new applications from SWE and BDM forms
2. Cleans and maps form fields
3. Checks Supabase for duplicates
4. Downloads resumes
5. Extracts PDF content
6. Builds role-specific AI prompts
7. Evaluates candidate using AI
8. Stores AI assessment
9. Sends confirmation email

---

## 📧 Workflow 2 — Communication & Scheduling

**Runs Every:** 12 Hours

### Flow

```text
Pending Candidates
        ↓
AI Classification Check
        ↓
Strong / Average / Weak
        ↓
Interview / Review / Reject
        ↓
Status Update
```

### Decision Logic

### 🟢 Strong Candidates

```text
Available Slot Check
        ↓
Create Calendar Event
        ↓
Book Slot
        ↓
Interview Email
```

### 🟡 Average Candidates

```text
Manual Review Email
        ↓
Hiring Team Decision
```

### 🔴 Weak Candidates

```text
Rejection Email
```

---

## 🗄 Database Setup

The workflow uses **Supabase PostgreSQL** for persistent hiring data.

### Main Tables

### `candidates`

Stores:

* Candidate information
* Resume links
* AI score
* Classification
* Strengths & concerns
* Hiring status

### `available_slots`

Stores:

* Interview timings
* Booking status
* Assigned candidate

SQL setup file is included inside:

```bash
database_setup/
```

---

## ✅ Prerequisites

Before running locally, make sure you have:

* Running **n8n** instance
* Google account
* Google Forms + Sheets + Drive + Gmail + Calendar access
* Supabase project
* Gemini API key
* Groq API key

---

## 🔐 Credentials Setup

Configure these credentials inside n8n:

### 1. Google Sheets OAuth2

Used for:

* Reading application forms

---

### 2. Google Drive OAuth2

Used for:

* Downloading resumes

---

### 3. Google Calendar OAuth2

Used for:

* Creating interview events

---

### 4. Gmail OAuth2

Used for:

* Sending candidate emails

---

### 5. Supabase

Add:

* Project URL
* Service Role Key

Used for:

* Candidate database
* Interview slots

---

### 6. Gemini API

Used for:

* Primary AI screening

---

### 7. Groq API

Used for:

* AI fallback handling

---

# ⚙️ Run Locally

## Step 1 — Clone Repository

```bash
git clone https://github.com/fewgets/HireFlowAI.git
cd HireFlowAI
```

---

## Step 2 — Setup Database

Open **Supabase SQL Editor** and run:

```bash
database_setup/db_query.sql
```

This creates:

* candidates table
* available_slots table

---

## Step 3 — Import Workflow

Inside n8n:

```text
Workflows
    ↓
Import
    ↓
workflow/Hiring Automation.json
```

---

## Step 4 — Configure Credentials

Update:

* Google OAuth credentials
* Supabase keys
* Gemini API
* Groq API

Inside relevant nodes.

---

## Step 5 — Update Google Assets

Replace:

* Google Sheet IDs
* Calendar ID
* Manager Email
* Form-linked resources

Inside workflow nodes.

---

## Step 6 — Test Workflow

Run node-by-node:

```text
Sheets
↓
Drive
↓
AI
↓
Supabase
↓
Email
```

Verify successful execution.

---

## Step 7 — Activate

Once everything works:

```text
Save Workflow
        ↓
Enable Active Toggle
```

The automation now runs automatically.

---

## 📷 Workflow Screenshots

| Workflow 1                | Workflow 2                |
| ------------------------- | ------------------------- |
| ![](images/workflow1.png) | ![](images/workflow2.png) |

---

## 🤝 Contact & Support

For collaborations, freelance work, or questions:

### 👤 Usama Shahid

📧 **Email**
[dev.usamashahid@gmail.com](mailto:dev.usamashahid@gmail.com)

🔗 **LinkedIn**
https://linkedin.com/in/usamashahid2366009

🐙 **GitHub**
https://github.com/fewgets

---

## 📜 License

This project is built for **learning, automation research, and portfolio demonstration**.

Feel free to fork, improve, and adapt.

---

<div align="center">

### Built with ❤️ using n8n • Supabase • Gemini • Groq

*"Automating hiring so humans can focus on humans."*

</div>
