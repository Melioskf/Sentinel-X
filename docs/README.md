# SentinelX Engineering Documentation

This directory is the engineering source of truth for how SentinelX is built, tested, operated, and changed.

## Start here

| Document | Purpose |
|---|---|
| [Architecture](ARCHITECTURE.md) | System boundaries, components, data flow, and trust boundaries |
| [Development](DEVELOPMENT.md) | Local setup and day-to-day development |
| [API](API.md) | Backend HTTP/WebSocket surface and conventions |
| [Configuration](CONFIGURATION.md) | Environment variables and configuration rules |
| [Deployment](DEPLOYMENT.md) | Deployment, release, and rollback guidance |
| [Testing](TESTING.md) | Validation strategy and current test coverage |
| [Security](SECURITY.md) | Security engineering expectations |
| [Threat Model](THREAT_MODEL.md) | Assets, threats, trust boundaries, and mitigations |
| [Operations](OPERATIONS.md) | Health checks, incidents, observability, and recovery |
| [Workflow](WORKFLOW.md) | Branching, commits, PRs, reviews, and releases |
| [ADR index](adr/README.md) | Architectural decisions and their rationale |

## Existing project documents

The repository also contains older project documents such as `project_discription.md`, `update.md`, and `walkthrough.md`. They are retained for historical context. New engineering decisions and operational instructions should be recorded under `docs/`.

## Documentation rule

When code changes the externally observable behavior, configuration, API, architecture, security model, or operational procedure, update the relevant documentation in the same change.
