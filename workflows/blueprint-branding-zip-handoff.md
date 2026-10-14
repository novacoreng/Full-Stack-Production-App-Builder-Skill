# Blueprint Documentation, Logo Approval and ZIP Delivery

## Basis and distinction
The user-provided "The Vibe Coding Blueprint" (31-page PDF) emphasizes context before code and eight core documents: PRD.md, DESIGN_SYSTEM.md, ARCHITECTURE.md, DATABASE.md, SECURITY.md, CODE_STYLE.md, TESTING.md and AGENTS.md. It also introduces UX_FLOWS.md and an incomplete API.md section; its expanded API starter and workflow prompts are editorial additions, not part of the original eight. Adapt these concepts to existing accepted PRD, TRD, App Flow, Design Brief, Background Schema and Documentation Plan gates. Do not duplicate or replace approved source-of-truth documents.

The **logo concept approval** and **ZIP delivery** requirements below are user-added requirements, not claims made by the PDF.

## Pre-phase documentation alignment
Before implementation, establish or cross-reference:
- PRD: problem, users, scope, non-goals, acceptance criteria and definition of done.
- Design system/design brief: brand, approved logo, typography, colors, spacing, components, states, responsive rules and accessibility.
- TRD/architecture: components, dependencies, infrastructure, integration choices, failures and data flows.
- Database/background schema: entities, relationships, constraints, validation, migrations and sensitive data.
- Security: authentication, authorization, secrets, data protection, uploads and abuse controls.
- Code style: project conventions, imports, reuse, logging, error handling and lint/format checks.
- Testing: unit/integration/E2E plans, critical journeys, commands, coverage and evidence.
- Agent instructions: documentation discovery, source-of-truth precedence, change control and validation.
- App/user flows and API contracts when applicable, including failure/loading/empty states, auth/ownership, retries and idempotency.

Keep documentation minimal but complete, versioned and consistent with implementation. Do not choose an unapproved technology stack or invent missing business requirements. Resolve contradictions before coding.

## Logo concept approval before phase build
1. Check whether a real, approved brand logo already exists in user assets or the repository. If so, preserve it exactly unless an explicit redesign is requested.
2. For a new brand without an approved logo, prepare a **clearly labeled logo concept** before the first production implementation phase. Include intended visual direction, color rationale, light/dark usage, app icon/favicon considerations and legibility at small sizes.
3. Provide an actual visual concept when image creation is supported and requested/authorized; otherwise provide a written concept and mark visual asset generation BLOCKED, rather than falsely claiming an image exists.
4. Request approval or revisions. Do not promote a concept to the official logo, replace supplied brand assets or implement it across the app before approval.
5. Record the approved asset, variants, license/provenance and decision in the design brief. If approval is outstanding, the brand-asset gate remains BLOCKED; documentation work may continue but branded production build does not start.

## Build ZIP delivery
- For **each completed phase build**, offer and, when filesystem tooling is available, generate a downloadable ZIP snapshot containing that phase's deliverable source, relevant documentation, configuration examples, assets and a manifest identifying project, phase, version, commit and validation status.
- Also provide a complete ZIP at final handoff. If the user requests a ZIP before the first phase, supply a **pre-production starter ZIP** with locked documentation, approved assets (if any), folder skeleton, README and setup instructions, clearly marked NOT YET IMPLEMENTED rather than pretending it is a functional app.
- Include README with prerequisites, installation, build/test commands, environment variable names (never values), provider setup steps, known blockers and phase status.
- Exclude .env, API keys, credentials, certificates, production database exports, user data, caches, node_modules, build outputs unless explicitly required and safe, and unlicensed assets.
- Preserve the project's real file structure and package/lock files. Do not ship empty or fabricated features as working.
- Validate ZIP integrity by listing entries and opening the archive; run applicable source tests/builds separately and record exact results. A valid ZIP does not prove the app runs.
- If filesystem/archive creation or delivery is unavailable, mark ZIP DELIVERY BLOCKED and provide an accurate handoff plan. Never invent a download link.
- If GitHub is connected, commit each phase and record the commit SHA; the ZIP manifest must identify the exact snapshot or clearly label uncommitted changes.
- Keep approved logo and asset decisions consistent across the ZIP, repository and deployed build.

## Gate order
PRD -> TRD -> App Flow -> Design Brief (including logo concept approval if needed) -> Background Schema -> Documentation Plan -> Production phase implementation -> Phase verification and ZIP handoff.

Do not bypass the six locked pre-production gates. The concept review may be prepared during Design Brief, but phase coding cannot begin until required approvals are recorded.
