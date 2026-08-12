# Architecture

SentinelX is a multi-component Web3 security platform. The current repository is organized as a React/Vite frontend, FastAPI backend, Hardhat smart-contract project, and JavaScript SDK.

## System context

```text
Browser / Web3 wallet
        |
        v
  React + Vite frontend
        |
        | HTTP / WebSocket
        v
  FastAPI backend
   |      |       |       |
   |      |       |       +--> OpenRouter (optional LLM analysis)
   |      |       +----------> PostgreSQL
   |      +------------------> Risk / Guard / Enforcement services
   +-------------------------> Merkle audit batching
                                  |
                                  v
                         Ethereum Sepolia contract
```

## Components

### Frontend

`frontend/` contains the browser application. It provides wallet authentication, dashboards, audit views, GuardLayer views, transaction-risk flows, simulation, and real-time chat. Vite serves development on port `5173` by default.

### Backend

`backend/` contains the FastAPI application. Routers define HTTP/WebSocket boundaries; services contain risk, enforcement, JWT, Merkle, and transaction-risk logic; SQLAlchemy models represent persistent state.

### Smart contracts

`contracts/` is a Hardhat project containing `AuditProofBatch.sol` and deployment tooling. The current design stores Merkle batch roots on Ethereum Sepolia rather than every raw event.

### SDK

`sdk/` contains browser-side integration assets for applications embedding SentinelX security capabilities.

## Backend layering

```text
HTTP / WebSocket routers
        |
        v
Domain services
        |
        +--> risk engine
        +--> transaction risk
        +--> GuardLayer / enforcement
        +--> JWT utilities
        +--> Merkle batching
        |
        v
Persistence / external providers
        |
        +--> PostgreSQL
        +--> OpenRouter (optional)
        +--> Ethereum Sepolia
```

Routers should remain thin: validate inputs, enforce request-level authorization, call domain services, and translate results into API responses. Business logic should not be duplicated across routers.

## Trust boundaries

1. **Browser boundary:** all browser input is untrusted.
2. **Wallet boundary:** signatures prove control of an address but do not automatically establish application authorization.
3. **API boundary:** every request must be treated as untrusted until authentication, authorization, and validation succeed.
4. **LLM boundary:** LLM output is advisory/untrusted and must not be treated as an authorization decision by itself.
5. **Database boundary:** persisted security events and user state require integrity and least-privilege access.
6. **Blockchain boundary:** on-chain state is public and immutable; no secret or sensitive raw payload should be written to the chain.

## Key flows

### Authentication

1. Client requests/receives a nonce.
2. Wallet signs the SIWE message.
3. Backend validates the nonce, signature, domain/context, and wallet address.
4. Backend creates a JWT session.
5. Login context is persisted for risk evaluation.
6. Elevated risk may trigger step-up authentication.

### Risk evaluation

Login risk is history-aware and explainable. Current factors include new device/browser, new location, rapid attempts, and unusual login time. Scores are normalized and classified into low, medium, and high risk.

### GuardLayer

Content passes through local sensitive-data detection and may optionally be evaluated by an LLM through OpenRouter. Enforcement decisions must remain deterministic and policy-driven; an LLM should not be the sole authorization mechanism.

### Transaction risk

Transaction context is evaluated before sensitive Web3 actions. Risk factors and enforcement outcomes are returned to the caller and recorded as security events where appropriate.

### Audit trail

Security events can be batched into a Merkle tree. The batch root is anchored on-chain. This gives tamper-evident proof without requiring raw event payloads to be stored publicly on Ethereum.

## Design principles

- Least privilege.
- Explicit trust boundaries.
- Explainable security decisions.
- Deterministic enforcement around probabilistic/advisory components.
- No secrets in source control.
- Documentation changes ship with behavior changes.
- Prefer small, reversible changes.
