<p align="center">
  <img src="https://img.shields.io/badge/SentinelX-Web3_Security-10b981?style=for-the-badge&logo=ethereum&logoColor=white" alt="SentinelX" />
</p>

<h1 align="center">🛡️ SentinelX</h1>

<p align="center">
  <strong>Adaptive Security Platform for Web3</strong><br/>
  <em>Wallet authentication · Adaptive risk scoring · Data leak prevention · Transaction protection · On-chain audit trails</em>
</p>

<p align="center">
  <a href="#-features"><img src="https://img.shields.io/badge/Features-9-emerald?style=flat-square" alt="Features" /></a>
  <a href="#-quick-start"><img src="https://img.shields.io/badge/Quick_Start-5_min-blue?style=flat-square" alt="Quick Start" /></a>
  <a href="https://sepolia.etherscan.io"><img src="https://img.shields.io/badge/Network-Sepolia-purple?style=flat-square" alt="Sepolia" /></a>
  <a href="#-license"><img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License" /></a>
</p>

<p align="center">
  <a href="https://github.com/Melioskf/Sentinel-X">
    <img src="https://img.shields.io/github/stars/Melioskf/Sentinel-X?style=social" alt="GitHub Stars" />
  </a>
</p>

---

## 🎯 What is SentinelX?

**SentinelX** is an adaptive security platform for Web3 applications. It combines wallet-based authentication, history-aware risk scoring, data leak prevention, transaction risk analysis, real-time security telemetry, and tamper-evident audit trails.

The platform is designed around a simple principle:

> **Authenticate the user, evaluate the context, protect the action, and preserve an auditable security trail.**

### Core capabilities

- 🔐 **Passwordless wallet authentication** using Sign-In with Ethereum (SIWE)
- 🧠 **Adaptive risk scoring** based on login history and behavioral signals
- 🛡️ **GuardLayer DLP** using local pattern detection with optional LLM analysis
- 💸 **Transaction risk analysis** for Web3 actions before execution
- ⛓️ **Merkle-batched audit trails** with Ethereum Sepolia anchoring
- 📊 **Live security dashboard** with risk, login, audit, and activity telemetry
- 🚨 **Step-up authentication** for elevated-risk sessions
- 💬 **Real-time secure chat** with expiring messages and GuardLayer protection
- 🎮 **Attack Simulation Lab** for demonstrating defensive controls

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🔑 SIWE Wallet Authentication
Passwordless authentication with **Sign-In with Ethereum (EIP-4361)**.

- Wallet-based login
- JWT session management
- Nonce validation
- MetaMask / WalletConnect-compatible wallet flow
- Login context and geographic metadata

</td>
<td width="50%">

### 🧠 Adaptive Risk Engine
History-aware login risk scoring using graduated behavioral factors:

- New device / browser
- New geographic location
- Rapid login attempts
- Unusual login time
- Explainable factor contributions

Risk is normalized to **0–1** and classified as **low, medium, or high**.

</td>
</tr>
<tr>
<td width="50%">

### 🛡️ GuardLayer DLP
Multi-layer protection for sensitive content:

- Local pattern/regex scanning
- Optional OpenRouter LLM analysis
- Sensitive-data detection
- User override tracking
- Enforcement hooks for protected content

</td>
<td width="50%">

### 💸 Transaction Risk Engine
Evaluate Web3 transaction context before sensitive actions:

- Transaction risk scoring
- Risk-factor explanations
- Policy/enforcement integration
- Security events for high-risk activity

</td>
</tr>
<tr>
<td width="50%">

### ⛓️ Merkle Audit Trail
Security events can be grouped into Merkle batches and anchored on **Ethereum Sepolia**.

- Gas-efficient root storage
- Batch event counts and timestamps
- Inclusion-proof verification
- No raw security-event payloads required on-chain

</td>
<td width="50%">

### 📊 Security Dashboard
Centralized visibility into the security posture:

