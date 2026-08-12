# Configuration

Configuration is environment-driven. Never commit real credentials.

## Backend variables

| Variable | Purpose | Required |
|---|---|---|
| `SECRET_KEY` | JWT/signing secret | Yes in deployed environments |
| `ALGORITHM` | JWT algorithm, currently `HS256` | Yes |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | JWT lifetime | Yes |
| `OPENROUTER_API_KEY` | Optional LLM provider credential | Only for LLM-backed GuardLayer behavior |
| `SEPOLIA_RPC_URL` | Ethereum Sepolia RPC endpoint | For blockchain operations |
| `DEPLOYER_PRIVATE_KEY` | Contract deployment key | Deployment only; never use in the running app unless explicitly required |
| `AUDIT_CONTRACT_ADDRESS` | Deployed audit contract | For on-chain audit operations |
| `DATABASE_URL` | PostgreSQL connection string | Yes for persistent operation |
| `FRONTEND_URL` | Comma-separated allowed CORS origins | Yes in deployed environments |

The example values live in `backend/.env.example`.

## Frontend configuration

Frontend configuration should use Vite-supported public environment variables only. Never put private keys, JWT signing secrets, database credentials, or provider secrets into browser-exposed variables.

## Contract deployment configuration

Hardhat deployment configuration is under `contracts/`. Deployment credentials must be supplied through environment variables or a secret manager. Never commit a deployer private key.

## Configuration invariants

- Production secrets must differ from local/example values.
- CORS origins should be explicit and minimal.
- RPC endpoints should be HTTPS where supported.
- JWT signing secrets must be high-entropy and rotated through an operational process.
- Database credentials must use least-privilege accounts.
- Optional external providers should fail safely when unavailable.
