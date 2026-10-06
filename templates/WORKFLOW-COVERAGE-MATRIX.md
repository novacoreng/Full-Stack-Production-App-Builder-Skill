# WORKFLOW COVERAGE MATRIX

Every file under `workflows/` must have a row before a phase lock/release audit. Do not silently omit workflows.

Allowed applicability/status values:
- REQUIRED
- EXECUTED
- BLOCKED
- NOT APPLICABLE

| Workflow | Phase / release gate | Applicability | Reason / requirement | Evidence / test | Blocker / remediation | Commit SHA |
|---|---|---|---|---|---|---|

## Enforcement
- No blank applicability values.
- No SKIPPED status.
- REQUIRED must become EXECUTED before its dependent gate can pass, unless BLOCKED is explicitly accepted and is not release-blocking.
- NOT APPLICABLE requires a concrete product/architecture reason.
- BLOCKED requires the exact missing access/resource/provider/manual action and release impact.
- Re-evaluate the matrix after material PRD/TRD/architecture/provider/platform changes.
- Before production release, compare this matrix against the current repository `workflows/` directory and add any newly introduced workflow.
