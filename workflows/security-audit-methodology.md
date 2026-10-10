# Security Audit Methodology Integration

Adapted from the user-provided Cloudflare security-audit skill (MIT license, copyright 2025-2026 Cloudflare, Inc.).

## Modes
Guidance mode covers focused security questions and reviews. Full audit mode is for explicit comprehensive audit, penetration-test or audit-report requests. Do not start a full audit merely because security guidance is relevant.

## Safe audit execution
Source inspection is read-only by default. Run target-controlled builds, tests or fuzzers only inside a properly isolated, resource-limited sandbox with no external network, allowlisted environment, read-only target and scratch-only writes. If that isolation is unavailable, do not run untrusted code; mark NEEDS VALIDATION. Avoid probing live services, real users, production accounts and paid providers.

## Coverage
Inventory attack surfaces and trust boundaries. Assess applicable web authentication, authorization, client-side, cloud/deployment, data isolation/lifecycle, desktop/mobile/IPC, RPC/messaging, resource exhaustion, supply chain, memory safety/native binaries, AI/LLM, and other attack classes.

## Findings
Use source-first evidence. A confirmed vulnerability requires a concrete affected principal/resource, violated trust boundary and security outcome. Distinguish severity from confidence and CONFIRMED from NEEDS VALIDATION. Independently validate candidates where safely possible. Track coverage, safe reproduction, affected versions, minimal fixes and regression tests. Do not equate zero findings with security.

## Reporting
For full audits, produce architecture, coverage ledger, findings, detailed evidence, unresolved validation and remediation priorities. Keep artifacts outside the audited repository by default. Avoid secrets and unsafe artifact promotion. Follow existing `workflows/security.md` and the strict workflow applicability gate.

The uploaded source also includes detailed modules for reconnaissance, hunting, attack classes, web protocols, client-side, cloud, data isolation, desktop/mobile IPC, RPC, availability, supply chain, binary/memory safety, AI/LLM and validation, plus report schema and validators. This file is an adaptation, not a full verbatim import.
