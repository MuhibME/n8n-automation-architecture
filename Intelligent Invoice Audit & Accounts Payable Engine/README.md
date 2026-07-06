# AI-Powered Invoice Audit & Automation Engine
<img width="1589" height="663" alt="image" src="https://github.com/user-attachments/assets/7377e4c8-2bb6-484e-af2e-e4c296888f4e" />

An enterprise-grade, closed-loop backend automation pipeline that ingests unstructured invoice PDFs, extracts structured data using Generative AI, validates mathematical integrity, defends against duplicate submissions, and routes data dynamically to a custom PostgreSQL database and notification loops.

## 🚀 System Architecture

The workflow is self-hosted via Docker Compose and exposed through a secure Cloudflare network tunnel to process incoming documents in real time.

1. **Ingestion & Data Extraction:** Receives PDF inputs, leveraging an LLM extraction node to transform unstructured document layout into a structured JSON payload.
2. **Defensive Identity Resolution:** Queries a custom PostgreSQL instance using a composite fingerprint to intercept duplicate submissions before executing heavy operational logic.
3. **Deterministic Math Audit:** Executes a strict calculation check (`Subtotal + Tax == Grand Total`) using JavaScript floating-point correction algorithms to evaluate billing accuracy.
4. **Conditional Routing & Dual-Branch Persistence:** Dynamically updates invoice lifecycles based on audit outcomes, saving clear audit logs into a relational database.
5. **Real-Time Notification Loop:** Closes the operations loop using Gmail API OAuth2 integration to alert respective stakeholders dynamically.

---

## 🛠️ Tech Stack

* **Workflow Orchestration:** n8n (Self-Hosted, Dockerized)
* **Database Engine:** PostgreSQL 16 (Custom relational schema)
* **AI Processing Layer:** Google Gemini (Structured text extraction)
* **Network & Proxying:** Cloudflare Tunnels (Secure Webhook Routing)
* **Notification Layer:** Google Workspace / Gmail API (OAuth 2.0 Identity Protocol)

---
