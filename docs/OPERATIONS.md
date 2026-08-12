# Operations

## Health

The backend exposes `GET /health` as a lightweight process health endpoint. A deployment platform should additionally verify that the service can reach required dependencies before considering it fully ready.

## Background tasks

The backend starts background tasks for Merkle batching and expired chat-message cleanup. Operational monitoring should alert on repeated task failures and unexpected process restarts.

## Logging

Logs should be structured enough to identify request/operation failures without recording secrets, JWTs, private keys, raw sensitive content, or unnecessary personal data.

## Incident response

1. Confirm the affected component and scope.
2. Preserve relevant logs and commit/deployment identifiers.
3. Contain compromised credentials or access paths.
4. Rotate secrets when exposure is possible.
5. Disable or restrict risky functionality if necessary.
6. Patch and validate the root cause.
7. Record the incident and prevention work.

Security vulnerabilities should follow `SECURITY.md` rather than public issue reporting.

## Recovery

Application rollback is possible for frontend/backend deployments when the previous artifact is available. Database changes require a separate recovery plan. Smart-contract state is immutable and requires a new deployment or migration strategy if incorrect.

## Release evidence

Keep the release commit SHA, application versions, contract address/network, migration notes, configuration changes, and validation results together so an incident can be reconstructed later.
