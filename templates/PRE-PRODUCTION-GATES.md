# PRE-PRODUCTION GATE MATRIX

Required sequence:

**PRD → TRD → App Flow → Design Brief → Background Schema → Documentation Plan → Production**

| Gate | Artifact / location | Status | Acceptance evidence | Downstream impact | Locked commit |
|---|---|---|---|---|---|
| PRD | | NOT STARTED | | | |
| TRD | | NOT STARTED | | | |
| App Flow | | NOT STARTED | | | |
| Design Brief | | NOT STARTED | | | |
| Background Schema | | NOT STARTED | | | |
| Documentation Plan | | NOT STARTED | | | |
| Production entry | | BLOCKED | Gates 1–6 required | | |

Statuses: NOT STARTED / DRAFT / REVIEW / LOCKED / BLOCKED / REOPENED.

## Enforcement
- Production entry remains BLOCKED until gates 1–6 are LOCKED.
- Do not silently skip or reorder a gate.
- Existing documents must be audited against current requirements before being marked LOCKED.
- Material changes require downstream change-impact analysis.
- Reopen, update and re-lock every affected downstream artifact.
- Record GitHub evidence when a repository is connected.

## Branding and delivery checkpoints
- At Design Brief review, check for an existing approved logo. Preserve it if present. Otherwise present a concept, obtain explicit approval and record the approved source asset before branded production implementation.
- Before first phase implementation, optionally provide a clearly labeled pre-production starter ZIP containing approved/locked documents and project skeleton, not a claimed working application.
- At each phase handoff, provide a verified ZIP archive of the actual phase source and relevant documentation, plus commit SHA, manifest, setup notes and test status. At final handoff provide a full ZIP. If packaging cannot be performed, mark ZIP DELIVERY BLOCKED rather than inventing an artifact.
- See `workflows/blueprint-branding-zip-handoff.md`.
