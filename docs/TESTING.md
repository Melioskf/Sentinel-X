# Testing

## Current state

The repository currently has a strong build/syntax baseline but limited committed automated application tests. This document makes that gap explicit rather than claiming coverage that does not exist.

## CI checks

The CI workflow validates:

- Python compilation for the backend;
- frontend dependency installation and production build;
- Hardhat contract compilation and test command.

CodeQL performs static security analysis for JavaScript and Python.

## Test layers

### Unit tests

Add unit tests around deterministic security logic first:

- risk-factor calculation and thresholds;
- transaction-risk scoring;
- GuardLayer pattern matching;
- JWT utilities;
- Merkle tree construction/proof verification;
- enforcement decisions.

### API tests

Use FastAPI's test client or HTTPX to cover authentication, authorization, validation, and error behavior. Database tests should use isolated test data and never production credentials.

### Frontend tests

Add component/page tests for authentication state, risk presentation, transaction warnings, GuardLayer results, and failure states before introducing large UI refactors.

### Smart-contract tests

Every externally callable contract behavior should have Hardhat tests for success, invalid input, authorization, event emission, and relevant edge cases.

### Integration tests

Critical cross-component flows should eventually cover:

1. wallet authentication → risk evaluation → session creation;
2. protected transaction → risk evaluation → enforcement;
3. security event → Merkle batch → proof/anchor verification;
4. chat message → GuardLayer → persistence/expiration.

## Security regression tests

Every confirmed security issue should result in a regression test where practical. The test should demonstrate the vulnerable behavior is no longer possible.

## Manual smoke test

Before a demo/release, verify:

- wallet login works;
- high-risk login triggers the intended step-up behavior;
- GuardLayer blocks or flags representative sensitive content;
- transaction-risk UI shows the expected decision;
- dashboard data loads;
- audit records are visible and proof flow works when configured;
- chat connects, handles expiry, and rejects invalid sessions;
- simulation scenarios execute without corrupting real data.
