# Deployment

SentinelX has three deployable application areas: frontend, backend, and smart contracts. Deploy them independently but validate the compatibility between them.

## Pre-deployment checklist

- CI is green on the exact commit being deployed.
- No secrets are present in the repository or build artifacts.
- Database connectivity has been validated.
- CORS origins are production-only and explicit.
- JWT signing secrets are production-grade and stored in a secret manager.
- RPC credentials and contract addresses are correct for the target network.
- Smart-contract changes have been compiled, tested, reviewed, and verified before use.
- Rollback steps are known before deployment.

## Frontend

The frontend is a Vite application and produces a static build with:

```bash
cd frontend
npm ci
npm run build
```

Deploy the resulting `dist/` directory using the chosen static hosting platform. Ensure its public API/WebSocket configuration points to the intended backend.

## Backend

The backend is a FastAPI service. A typical production process is:

```bash
python -m pip install -r backend/requirements.txt
cd backend
uvicorn main:app --host 0.0.0.0 --port 8000
```

Use a process manager/container/orchestrator appropriate to the hosting environment. Termination, restarts, health checks, timeouts, and log collection should be configured outside the application where possible.

## Database

The application expects PostgreSQL through `DATABASE_URL`. Database migrations are not currently represented by a committed migration framework, so schema changes must be treated as a deployment risk and should not be introduced casually. A future migration system should be established before production schema evolution becomes frequent.

## Smart contracts

Contract deployment is network-specific and irreversible once confirmed on-chain. Before deployment:

1. compile and test locally;
2. review the exact Solidity diff;
3. verify constructor/deployer configuration;
4. use a dedicated deployment key;
5. confirm the target network and RPC;
6. record the deployed address and transaction hash;
7. verify the contract source when appropriate.

## Rollback

- Frontend: redeploy the previous known-good build.
- Backend: redeploy the previous known-good application commit/image.
- Database: follow the documented database recovery procedure; do not assume application rollback reverses schema changes.
- Smart contracts: on-chain deployments cannot be rolled back. Use an explicit migration/upgrade strategy if future contracts require one.

## Release record

Record release version, commit SHA, deployed frontend/backend versions, contract address/network, configuration changes, and known issues in the release notes.
