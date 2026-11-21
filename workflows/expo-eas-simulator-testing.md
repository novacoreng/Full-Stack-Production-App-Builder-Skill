# Expo Skills and EAS Simulator Testing

Official sources:
- https://docs.expo.dev/skills/
- https://docs.expo.dev/eas/simulators/get-started/
- https://github.com/expo/skills/tree/main/plugins/expo/skills/eas-simulator

## Applicability
For Expo and React Native applications that need iOS/Android device testing, evaluate the official Expo Skills. Prefer the `eas-simulator` skill when a local simulator is unavailable (Linux/headless CI/cloud agents) or the user explicitly requests cloud simulator testing. On macOS with working local simulators, use local testing unless cloud testing is specifically desired. For non-Expo applications, choose an appropriate testing approach instead. A web PWA is not automatically an installable native Expo app.

## Install and read the official skill
In Codex, Expo documents `codex plugin add expo@openai-curated`; in other compatible agents it documents `npx skills add expo/skills`. Install only in an authorized development environment and check tool availability and compatibility. Read the latest official `eas-simulator` SKILL.md before issuing any experimental simulator commands, since flags may change. Inspect `eas simulator:start --help` for supported syntax.

## Prerequisites and safety
- Work in the target Expo project directory. Verify app configuration and EAS project linkage; `eas init` requires an intentional project setup.
- Confirm the Expo identity with `eas whoami` or the authenticated equivalent. Headless environments need a securely injected `EXPO_TOKEN`, never a token committed to GitHub or displayed in reports.
- Run `eas simulator:availability --json` **before** starting a session. If `available` is not true, do not start. Mark BLOCKED and use a suitable local or other authorized alternative.
- Expo Simulators is a paid service. Respect account access, cost limits and approved test scope. Set a bounded duration and stop the session after testing.
- Add `.env.eas-simulator` to `.gitignore` before starting. It contains sensitive simulator controller credentials. Never commit or share it.
- Use synthetic/non-production identities and data, and preserve project isolation. Do not connect to production databases or perform real payments during routine testing.

## Session and app installation
1. From the linked project, check CLI version/help, authenticated account and `eas simulator:availability --json`.
2. Choose `--platform ios` or `--platform android`, a named session and controller type, such as `agent-device`. Example: `eas simulator:start --platform ios --type agent-device --name "Phase QA iOS" --non-interactive --max-duration-minutes 30`. Confirm exact flags with current CLI help.
3. Install the **real target app** using an appropriate existing EAS build ID, fingerprint, application archive URL or Expo Go option, following the current official skill and docs. Do not invent an archive, build or app ID. If a native build is missing, report the blocker and seek the required build approval.
4. Verify the session with `eas simulator:get --json --non-interactive`; require `status: IN_PROGRESS` and usable remote configuration.
5. Drive supported interactions using the session controller and the official skill. Capture screenshots, logs and interaction evidence; verify launch, navigation, signup/auth, forms, keyboard, safe areas, orientation, gestures, errors and critical product flows. Android controller capabilities may differ from iOS; do not claim unsupported actions.
6. Record platform, device profile, OS version, app build/commit, session ID (non-secret), test cases, observed results and defects. Distinguish simulated testing from physical-device testing.
7. Stop with `eas simulator:stop` or the current documented equivalent, confirm stopped status, and clean up session credentials safely.

## Mandatory build phase reporting
At each relevant mobile phase, include iOS and Android test status in the complete phase checklist. Mark PASS only with real installation and interactive evidence. Record NOT TESTED or BLOCKED if Expo account access, project linkage, credentials, build or simulator tools are missing. Never claim a simulator session was started or an app installed unless the commands actually succeeded. Include screenshots/logs when available and track remaining device coverage.

## Installation is not testing
Adding this workflow to the builder repository does not install Expo Skills into every app, grant an Expo subscription, start a cloud session or test an application. Those actions must be performed in the specific development environment with the project and account available.
