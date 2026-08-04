# InnovaFund-AI

**Research Funding & Innovation Intelligence Platform**

An AI-powered platform that helps researchers, startups, universities, and innovation centers discover funding opportunities, analyze research trends, evaluate patent landscapes, and generate commercialization recommendations — all through a centralized innovation intelligence dashboard.

---

## Tech Stack

**Backend:** Python, FastAPI, SQLAlchemy
**Frontend:** React.js (Vite)
**Databases:** PostgreSQL (structured data), MongoDB (flexible/document data)
**Auth:** JWT-based authentication, bcrypt password hashing, role-based access control
**External Data:** OpenAlex API (publications), USPTO Open Data Portal (patents — pending API key)
**Infra:** Docker & Docker Compose (local Postgres + MongoDB)

---

## Project Structure

```
InnovaFund-AI/
├── docker-compose.yml       # Spins up Postgres + MongoDB containers
├── .gitignore
├── backend/
│   ├── main.py                # All API routes
│   ├── models.py               # SQLAlchemy models (User, ResearchProfile)
│   ├── database.py              # DB session/engine setup
│   ├── auth.py                    # Password hashing, JWT creation/verification
│   ├── dependencies.py             # Auth guards (get_current_user, require_role)
│   ├── schemas.py                    # Pydantic request/response models
│   └── requirements.txt
├── frontend/
│   ├── src/                            # React app
│   └── package.json
└── database/
    └── schema.sql                        # Table definitions
```

---

## Getting Started

### Prerequisites
- Docker Desktop
- Python 3.11+
- Node.js 18+
- Git

### Setup

```bash
# 1. Clone the repo
git clone https://github.com/Nithya21shree/InnovaFund-AI.git
cd InnovaFund-AI

# 2. Start the databases
docker compose up -d

# 3. Backend setup
cd backend
python -m venv venv
venv\Scripts\activate        # Windows
pip install -r requirements.txt

# Create a .env file with:
# POSTGRES_URL=postgresql://postgres:postgres@localhost:5433/funding_innovation_platform
# MONGO_URL=mongodb://localhost:27017
# SECRET_KEY=your-secret-key-here

# Apply the schema
psql -U postgres -h localhost -p 5433 -d funding_innovation_platform -f ../database/schema.sql

# Run the backend
uvicorn main:app --reload
# API docs available at http://127.0.0.1:8000/docs

# 4. Frontend setup (in a separate terminal)
cd frontend
npm install
npm run dev
# App available at http://localhost:5173
```

---

## Database Schema

### `users`

| Column | Type | Purpose |
|---|---|---|
| `id` | SERIAL | Primary key |
| `full_name` | VARCHAR(150) | User's name |
| `email` | VARCHAR(150), UNIQUE | Login identifier |
| `password_hash` | VARCHAR(255) | bcrypt-hashed password (never stored in plain text) |
| `role` | VARCHAR(50) | One of: `researcher`, `startup_founder`, `innovation_manager`, `administrator` |
| `organization` | VARCHAR(200) | Optional — university/company name |
| `created_at` | TIMESTAMP | Auto-set on account creation |

### `research_profiles`

| Column | Type | Purpose |
|---|---|---|
| `id` | SERIAL | Primary key |
| `user_id` | INTEGER, FOREIGN KEY → `users.id` | Links profile to a user (one-to-one) |
| `research_domains` | TEXT | e.g. "AI, Machine Learning" |
| `keywords` | TEXT | e.g. "NLP, RAG, LLMs" |
| `publications` | TEXT | User's listed publications |
| `patents` | TEXT | User's listed patents |
| `technology_areas` | TEXT | e.g. "Agentic AI" |
| `created_at` | TIMESTAMP | Auto-set on creation |

`research_profiles.user_id` uses `ON DELETE CASCADE` — if a user is deleted, their research profile is deleted automatically rather than left orphaned. Authentication data (`users`) is kept separate from domain-specific data (`research_profiles`) so the core user table stays lean and reusable across the app.

---

## API Endpoints

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| GET | `/` | Health/status message | No |
| GET | `/health` | Checks DB connectivity | No |
| POST | `/register` | Create a new user | No |
| POST | `/login` | Log in, returns JWT token | No |
| GET | `/me` | Get current user's details | Yes |
| GET | `/admin/users` | List all users | Yes (admin only) |
| POST | `/profile` | Create/update research profile | Yes |
| GET | `/profile` | Get own research profile | Yes |
| GET | `/publications/search?query=...` | Search live publication data (OpenAlex) | No |
| GET | `/patents/search?query=...` | Search patent data | No (pending USPTO API key) |

**User roles:** `researcher`, `startup_founder`, `innovation_manager`, `administrator`

---

## Project Status — Milestone 1 (Week 1 & 2)

- [x] Frontend and backend environments set up (Docker, FastAPI, React/Vite)
- [x] Database schema designed and applied
- [x] Authentication and role-based access control implemented and tested
- [x] Research profile management (create/view) implemented and tested
- [x] Publication dataset integration (OpenAlex — live)
- [ ] Patent dataset integration — endpoint built, pending USPTO Open Data Portal API key (requires a verified USPTO.gov account with MFA)
- [ ] System architecture diagram
- [ ] UI wireframes and workflow planning
- [ ] Project objectives / workflow document

**Upcoming:** Milestone 2 — funding recommendation engine, research trend intelligence dashboards

---

## Branching

Each team member works on their own branch and merges into `main` via Pull Request after review. This branch: `saumyaa-dev`.
