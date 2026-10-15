# TripMind — Autonomous AI Travel & Budget Planning Engine

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![LangGraph](https://img.shields.io/badge/LangGraph-Agentic_AI-orange?style=for-the-badge)](https://langchain-ai.github.io/langgraph/)
[![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-ORM-red?style=for-the-badge)](https://www.sqlalchemy.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Stripe](https://img.shields.io/badge/Stripe-API-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://stripe.com)

TripMind is an autonomous AI-powered travel planning and budget optimization platform that processes natural language queries to synthesize end-to-end travel itineraries, accommodation recommendations, cost breakdowns, and calendar-integrated booking workflows.

---

## Key Features

* **ReAct Agentic Workflow:** Powered by LangGraph and LLMs via OpenRouter, utilizing a Reasoning + Acting framework to orchestrate multi-step itinerary composition.
* **Intelligent Tool Registry:** Pydantic-validated tool integrations for flight discovery, accommodation selection, weather forecasts, and dynamic cost estimation.
* **Flexible Relational Persistence:** Dual database architecture supporting SQLite for rapid local prototyping and PostgreSQL with connection pooling for production deployments.
* **Secure Authentication & Payments:** Session-backed user authentication paired with native Stripe checkout workflows.
* **Interactive UI/UX:** Responsive client dashboard featuring glassmorphism design, real-time itinerary timelines, budget visualizations, and calendar exports.

---

## System Architecture

```
User (Browser)
   │
   ▼
FastAPI REST API Server (Uvicorn ASGI)
   │
   ├── /api/chat ──────► LangGraph ReAct Agent (OpenRouter / Llama 3.3 70B)
   │                        ├── Tool: Flight & Route Discovery
   │                        ├── Tool: Hotel & Accommodation Matching
   │                        ├── Tool: Dynamic Cost & Budget Optimizer
   │                        └── Tool: Daily Timeline Synthesis
   │
   ├── /api/itineraries ─► SQLAlchemy ORM Engine (Connection Pooled)
   │                        └── Database (PostgreSQL / SQLite fallback)
   │
   └── /api/bookings ────► Stripe Checkout & Webhook Pipeline
```

---

## Quick Start Guide

### 1. Prerequisites
* Python 3.10+
* Git

### 2. Clone Repository
```bash
git clone https://github.com/Dotify71/TripMind.git
cd TripMind
```

### 3. Environment Configuration
Copy the sample environment file and configure your credentials:
```bash
cp .env.example .env
```
Update `.env` with your API keys:
* `OPENROUTER_API_KEY`: Your LLM provider API key
* `STRIPE_SECRET_KEY`: Stripe test secret key (optional for local chat testing)
* `DATABASE_URL`: `sqlite:///./travel_planner.db` (default) or PostgreSQL connection URI

### 4. Install Dependencies
```bash
pip install -r requirements.txt
```

### 5. Launch the Application
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
Open **`http://localhost:8000`** in your browser to access the interactive dashboard.

---

## API Endpoints Overview

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/chat` | Natural language planning endpoint orchestrated by the LangGraph agent |
| `GET` | `/api/itineraries` | Retrieve saved user trip itineraries and budget models |
| `POST` | `/api/bookings/create-session` | Generate secure Stripe checkout session for trip booking |
| `GET` | `/api/calendar/events` | Fetch calendar events and scheduled travel timeline items |
| `POST` | `/api/auth/register` | User account registration with bcrypt password hashing |
| `POST` | `/api/auth/login` | Session token generation and authentication verification |

---

## Author & Maintainer

* **Dushyant Acharya** ([@Dotify71](https://github.com/Dotify71))
  * International Open Source Contributor (CNCF OpenTelemetry, openSUSE, Microsoft)
  * Speaker, openSUSE Conference 2026 (Nuremberg, Germany)

---

## License
This project is open-sourced under the MIT License.