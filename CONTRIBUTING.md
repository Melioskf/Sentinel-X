# Contributing to SentinelX

Thank you for contributing. SentinelX is a security-sensitive Web3 application, so changes should be small, reviewable, tested, and explicit about security impact.

## Before you start

1. Read `docs/DEVELOPMENT.md` for local setup.
2. Read `docs/WORKFLOW.md` for the branch, commit, review, and release workflow.
3. Read `SECURITY.md` before reporting a vulnerability.
4. Search existing issues and pull requests before opening new work.

## Development rules

- Prefer focused branches such as `feat/...`, `fix/...`, `docs/...`, `chore/...`, or `security/...`.
- Keep unrelated refactors out of feature fixes.
- Never commit secrets, private keys, wallet seed phrases, access tokens, production credentials, or real user data.
- Treat authentication, authorization, transaction controls, DLP/GuardLayer, audit logging, and smart contracts as security-sensitive code.
- Update documentation when behavior, configuration, APIs, architecture, or operational procedures change.
- Add or update tests when behavior changes. If a test cannot reasonably be added, explain why in the PR.

## Validation

At minimum, run the checks relevant to your change:

```text
Backend:   python -m compileall -q backend
Frontend:  cd frontend && npm ci && npm run build
Contracts: cd contracts && npm install && npm run compile && npm test
```

Also perform the manual checks described in `docs/TESTING.md` when touching authentication, transactions, GuardLayer, audit trails, or deployment configuration.

## Pull requests

A PR should explain:

- what changed;
- why it changed;
- how it was validated;
- security/data implications;
- breaking changes;
- follow-up work, if any.

CI should be green before merge. Reviewers may request changes for correctness, security, maintainability, or documentation gaps.

## Commit messages

Use concise conventional prefixes where practical:

- `feat:` new behavior
- `fix:` bug fix
- `docs:` documentation
- `chore:` maintenance/tooling
- `refactor:` behavior-preserving restructuring
- `test:` tests
- `security:` security hardening or vulnerability remediation
- `ci:` CI/CD changes

## Security-sensitive changes

For changes affecting authentication, JWT handling, wallet signatures, transaction enforcement, smart contracts, secrets, DLP, or audit integrity, explicitly document the threat being addressed and the validation performed. Do not disclose exploitable vulnerability details in a public issue.
