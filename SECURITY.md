# Security Policy

SentinelX handles authentication, wallet signatures, transaction risk, sensitive-data detection, and audit records. Please treat security issues as private until they are assessed and fixed.

## Reporting a vulnerability

**Do not open a public GitHub issue for a suspected vulnerability.** Contact the repository maintainer privately through GitHub and include enough information to reproduce the issue safely.

Please include:

- affected component and version/commit;
- vulnerability class and security impact;
- minimal reproduction steps or proof of concept;
- required configuration or assumptions;
- suggested mitigation, if known.

Redact secrets, private keys, credentials, personal data, and production identifiers.

## Response expectations

The maintainer will acknowledge receipt as soon as practical, validate the report, assess impact, and coordinate a fix or mitigation. Disclosure timing should be agreed based on exploitability and user impact.

## Security-sensitive areas

Extra review is required for changes involving:

- SIWE nonces and signature verification;
- JWT/session handling;
- transaction risk and enforcement;
- GuardLayer/DLP rules and LLM integrations;
- audit-event integrity and Merkle proofs;
- smart-contract deployment or authorization;
- private keys, RPC credentials, and environment configuration.

## Supported versions

The `main` branch is the primary supported development line. Released versions are supported according to the release notes for that version.
