# IntelliTradeX Backend

## Overview

This is the backend service for **IntelliTradeX**, an AI-powered stock market intelligence platform.

At this stage, the backend includes:

* Project setup using **FastAPI**
* Dependency management using **UV**
* Initial **enterprise-level folder structure**
* Basic API routing setup

This forms the foundation for building scalable features like trading systems, AI insights, and real-time data processing.

---

## Tech Stack (Current Setup)

### Backend Framework

* FastAPI
* Python 3.12+

### Dependency Management

* UV (`pyproject.toml` based)

### Database (Planned Integration)

* PostgreSQL
* SQLAlchemy
* Alembic

### Async & Background (Planned)

* Redis
* Celery
* Kafka

### AI Stack (Planned)

* LangChain
* FAISS / ChromaDB
* HuggingFace Transformers

---

## Project Structure

```id
backend/
│
├── app/
│   ├── main.py                         # FastAPI entrypoint
│   ├── __init__.py
│   │
│   ├── api/                            # Presentation Layer (routes)
│   │   ├── __init__.py
│   │   └── v1/
│   │       ├── __init__.py
│   │       ├── api.py                  # Central router
│   │       │
│   │       └── endpoints/
│   │           ├── __init__.py
│   │           ├── auth.py             # Auth endpoints
│   │           ├── user.py             # User APIs
│   │           ├── market.py           # Market data APIs
│   │           ├── trading.py          # Order execution APIs
│   │           ├── portfolio.py        # Portfolio APIs
│   │           ├── ai.py               # AI endpoints
│   │           ├── strategy.py         # Strategy APIs
│   │           ├── notification.py     # Alerts APIs
│   │           └── admin.py            # Admin APIs
│   │
│   ├── core/                           # Core configs & system logic
│   │   ├── __init__.py
│   │   ├── config.py                   # Environment settings
│   │   ├── security.py                 # JWT, hashing
│   │   ├── dependencies.py             # FastAPI dependencies
│   │   ├── constants.py                # App constants
│   │   ├── logging.py                  # Logging config
│   │   └── events.py                   # Startup/shutdown events
│   │
│   ├── models/                         # SQLAlchemy Models
│   │   ├── __init__.py
│   │   ├── base.py                     # Base model
│   │   ├── user.py
│   │   ├── role.py
│   │   ├── portfolio.py
│   │   ├── order.py
│   │   ├── trade.py
│   │   ├── transaction.py
│   │   ├── stock.py
│   │   ├── strategy.py
│   │   ├── notification.py
│   │   └── audit.py
│   │
│   ├── schemas/                        # Pydantic Schemas
│   │   ├── __init__.py
│   │   ├── auth.py
│   │   ├── user.py
│   │   ├── portfolio.py
│   │   ├── order.py
│   │   ├── trade.py
│   │   ├── stock.py
│   │   ├── strategy.py
│   │   └── notification.py
│   │
│   ├── repository/                     # Data Access Layer
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── user_repository.py
│   │   ├── portfolio_repository.py
│   │   ├── order_repository.py
│   │   ├── trade_repository.py
│   │   ├── strategy_repository.py
│   │   ├── notification_repository.py
│   │   └── audit_repository.py
│   │
│   ├── services/                       # Business Logic Layer
│   │   ├── __init__.py
│   │   ├── auth_service.py
│   │   ├── user_service.py
│   │   ├── trading_service.py
│   │   ├── portfolio_service.py
│   │   ├── market_service.py
│   │   ├── strategy_service.py
│   │   ├── ai_service.py
│   │   ├── notification_service.py
│   │   └── risk_service.py
│   │
│   ├── db/                             # Database Layer
│   │   ├── __init__.py
│   │   ├── session.py                  # DB session
│   │   ├── base.py                     # Import all models for Alembic
│   │   └── init_db.py                  # DB initialization
│   │
│   ├── ai/                             # AI Engine
│   │   ├── __init__.py
│   │   │
│   │   ├── agents/                     # Multi-agent system
│   │   │   ├── __init__.py
│   │   │   ├── market_agent.py
│   │   │   ├── news_agent.py
│   │   │   ├── risk_agent.py
│   │   │   └── advisor_agent.py
│   │   │
│   │   ├── rag/                        # RAG pipeline
│   │   │   ├── __init__.py
│   │   │   ├── pipeline.py
│   │   │   ├── embeddings.py
│   │   │   ├── retriever.py
│   │   │   └── vector_store.py
│   │   │
│   │   ├── models/                     # ML models / wrappers
│   │   │   ├── __init__.py
│   │   │   └── llm.py
│   │   │
│   │   ├── prompts/                    # Prompt templates
│   │   │   ├── __init__.py
│   │   │   └── templates.py
│   │   │
│   │   └── utils/                      # AI utilities
│   │       ├── __init__.py
│   │       └── helpers.py
│   │
│   ├── workers/                        # Background jobs (Celery)
│   │   ├── __init__.py
│   │   ├── celery_app.py
│   │   │
│   │   └── tasks/
│   │       ├── __init__.py
│   │       ├── market_tasks.py
│   │       ├── ai_tasks.py
│   │       └── notification_tasks.py
│   │
│   ├── realtime/                       # WebSocket Layer
│   │   ├── __init__.py
│   │   ├── manager.py
│   │   ├── market_stream.py
│   │   └── notification_stream.py
│   │
│   ├── utils/                          # Shared Utilities
│   │   ├── __init__.py
│   │   ├── helpers.py
│   │   ├── validators.py
│   │   ├── enums.py
│   │   └── exceptions.py
│   │
│   └── tests/                          # Unit Tests (app-level)
│       ├── __init__.py
│       ├── test_auth.py
│       ├── test_user.py
│       └── test_health.py
│
├── alembic/                            # DB migrations
│   ├── versions/
│   └── env.py
│
├── scripts/                            # Utility scripts
│   ├── seed_data.py
│   ├── create_admin.py
│   └── run_workers.py
│
├── tests/                              # Integration tests
│   ├── test_main.py
│   └── test_api.py
│
├── .env
├── .env.example
├── .gitignore
├── pyproject.toml
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md
```