- Risk timeline
- Login-origin map
- Recent security events
- Trust / risk indicators
- Security reports

</td>
</tr>
<tr>
<td width="50%">

### 🚨 Step-Up Authentication
Adaptive friction when a login crosses a configured risk threshold:

- Secondary wallet signature
- Trust-score updates
- Configurable challenge flow
- Restricted access when verification is skipped

</td>
<td width="50%">

### 💬 Secure Real-Time Chat
Security-aware messaging integrated with the platform:

- WebSocket-based communication
- GuardLayer scanning
- Message expiration / cleanup
- Protected conversation flow

</td>
</tr>
<tr>
<td width="50%">

### 🎮 Attack Simulation Lab
Demonstrate the security controls with repeatable scenarios:

- Suspicious login attempts
- Data-leak attempts
- Burst / rapid-login patterns
- Transaction-risk scenarios
- Demo-data generation

</td>
<td width="50%">

### 📦 JavaScript SDK
The SDK provides integration building blocks for applications that want to embed SentinelX security controls.

- Authentication integration
- GuardLayer integration
- Configurable policies
- Event callbacks

</td>
</tr>
</table>

---

## 🏗️ Architecture

```text
┌─────────────────────────────────────────────────────────────────────┐
│                    FRONTEND (React + Vite)                          │
│                                                                     │
│  Wallet Auth │ Dashboard │ GuardLayer │ Chat │ Simulation │ Txns    │
└──────────────────────────────┬──────────────────────────────────────┘
                               │ HTTP / WebSocket
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       BACKEND (FastAPI)                             │
│                                                                     │
│  SIWE + JWT        Adaptive Risk Engine        GuardLayer DLP       │
│  Transaction Risk  Dashboard / Reports         Chat / WebSockets    │
│  Simulation        Merkle Audit Batcher        Enforcement          │
└───────────────┬──────────────────────────────┬─────────────────────┘
                │                              │
                ▼                              ▼
┌───────────────────────────┐      ┌─────────────────────────────────┐
│ PostgreSQL / SQLAlchemy   │      │ Ethereum Sepolia                │
│                           │      │                                 │
│ Users, sessions, login    │      │ AuditProofBatch.sol             │
│ events, messages, audits  │      │ Stores Merkle roots + metadata  │
└───────────────────────────┘      └─────────────────────────────────┘
```

The backend starts background tasks for **Merkle batching** and **expired-message cleanup**. The blockchain layer stores batch roots and metadata rather than raw application/security data.

---

## 🚀 Quick Start

### Prerequisites

| Requirement | Version / Notes |
|-------------|-----------------|
| Python | 3.10+ recommended |
| Node.js | 18+ |
| PostgreSQL | Required for the backend database |
| MetaMask | Optional for wallet flows |
| Sepolia RPC | Required only for on-chain deployment/use |

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/Melioskf/Sentinel-X.git
cd Sentinel-X
```

### 2️⃣ Backend Setup

```bash
cd backend

python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
# source venv/bin/activate

pip install -r requirements.txt

# Copy the environment template and configure it
# Windows:
copy .env.example .env
# macOS / Linux:
# cp .env.example .env

uvicorn main:app --reload --port 8000
```

Backend endpoints are available at **http://localhost:8000**.

FastAPI's interactive API documentation is available at **http://localhost:8000/docs**.

Health check: **http://localhost:8000/health**

### 3️⃣ Frontend Setup

Open a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Vite is configured to serve the frontend at **http://localhost:5173** and proxy `/api` requests to the backend on port `8000`.

### 4️⃣ Smart Contracts (Optional)

```bash
cd contracts
npm install
npx hardhat compile

