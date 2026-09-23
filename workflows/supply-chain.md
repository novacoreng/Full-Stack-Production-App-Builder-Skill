# Software Supply Chain and Secure Delivery

Use a risk-based software supply-chain process. The goal is to reduce vulnerabilities and improve traceability from source to deployed artifact.

## Pre-build

- pin or lock dependencies where supported;
- inspect lockfile changes;
- scan for known vulnerable dependencies;
- detect accidental secrets;
- review dependency licenses where the product requires it;
- prefer maintained packages with clear provenance;
- minimize unnecessary dependencies;
- verify package manager and runtime versions;
- review install/build scripts for unexpected behavior.

## Build and CI/CD

Where applicable:
- run lint/typecheck/tests;
- run SAST;
- run dependency/SCA scanning;
- run secret scanning;
- generate an SBOM or dependency inventory;
- scan containers/images when containers are used;
- use protected CI/CD environments for production;
- avoid broad long-lived CI credentials;
- use least-privilege deployment identities;
- keep production deployment credentials out of pull requests from untrusted forks;
- record artifact/build provenance when supported.

## Release

Before release:
- verify the commit/artifact being deployed;
- verify migrations and rollback plan;
- verify release configuration;
- verify environment-specific secrets;
- perform smoke tests;
- retain the artifact/version needed for rollback;
- document release evidence.

## Runtime

Monitor:
- dependency/security alerts;
- abnormal errors;
- authentication/authorization failures;
- resource exhaustion;
- unexpected outbound calls;
- suspicious administrative actions.

Patch or rotate affected components according to risk.

Never claim a formal security certification merely because these checks were run.
