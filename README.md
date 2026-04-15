# SmartRoute - AI-Powered Payment Router 🚀

> Intelligent payment routing with ML-powered fraud detection and dynamic gateway optimization

## 🌐 Live Demo

| Service | URL |
|---------|-----|
| **Frontend Dashboard** | [https://smartroute-frontend.onrender.com](https://smartroute-frontend.onrender.com) |
| **Backend API** | [https://smartroute-backend-kxuc.onrender.com](https://smartroute-backend-kxuc.onrender.com) |
| **ML Service** | [https://smartroute-ml.onrender.com](https://smartroute-ml.onrender.com) |

> **Note:** Free-tier services spin down after 15 min of inactivity. First request may take ~30s to cold-start.

## Architecture

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Frontend   │────▶│   Backend   │────▶│ ML Service  │
│  Next.js 14  │     │  Express.js │     │   FastAPI    │
│   :3000      │     │   :5000     │     │   :8000     │
└─────────────┘     └──────┬──────┘     └─────────────┘
                           │
                    ┌──────┴──────┐
                    │             │
              ┌─────┴─────┐ ┌────┴────┐
              │   SQLite   │ │In-Memory│
              │  (local)   │ │  Cache  │
              └───────────┘ └─────────┘
```

## Quick Start

### Local Development

```bash
# Backend
cd backend
npm install
npm run dev          # Express API on :5000

# Frontend
cd frontend
npm install
npm run dev          # Next.js dashboard on :3000

# ML Service
cd ml-service
pip install -r requirements.txt
python main.py       # FastAPI on :8000
```

### Docker (All Services)

```bash
docker-compose up --build

# Services available at:
# Frontend:    http://localhost:3000
# Backend:     http://localhost:5000
# ML Service:  http://localhost:8000
```

## Features

- **🔀 Smart Routing Engine** — Rule-based + ML-powered gateway selection optimizing for cost, speed, and reliability
- **🛡️ Fraud Detection** — Isolation Forest model for real-time anomaly detection with risk scoring
- **📊 Real-Time Dashboard** — Live metrics, gateway performance, and transaction monitoring via WebSocket
- **🏦 Multi-Gateway Support** — Razorpay, Stripe, PayU, Cashfree with simulated processing
- **🧪 A/B Testing** — Compare routing strategies with statistical significance testing
- **📈 Analytics** — Transaction trends, gateway comparison, and cost analysis

## API Endpoints

### Backend (Port 5000)
- `GET  /api/health` — Health check with dependency status
- `GET  /api/transactions` — List transactions (paginated)
- `POST /api/transactions` — Create & process a transaction
- `GET  /api/metrics/summary` — Dashboard KPIs
- `GET  /api/metrics/gateways` — Gateway performance metrics
- `GET  /api/gateways` — List payment gateways
- `WS   /ws` — Real-time transaction feed

### ML Service (Port 8000)
- `GET  /health` — Service health
- `POST /predict/fraud` — Fraud score prediction (Isolation Forest)
- `POST /predict/routing` — Optimal gateway prediction (XGBoost)
- `POST /predict/fraud/batch` — Batch fraud detection
- `POST /train` — Trigger model training
- `GET  /models/status` — Model metadata & status

## Tech Stack

| Service | Technology | Purpose |
|---------|-----------|---------|
| Frontend | Next.js 14 + TypeScript | Dashboard UI |
| Backend | Express.js + TypeScript | API Server |
| ML Service | FastAPI + Python | ML Models |
| Database | SQLite (better-sqlite3) | Data Storage |
| Cache | In-Memory (Map) | Caching Layer |
| Real-time | WebSocket (ws) | Live Updates |
| Deployment | Render.com (Blueprint) | Cloud Hosting |

## Payment Gateways

| Gateway | Success Rate | Avg Latency | Cost | Supported Methods |
|---------|-------------|-------------|------|-------------------|
| Razorpay | 96.5% | 180ms | 2.00% | Cards, UPI, Net Banking, Wallet |
| Stripe | 97.8% | 220ms | 2.90% | Cards, Net Banking, Wallet |
| PayU | 94.2% | 250ms | 1.80% | Cards, UPI, Net Banking, EMI |
| Cashfree | 95.1% | 200ms | 1.95% | Cards, UPI, Net Banking, Wallet |

## Project Structure

```
smart-payment-routing-engine/
├── render.yaml              # Render Blueprint (IaC)
├── docker-compose.yml       # Local Docker setup
├── backend/
│   ├── Dockerfile           # Multi-stage build
│   ├── src/
│   │   ├── server.ts        # Express app entry
│   │   ├── config/
│   │   │   ├── database.ts  # SQLite + schema + seeds
│   │   │   └── redis.ts     # In-memory cache
│   │   ├── routes/
│   │   │   ├── health.ts
│   │   │   ├── transactions.ts
│   │   │   ├── metrics.ts
│   │   │   └── gateways.ts
│   │   ├── services/
│   │   │   ├── routingEngine.ts
│   │   │   ├── gatewaySimulator.ts
│   │   │   ├── transactionProcessor.ts
│   │   │   └── websocket.ts
│   │   └── scripts/
│   │       └── seed.ts
│   └── db/
│       └── init.sql
├── frontend/
│   ├── Dockerfile
│   └── src/
│       ├── app/
│       │   ├── layout.tsx
│       │   ├── page.tsx          # Dashboard
│       │   ├── transactions/
│       │   ├── gateways/
│       │   ├── health/
│       │   ├── fraud/
│       │   ├── routing/
│       │   ├── analytics/
│       │   └── ab-testing/
│       ├── components/
│       │   └── Sidebar.tsx
│       └── lib/
│           └── api.ts
└── ml-service/
    ├── Dockerfile
    ├── requirements.txt
    ├── main.py               # FastAPI app
    └── train_models.py       # Model training script
```

## Deployment

Deployed on **Render.com** via [Blueprint](render.yaml) — push to `main` triggers auto-deploy.

```bash
# One-click deploy
https://render.com/deploy?repo=https://github.com/ronak-kumar06/smart-payment-routing-engine
```

| Service | Runtime | Plan |
|---------|---------|------|
| smartroute-frontend | Node.js | Free |
| smartroute-backend | Docker | Free |
| smartroute-ml | Docker | Free |

## Roadmap

- [x] **Phase 1**: Foundation — Services scaffolded, DB schema, health checks
- [x] **Phase 2**: Core Routing — Gateway simulator, routing engine, transaction processing
- [x] **Phase 3**: ML & Fraud — Isolation Forest, XGBoost, ML integration
- [x] **Phase 4**: Polish — Analytics, WebSocket, A/B testing, deployment
