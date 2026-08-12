# Security Engineering

## Security priorities

1. Authentication and session integrity.
2. Authorization and transaction enforcement.
3. Secret and key protection.
4. Sensitive-data handling.
5. Audit integrity.
6. Smart-contract safety.
7. Supply-chain and CI security.

## Secure coding rules

- Validate all client-controlled input at the API boundary.
- Do not trust wallet ownership as proof of authorization for every action.
- Treat LLM output as untrusted advisory data.
- Never use user-provided text to construct SQL, shell commands, code, or contract calls without strict validation.
- Do not log secrets, JWTs, private keys, or sensitive personal data.
- Use least-privilege database and cloud credentials.
- Keep CORS origins explicit.
- Prefer dependency lockfiles and automated dependency/security updates.
- Review workflow permission scopes and third-party Actions before use.

## Authentication-specific controls

SIWE flows must protect nonce uniqueness, signature verification, domain/URI context, replay resistance, and session lifecycle. JWT signing secrets must never be client-exposed.

## Transaction controls

A transaction-risk score is an input to policy, not a substitute for authorization. High-risk actions should have deterministic enforcement and, where appropriate, step-up authentication.

## GuardLayer

Regex/pattern checks are deterministic. LLM checks are probabilistic and may be unavailable or manipulated by prompt injection. LLM output must therefore be constrained to advisory classification and must not directly grant privileged access.

## Audit trail

Merkle roots provide integrity evidence, but the system must protect the source events and batching process as well. Public-chain data should contain only information intentionally made public.

## CI/CD

GitHub Actions use explicit `GITHUB_TOKEN` permissions. Dependency automation and CodeQL are enabled through repository configuration. Workflow changes should receive CODEOWNERS review.
