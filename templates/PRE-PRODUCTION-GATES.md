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
