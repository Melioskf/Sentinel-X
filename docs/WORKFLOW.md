# Engineering Workflow

This repository uses a lightweight trunk-based workflow with short-lived branches and pull requests.

## 1. Start from main

```bash
git checkout main
git pull --ff-only origin main
git checkout -b <type>/<short-description>
```

Recommended types: `feat`, `fix`, `security`, `docs`, `refactor`, `chore`, `test`, `ci`.

## 2. Make one coherent change

Keep a branch focused. Avoid mixing unrelated formatting, dependency upgrades, feature work, and refactors.

## 3. Validate locally

Run the checks relevant to the changed component. For security-sensitive changes, follow the additional manual checks in `docs/TESTING.md`.

## 4. Commit clearly

Prefer small commits with descriptive prefixes. Keep secrets and generated build output out of commits.

## 5. Open a pull request

The PR should explain the problem, implementation, validation, security/data impact, breaking changes, and follow-up work. Link issues where applicable.

## 6. Review

CODEOWNERS identifies the maintainer responsible for repository areas. Security-sensitive changes should receive deliberate review even when the diff is small.

## 7. CI

CI runs backend, frontend, and smart-contract checks. CodeQL provides static security analysis. Dependency updates are proposed through Dependabot.

## 8. Merge

Prefer squash merges for focused changes unless a different strategy is intentionally chosen. Delete merged branches when the repository settings support it.

## 9. Release

For a release:

1. ensure CI is green;
2. update `CHANGELOG.md`;
3. update version metadata where the component uses explicit versions;
4. verify deployment configuration;
5. deploy backend/frontend;
6. deploy/verify contracts only when required;
7. record commit SHA and deployment identifiers;
8. publish release notes.

## Hotfixes

Security or production hotfixes may use a short path to production, but should still receive review, CI validation, changelog/documentation updates, and a follow-up issue if normal process was bypassed.
