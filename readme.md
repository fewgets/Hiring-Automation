<!-- HireFlow AI · README by Usama Shahid (fewgets) -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,55:0F3D3E,100:36FFC7&height=230&section=header&text=HireFlow%20AI&fontSize=60&fontColor=FFFFFF&fontAlignY=36&desc=End-to-end%20AI%20hiring%20automation%20built%20in%20n8n&descSize=17&descAlignY=58&animation=fadeIn" width="100%" alt="HireFlow AI"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=700&color=36FFC7&center=true&vCenter=true&width=720&height=60&lines=AI+Resume+Screening;Automatic+Interview+Scheduling;Hiring+Without+the+Busywork" alt="Typing SVG"/>

<p>
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n"/>
  <img src="https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white" alt="Gemini"/>
  <img src="https://img.shields.io/badge/Groq-F55036?style=for-the-badge&logo=groq&logoColor=white" alt="Groq"/>
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase"/>
  <img src="https://img.shields.io/badge/Google%20Workspace-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Google Workspace"/>
</p>

</div>

---
## 📌 Overview

**HireFlow AI** is an end-to-end **recruitment automation system** built in **n8n**. It takes over the
repetitive parts of hiring (reading applications, screening resumes, sending emails and booking
interviews) so the hiring team only spends time on the candidates who matter.

Applications come in through **Google Forms**, resumes are screened by **AI (Gemini, with Groq as a
fallback)**, every decision is stored in **Supabase**, and candidates automatically get the right
email or an **interview booked on Google Calendar**.

> Currently configured for two roles: 💻 **Software Engineer** and 📈 **Business Development Manager**.

---

## 🎥 Workflows

### 🔹 Workflow 1: Candidate Ingestion and AI Screening
<p align="center"><img src="images/workflow1.png" alt="Workflow 1" width="95%"/></p>

### 🔹 Workflow 2: Communication and Interview Scheduling
<p align="center"><img src="images/workflow2.png" alt="Workflow 2" width="95%"/></p>

---

## ✨ Features

| | Feature |
|:-:|---|
| 📥 | Collects applications from **Google Forms and Sheets** |
| 🧹 | Normalises different role forms into **one candidate schema** |
| 🔁 | **Duplicate detection** so no candidate is processed twice |
| 📄 | Downloads resumes from **Google Drive** and extracts PDF text |
| 🤖 | **AI screening** with role-specific prompts: score, strengths, concerns |
| 🧠 | **Gemini → Groq fallback** keeps screening running if one provider fails |
| 🛢️ | Full candidate history in **Supabase PostgreSQL** |
| 📅 | **Automatic interview booking** in free calendar slots |
| 📧 | Acknowledgement, interview, review and rejection **emails** |
| 🔄 | Two **decoupled workflows** for reliability and easy debugging |

---

## 🔄 How It Works

### 🚀 Workflow 1: Ingestion and Screening *(every 2 hours)*

```mermaid
flowchart LR
    F[📝 Google Forms<br/>+ Sheets] --> N[🧹 Clean and map]
    N --> D{🔁 Duplicate?}
    D -->|Yes| S[⏭️ Skip]
    D -->|No| R[📄 Download resume<br/>+ extract PDF]
    R --> AI[🤖 AI screening<br/>Gemini → Groq]
    AI --> DB[(🛢️ Supabase)]
    DB --> E[📧 Confirmation email]
```

### 📧 Workflow 2: Communication and Scheduling *(every 12 hours)*

```mermaid
flowchart LR
    P[⏳ Pending candidates] --> C{🧠 AI classification}
    C -->|🟢 Strong| I[📅 Book free slot<br/>+ interview email]
    C -->|🟡 Average| M[👀 Manual review email<br/>to hiring team]
    C -->|🔴 Weak| X[✉️ Polite rejection]
    I --> U[(Update status)]
    M --> U
    X --> U
```

---

## 🗄️ Database

| Table | Stores |
|---|---|
| `candidates` | Personal info, resume link, AI score, classification, strengths and concerns, hiring status |
| `available_slots` | Interview times, booking status, assigned candidate |

The SQL is in [`database_setup/queries.txt`](database_setup/queries.txt).

---

## ⚙️ Setup

### ✅ Prerequisites
A running **n8n** instance · a Google account (Forms, Sheets, Drive, Gmail, Calendar) · a **Supabase** project · **Gemini** and **Groq** API keys.

### 1. Clone
```bash
git clone https://github.com/fewgets/Hiring-Automation.git
cd Hiring-Automation
```

### 2. Database
Open the **Supabase SQL Editor** and run `database_setup/queries.txt`. This creates `candidates` and `available_slots`.

### 3. Import the workflow
In n8n: **Workflows → Import** → `workflow/Hiring Automation.json`.

### 4. Credentials
Add these in n8n:

| Credential | Used for |
|---|---|
| Google Sheets OAuth2 | Reading applications |
| Google Drive OAuth2 | Downloading resumes |
| Google Calendar OAuth2 | Creating interview events |
| Gmail OAuth2 | Candidate emails |
| Supabase (URL + service role key) | Candidate database and slots |
| Gemini API | Primary AI screening |
| Groq API | AI fallback |

### 5. Your Google assets
Replace the Sheet IDs, Calendar ID, hiring-manager email and form-linked resources in the workflow nodes.

### 6. Test and activate
Run node by node (Sheets → Drive → AI → Supabase → Email), then switch the workflow to **Active**.

---

## 🧰 Tech Stack

| Component | Tool |
|---|---|
| Automation Engine | n8n |
| Forms and Responses | Google Forms + Google Sheets |
| Resume Storage | Google Drive |
| AI Screening | Google Gemini |
| AI Fallback | Groq (Qwen) |
| Database | Supabase PostgreSQL |
| Scheduling | Google Calendar |
| Email | Gmail API |

```text
Hiring-Automation/
├── images/              # Workflow screenshots
├── workflow/            # n8n workflow export (JSON)
├── database_setup/      # Supabase SQL
└── readme.md
```

---

## 🤝 Let's Work Together

<div align="center">

**Have an idea, a freelance project, or want to collaborate on something in AI?**
I'm always open to collaborations, freelance work and full-time opportunities.

<a href="mailto:shaikhusama541@gmail.com?subject=Collaboration%20-%20HireFlow%20AI">
  <img src="https://img.shields.io/badge/Email-shaikhusama541%40gmail.com-36FFC7?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0D1117" alt="Email"/>
</a>
<a href="https://www.linkedin.com/in/-usamashahid/">
  <img src="https://img.shields.io/badge/LinkedIn-Usama%20Shahid-36FFC7?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0D1117" alt="LinkedIn"/>
</a>
<a href="https://github.com/fewgets">
  <img src="https://img.shields.io/badge/GitHub-fewgets-36FFC7?style=for-the-badge&logo=github&logoColor=white&labelColor=0D1117" alt="GitHub"/>
</a>

<br/><br/>

⭐ **If you like this project, please give it a star. It really helps!** ⭐

<br/>

<h3>"Automating hiring so humans can focus on humans."</h3>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:36FFC7,55:0F3D3E,100:0D1117&height=150&section=footer&animation=twinkling" width="100%" alt="footer"/>

</div>