---

## Architecture Overview

The backend follows a **layered architecture**:

```id="qz6y7c"
API Layer → Service Layer → Repository Layer → Database
```

### Layers Description

* **API Layer**: Handles HTTP requests and responses (FastAPI routes)
* **Service Layer**: Contains business logic
* **Repository Layer**: Handles database operations
* **Models & Schemas**: Define data structure and validation

---

## Setup Instructions

### 1. Clone Repository

```bash id="c4l0s1"
git clone https://github.com/Ashu11122000/IntelliTradeX.git
cd IntelliTradeX/backend
```

---

### 2. Install UV

```bash id="o8jv2m"
pip install uv
```

---

### 3. Create Virtual Environment

```bash id="r9x1kp"
uv venv
```

Activate environment:

**Windows**

```bash id="0gx1n8"
.\.venv\Scripts\activate
```

---

### 4. Install Dependencies

```bash id="c2y7rt"
uv sync
```

---

### 5. Environment Variables

Create a `.env` file:

```env id="c6q1hf"
DATABASE_URL=postgresql://user:password@localhost:5432/intellitradex
SECRET_KEY=your_secret_key
REDIS_URL=redis://localhost:6379
```

---

### 6. Run the Server

```bash id="i7w9zp"
uv run uvicorn app.main:app --reload
```

---

### 7. Access API

* Base URL:

```id="9o8plm"
http://127.0.0.1:8000
```

* Swagger Docs:

```id="4d8k2q"
http://127.0.0.1:8000/docs
```

---

## API Versioning

All APIs are prefixed with:

```id="6g3t1p"
/api/v1
```

---

## Current Status

### Completed

* Project initialization with Git
* Backend setup with FastAPI
* Dependency management using UV
* Initial folder structure (enterprise-level)
* Basic routing setup

### In Progress

* Database configuration (PostgreSQL + SQLAlchemy)
* Alembic migration setup
* Core models and services

### Upcoming

* Authentication system (JWT)
* User management APIs
* Trading engine
* AI integration
* Real-time WebSocket features

---

## Development Workflow

```bash id="7k1n9d"
# Create feature branch
git checkout -b feature-name

# Commit changes
git commit -m "Your message"

# Push changes
git push origin feature-name
```

---

## Coding Guidelines

* Follow clean architecture principles
* Keep API, service, and repository layers separate
* Use type hints
* Write modular and reusable code

---

## Notes

* Do not commit `.env` file
* Always use `uv add` to install dependencies
* Keep `pyproject.toml` as the source of truth for dependencies

---

## License

This project is for learning and development purposes.
