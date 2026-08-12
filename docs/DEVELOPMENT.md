# Development

## Prerequisites

- Git
- Python 3.12 recommended for backend development
- Node.js 20 recommended for frontend and contracts
- PostgreSQL for database-backed development
- A Web3 wallet such as MetaMask for wallet flows
- Optional OpenRouter API key for LLM-backed GuardLayer behavior
- Optional Sepolia RPC credentials for blockchain integration

## Repository layout

```text
backend/      FastAPI application
frontend/     React + Vite application
contracts/    Hardhat smart contracts
sdk/          JavaScript integration SDK
docs/         Engineering and operational documentation
.github/      CI, dependency automation, issue/PR templates
```

## Backend

```bash
cd backend
python -m venv .venv
# activate the virtual environment
python -m pip install -r requirements.txt
cp .env.example .env
uvicorn main:app --reload --port 8000
```

Do not commit `.env`. Use `backend/.env.example` as the configuration contract.

## Frontend

```bash
cd frontend
npm ci
npm run dev
```

Vite serves the application at `http://localhost:5173` unless overridden.

## Smart contracts

The current contract project does not contain a committed `package-lock.json`, so use `npm install` rather than `npm ci` there until a lockfile is intentionally introduced.

```bash
cd contracts
npm install
npm run compile
npm test
```

Deployment to Sepolia requires the environment variables described in `docs/CONFIGURATION.md` and should never use a production/private key from source control.

## SDK

Review the SDK source before changing its public API. Keep browser-facing integration code independent from backend-only secrets and credentials.

## Local development rules

- Keep backend, frontend, and contract changes independently testable.
- Prefer environment variables over hard-coded endpoints.
- Never use real production data for local testing.
- Use synthetic wallets, accounts, and test credentials.
- When changing security logic, document the expected threat and validation in the PR.
