# Threat Model

This is a living threat model. Update it when authentication, transaction, DLP, audit, or deployment architecture changes.

## Assets

- Wallet identities and signed authentication messages.
- JWT/session credentials.
- User/account records.
- Security events and risk history.
- Sensitive content submitted to GuardLayer.
- Transaction intent and policy decisions.
- Merkle batch state and proof material.
- Deployment credentials and RPC access.
- Smart-contract administrative authority.

## Trust boundaries

| Boundary | Primary risk |
|---|---|
| Browser → API | Forged input, CSRF/CORS mistakes, token theft |
| Wallet → API | Replay, malformed signatures, incorrect identity binding |
| API → database | Injection, over-privileged credentials, data leakage |
| API → LLM provider | Sensitive-data disclosure, prompt injection, unreliable output |
| API → blockchain | Wrong network, key compromise, irreversible writes |
| CI → deployment | Supply-chain compromise, workflow token abuse |

## Threats and mitigations

### Account takeover

**Threat:** stolen JWT, replayed SIWE message, or nonce reuse.

**Mitigations:** short-lived sessions, secure nonce handling, signature/domain validation, HTTPS, and careful client storage.

### Transaction abuse

**Threat:** a valid wallet session is used to perform an unintended or high-risk transaction.

**Mitigations:** transaction risk analysis, explicit policy enforcement, step-up authentication, and auditable security events.

### Prompt injection / DLP bypass

**Threat:** attacker-crafted content causes an LLM-backed scanner to misclassify sensitive content.

**Mitigations:** deterministic local checks, constrained LLM role, policy-based enforcement, and fail-safe behavior when the provider is unavailable.

### Audit tampering

**Threat:** database records are modified after the fact.

**Mitigations:** Merkle batching and on-chain root anchoring, plus protection of the off-chain source data and batch process.

### Supply-chain compromise

**Threat:** malicious dependency or GitHub Action enters the build.

**Mitigations:** Dependabot, CodeQL, lockfiles where available, minimal workflow permissions, review of workflow changes, and reproducible CI.

### Secret exposure

**Threat:** credentials are committed or leaked through logs/build artifacts.

**Mitigations:** environment-based secrets, `.gitignore`, GitHub secret scanning/push protection where enabled, log hygiene, and deployment secret managers.

## Residual risk

No risk score or scanner eliminates compromise. SentinelX should be treated as a defense-in-depth layer rather than a guarantee of security. Operational monitoring and secure wallet/key practices remain necessary.