# Deploy to Sepolia after configuring your RPC URL/private key
npx hardhat run scripts/deploy.js --network sepolia
```

After deployment, set `AUDIT_CONTRACT_ADDRESS` in the backend environment.

### 5️⃣ SDK

If you are working on the SDK package, install and build it from its directory:

```bash
cd sdk
npm install
npm run build
```

---

## ⚙️ Environment Configuration

The backend reads configuration from environment variables. Start with `backend/.env.example`.

| Variable | Purpose |
|----------|---------|
| `SECRET_KEY` | JWT signing secret |
| `ALGORITHM` | JWT algorithm, e.g. `HS256` |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | JWT lifetime |
| `OPENROUTER_API_KEY` | Optional LLM access for GuardLayer |
| `SEPOLIA_RPC_URL` | Ethereum Sepolia RPC endpoint |
| `DEPLOYER_PRIVATE_KEY` | Contract deployment key |
| `AUDIT_CONTRACT_ADDRESS` | Deployed `AuditProofBatch` address |
| `DATABASE_URL` | PostgreSQL connection string |
| `FRONTEND_URL` | Allowed frontend origin(s) |

**Never commit real API keys, private keys, JWT secrets, or database credentials.**

---

## 🎮 Demo Walkthrough

1. Start the backend on `localhost:8000`.
2. Start the frontend on `localhost:5173`.
3. Open the SentinelX dashboard.
4. Authenticate with the wallet flow or use the application's demo path when available.
5. Seed demo data from the dashboard if you want sample telemetry.
6. Inspect the risk timeline and login-origin data.
7. Test GuardLayer with sensitive-looking text.
8. Run an attack scenario in the Simulation Lab.
9. Test transaction-risk analysis for Web3 actions.
10. Inspect audit batches and verify Merkle inclusion proofs.

---

## 🔌 API Reference

All routers are mounted by the FastAPI application under the prefixes below. For request/response schemas, use **`/docs`** while the backend is running.

### Authentication — `/auth`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/auth/nonce` | GET | Generate a SIWE nonce |
| `/auth/verify` | POST | Verify wallet signature and evaluate login risk |
| `/auth/session` | GET | Check the current JWT session |
| `/auth/challenge` | POST | Request a step-up challenge |
| `/auth/step-up/verify` | POST | Verify the step-up signature |

### Risk Intelligence — `/risk`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/risk/score` | POST | Calculate login risk |
| `/risk/timeline` | GET | Retrieve risk history |
| `/risk/map` | GET | Retrieve login-origin coordinates |

### GuardLayer — `/guard`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/guard/scan` | POST | Scan content for sensitive data |
| `/guard/override` | POST | Record a user override |

### Audit Trail — `/audit`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/audit/batches` | GET | List Merkle batches |
| `/audit/batch` | POST | Force creation of a batch |
| `/audit/verify` | POST | Verify a Merkle inclusion proof |
| `/audit/pending` | GET | List pending audit events |

### Dashboard — `/dashboard`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/dashboard/overview` | GET | Aggregated security dashboard data |
| `/dashboard/security-report` | GET | Generate a security report |
| `/dashboard/seed` | POST | Seed demo data |

### Simulation — `/simulation`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/simulation/scenarios` | GET | List available scenarios |
| `/simulation/run` | POST | Execute a simulation scenario |

### Chat — `/chat`

The chat router provides real-time messaging and GuardLayer-aware message handling. Use **`/docs`** for the current HTTP endpoints and WebSocket contract.

### Transactions — `/transactions`

The transaction router provides transaction-risk evaluation and related security controls. Use **`/docs`** for the current request/response schemas.

### System

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Backend status and enabled modules |
| `/health` | GET | Health check |

---

## 🛠️ Tech Stack

<table>
<tr>
<td align="center" width="25%">

**Backend**

Python 3.10+<br/>
FastAPI<br/>
SQLAlchemy 2<br/>
PostgreSQL / asyncpg<br/>
OpenAI-compatible OpenRouter API

</td>
<td align="center" width="25%">

**Frontend**

