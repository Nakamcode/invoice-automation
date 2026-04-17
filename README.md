# Invoice Automation

A full-stack invoice management system with a FastAPI backend and React frontend.

## Prerequisites

- Python 3.10+
- Node.js 18+
- npm

---

## Setup

### Backend

```bash
cd backend
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Create a `backend/.env` file to override defaults (all fields optional):

```env
INV_DATABASE_URL=sqlite:///./data/invoices.db
INV_DEFAULT_CURRENCY=CAD
INV_DEFAULT_PAYMENT_TERMS=30
INV_MOCK_EMAIL=true

# SMTP (only needed if INV_MOCK_EMAIL=false)
INV_SMTP_HOST=
INV_SMTP_PORT=587
INV_SMTP_USER=
INV_SMTP_PASSWORD=
INV_SMTP_FROM=invoices@example.com
```

### Frontend

```bash
cd frontend
npm install
```

---

## Dev

Run both servers concurrently in separate terminals.

**Backend** (from `backend/`, with venv active):

```bash
uvicorn app.main:app --reload
```

API is available at `http://localhost:8000`. Interactive docs at `http://localhost:8000/docs`.

**Frontend** (from `frontend/`):

```bash
npm run dev
```

App is available at `http://localhost:5173`. API requests are proxied to the backend automatically.

---

## Test

### Backend unit tests

```bash
cd backend
source .venv/bin/activate
pytest
```

### Frontend end-to-end tests (Playwright)

Requires both the backend and frontend dev servers to be running first.

```bash
cd frontend
npx playwright install --with-deps   # first time only
npm run test:e2e
```

Run with a UI:

```bash
npm run test:e2e:ui
```

---

## Build

### Frontend

```bash
cd frontend
npm run build
```

Output is in `frontend/dist/`.

### Docker

Build and run each service with Docker:

```bash
# Backend
docker build -t invoice-backend ./backend
docker run -p 8000:8000 -v $(pwd)/data:/app/data invoice-backend

# Frontend
docker build -t invoice-frontend ./frontend
docker run -p 80:80 invoice-frontend
```
