# API

The backend is a FastAPI application. It exposes interactive OpenAPI documentation when the server is running:

- Swagger UI: `/docs`
- ReDoc: `/redoc`
- OpenAPI schema: `/openapi.json`

## Base endpoints

- `GET /` — service metadata and enabled modules.
- `GET /health` — lightweight health endpoint.

## Route groups

The application currently mounts these routers:

| Prefix | Responsibility |
|---|---|
| `/auth` | SIWE wallet authentication and session flows |
| `/risk` | Login risk evaluation and risk telemetry |
| `/guard` | GuardLayer/DLP scanning and enforcement |
| `/audit` | Security audit events and Merkle audit operations |
| `/simulation` | Security/attack simulation scenarios |
| `/dashboard` | Security dashboard data |
| `/chat` | Real-time and persisted secure chat |
| `/transactions` | Transaction risk analysis and enforcement |

The authoritative endpoint definitions are the router source files under `backend/app/routers/`. This document intentionally describes stable route groups rather than duplicating every generated schema field.

## Authentication

Authentication uses wallet signatures and JWT sessions. Treat JWTs as credentials. Clients must not expose tokens in logs, URLs, screenshots, or analytics payloads.

## Error handling

Clients should treat non-2xx responses as failures and avoid assuming that an error body is safe to display verbatim. Security-sensitive errors should not disclose internal stack traces, secrets, or authorization details.

## WebSocket

The chat module uses WebSocket communication. WebSocket clients must authenticate according to the current chat router contract and must handle disconnects, expiration, and server-side rejection.

## API change policy

Changes to request/response contracts should:

1. update the backend implementation;
2. update frontend/SDK consumers;
3. update this documentation when the public behavior changes;
4. add regression coverage where feasible;
5. call out breaking changes in the PR and changelog.