React 18<br/>
Vite<br/>
TailwindCSS<br/>
Recharts<br/>
React-Leaflet<br/>
Wagmi / Viem / RainbowKit

</td>
<td align="center" width="25%">

**Blockchain**

Solidity 0.8.19+<br/>
Hardhat<br/>
Ethers.js<br/>
Ethereum Sepolia

</td>
<td align="center" width="25%">

**SDK**

JavaScript<br/>
esbuild<br/>
Authentication<br/>
GuardLayer integration

</td>
</tr>
</table>

---

## 🔐 Security & Privacy

| Category | Current approach |
|----------|------------------|
| **Authentication** | SIWE nonce validation + JWT sessions |
| **Login Risk** | History-aware weighted scoring with explainable factors |
| **Content Scanning** | Local detection first; optional LLM analysis |
| **Transaction Protection** | Dedicated transaction-risk service and router |
| **Audit Storage** | Merkle roots and batch metadata on-chain |
| **Messages** | Expiration and background cleanup |
| **Secrets** | Environment variables; keep production secrets out of Git |

### Important deployment note

SentinelX is a security platform/demo, but it should not be treated as production-hardened solely from the README. Before production deployment, review authentication, secret management, database security, CORS, rate limiting, wallet/transaction policies, smart-contract ownership, RPC security, and audit-log integrity.

---

## 📁 Project Structure

```text
Sentinel-X/
├── backend/
│   ├── app/
│   │   ├── models/             # SQLAlchemy models
│   │   ├── routers/            # API / WebSocket routes
│   │   │   ├── auth.py
│   │   │   ├── risk.py
│   │   │   ├── guard.py
│   │   │   ├── audit.py
│   │   │   ├── simulation.py
│   │   │   ├── dashboard.py
│   │   │   ├── chat.py
│   │   │   └── transactions.py
│   │   └── services/            # Core security/business logic
│   │       ├── enforcement.py
│   │       ├── guard_layer.py
│   │       ├── jwt_utils.py
│   │       ├── merkle.py
│   │       ├── risk_engine.py
│   │       └── transaction_risk.py
│   ├── main.py                  # FastAPI application
│   ├── requirements.txt
│   ├── runtime.txt
│   └── .env.example
│
├── frontend/
│   ├── src/                     # React application
│   ├── public/
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── vercel.json
│
├── contracts/
│   ├── contracts/
│   │   └── AuditProofBatch.sol
│   ├── scripts/
│   │   └── deploy.js
│   ├── hardhat.config.js
│   └── package.json
│
├── sdk/                         # JavaScript SDK
└── readme.md
```

---

## 🤝 Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/my-feature
   ```
3. Make and test your changes.
4. Commit with a clear message:
   ```bash
   git commit -m "Add my feature"
   ```
5. Push the branch and open a Pull Request.

For security-sensitive changes, include the threat model, affected trust boundaries, and test coverage in the PR description.

---

## 📄 License

This project is licensed under the **MIT License** — see the `LICENSE` file for details.

---

<p align="center">
  <strong>Built with ❤️ for the Web3 security community</strong><br/>
  <a href="https://github.com/Melioskf/Sentinel-X">⭐ Star this repo</a> ·
  <a href="https://github.com/Melioskf/Sentinel-X/issues">🐛 Report Bug</a> ·
  <a href="https://github.com/Melioskf/Sentinel-X/issues">💡 Request Feature</a>
</p>

---

<p align="center">
  <img src="https://img.shields.io/badge/Made_with-FastAPI-009688?style=flat-square&logo=fastapi" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Made_with-React-61DAFB?style=flat-square&logo=react" alt="React" />
  <img src="https://img.shields.io/badge/Made_with-Ethereum-3C3C3D?style=flat-square&logo=ethereum" alt="Ethereum" />
  <img src="https://img.shields.io/badge/Made_with-TailwindCSS-38B2AC?style=flat-square&logo=tailwind-css" alt="TailwindCSS" />
</p>
