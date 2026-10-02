# Device Interactive QA and Runtime Verification

## Core principle
A successful build, TypeScript check, lint check, unit test, or CI run does **not** prove that an application works correctly for a real user. When the environment and tooling allow it, production development includes interactive runtime verification.

Standard QA flow:

**PLAN → BUILD → STATIC CHECK → AUTOMATED TEST → RUN → INTERACT → OBSERVE → DEBUG → FIX → RETEST → VERIFY → COMMIT**

The existing phased loop remains authoritative; TEST and VERIFY must include runtime/device/browser/API interaction where applicable.

## 1. Environment discovery
Before interactive QA, classify the project: Web, PWA, React Native, Expo, native Android, native iOS, Flutter, desktop, backend/API-only, or full-stack combination.

Detect only targets actually available: browser, Android emulator, connected Android device, iOS Simulator, connected iPhone/iPad, Expo development build, Expo Go where appropriate, local/staging backend, and provider sandbox.

Never claim a target was tested when it was unavailable.

## 2. Android verification
For Android-capable projects inspect as appropriate: Java, ADB, connected devices, ANDROID_HOME/ANDROID_SDK_ROOT, Gradle, SDK/target SDK/build tools, and emulator availability. Confirm the target through ADB and record model, Android version, API level, device ID, architecture, and application package. Android Studio being installed is not proof that emulator/device testing occurred.

## 3. iOS verification
On macOS with iOS tooling, inspect Xcode/xcodebuild, Simulator, connected devices, CocoaPods where applicable, and signing configuration. Record simulator/device details. On environments unable to run iOS (including Windows), report **NOT TESTED — ENVIRONMENT UNAVAILABLE**.

## 4. Start the actual stack
Derive startup commands from repository manifests/scripts; do not guess when authoritative scripts exist. Start only required frontend/backend/Metro/Expo/database/workers/queues/emulators. Verify service health first. For mobile, verify **DEVICE → APPLICATION → API → DATABASE/SERVICE** connectivity and do not assume device/emulator localhost maps to the host.

## 5. Install, launch, observe
Where possible build/install the actual development application and launch it on the selected target. Observe compiler/bundler/Metro errors, Logcat, runtime exceptions, API/provider errors, native crashes, navigation warnings, and unhandled promises. A rendered screen alone is not PASS.

## 6. Interactive control inventory
Inventory every reachable button, icon button, tab, navigation item, link, card action, dropdown, selector, switch, checkbox, radio, text input, form/submit, modal, bottom sheet, menu, gesture, back/refresh/retry, upload/camera/gallery, pagination, financial, authentication, and notification action.

Classify each: **PASS, FAIL, DISABLED BY DESIGN, PROVIDER BLOCKED, NOT REACHABLE, NOT TESTED, PLACEHOLDER**. There must be no unexplained dead control.

## 7. Action verification
Do not mark a control PASS merely because it renders, has a handler, compiles, or is mocked by a unit test. Where runtime interaction is available, activate it and verify the observable result end-to-end. Example: Save → request → backend accepts → database/state changes → UI updates → reload → state persists.

## 8. Product-specific user journeys
Derive journeys from the actual PRD, TRD, routes/screens, APIs, database, and existing tests. Do not blindly apply generic checks. Typical journeys can include signup/login/logout, profile, search, create/edit/delete, upload, messaging, notifications, payments, settings, and admin.

## 9. Negative testing
For important workflows test happy and failure paths: empty/invalid input, duplicates, unauthorized access, expired session, insufficient balance, invalid media, denied permission, unavailable API, timeout, network loss, retry, and interruption. Fail safely.

## 10. Authentication and authorization QA
Where applicable test signup/sign-in, incorrect credentials, OTP/resend/expiry/attempt limits, social auth, session persistence/expiry, logout, protected routes, unauthorized access, and account switching. Never expose test credentials in reports/screenshots/logs.

Test server-side authorization directly: cross-user private data, mutation of another user's data, admin/org controls, private messages, financial records, ownership IDs, and client-supplied role/account IDs. Hidden UI is not authorization.

## 11. Navigation and form QA
Test tabs, nested navigation, back, deep links, modals, repeated navigation, auth redirects, protected screens, notification links, and restart restoration. Detect loops, duplicate screens, invalid params, broken back behavior, and unreachable screens.

For forms test required/optional fields, validation, keyboard behavior, loading, double-submit, retry, server errors, state preservation, successful submission, and persistence where required. Prevent duplicate creation from repeated taps.

## 12. Media, theme, responsive, accessibility
Where relevant test media selection/camera/video/file selection, preview/upload/cancel/replace/delete, denied permissions, invalid/oversized media, failure/retry, and persistence.

For system appearance, interactively test light and dark themes including contrast, icons, surfaces, cards, borders, modals, navigation/status bars, inputs, loading/error/empty states.

Test representative mobile and web sizes for clipping, overflow, inaccessible controls, keyboard obstruction, safe areas, modal sizing, touch targets, and truncation.

Where tooling permits verify labels, roles, focus, keyboard navigation, touch targets, contrast, dynamic text/font scaling, screen readers, and meaningful image descriptions.

## 13. Network, restart, recovery
Where appropriate simulate offline/slow/unavailable APIs, timeout, interruption, and reconnection. Verify loading/error/retry/recovery without duplicate transactions or corrupted state.

For mobile/desktop, terminate and relaunch. Verify relevant auth, drafts, theme/preferences, pending operations, transaction recovery, and navigation state. Financial uncertainty is never success.

## 14. Financial QA
Financial state is server-authoritative. Never fake successful payment, wallet credit, withdrawal, refund, settlement, donation, or payout. Test amount validation, idempotency, duplicates, insufficient balance, reservation/settlement, provider/webhook verification, retry/interruption/reversal/reconciliation, ledger conservation, and concurrency. Client callbacks are not proof of payment success.

## 15. Concurrency
For high-risk operations (payments, transfers, withdrawals, donations, claims, inventory, booking/capacity, rewards, scheduled distributions), test concurrent/repeated requests and verify server/database constraints, locks, transactions, and idempotency prevent double-spend, duplicates, negative balances, and capacity overflow.

## 16. Provider-aware QA
Classify external providers (payments, OTP, email, KYC, OAuth, push, analytics, crash reporting, storage) as **CONFIGURED, PARTIALLY CONFIGURED, SANDBOX READY, PROVIDER BLOCKED, LIVE READY**. If credentials are unavailable, test to the provider boundary and mark the rest PROVIDER BLOCKED. Never fake provider success.

## 17. Notification QA
Where notifications exist test permission, token registration/refresh/removal, foreground handling, tap/navigation, settings, categories/channels/sounds where applicable, and background delivery where supported. Physical-device verification may be required for final status.

## 18. Privacy QA
Test privacy as behavior. Attempt cross-account access and verify APIs return only required data. Check profiles, messages, financial/KYC/contact data, private uploads, admin data, and audit data. Frontend hiding is not privacy enforcement.

## 19. Runtime log monitoring
During QA monitor relevant browser console/network, Metro, Logcat, backend/application logs, and provider logs. Inspect fatal exceptions, unhandled promises, repeated failures/5xx, memory/media/navigation/provider/security errors. Expected validation failures are not automatically defects.

## 20. Defect workflow
**REPRODUCE → ROOT CAUSE → SMALLEST APPROPRIATE FIX → ADD/UPDATE TEST → RETEST EXACT FAILURE → REGRESSION TEST RELATED AREA → VERIFY**

Never hide exceptions, delete functionality merely to pass tests, disable features without justification, weaken security, hard-code success, modify node_modules as a permanent fix, or bypass backend validation.

## 21. Automated regression after runtime QA
After runtime fixes rerun applicable TypeScript, lint, unit/component/integration/API/database/backend tests, production builds, and CI-equivalent commands. Interactive and automated QA complement each other; neither replaces the other.

## 22. Physical-device distinction
Report separately: **EMULATOR VERIFIED, SIMULATOR VERIFIED, PHYSICAL DEVICE VERIFIED**. Do not treat them as equivalent. Camera, biometrics, real push, background execution, deep links, microphone/voice, Bluetooth, NFC, real network transitions, provider SDK capture, and device permissions often require physical hardware. If unavailable, report it.

## 23. Web and backend equivalents
For web, use an actual browser when available: navigate routes, click controls, fill/submit forms, inspect network/console, test responsive sizes/auth/errors/persistence. A production build alone is not verification.

For backend/API-only projects use real HTTP requests, auth/authz, invalid payloads, idempotency, concurrency, database-state checks, provider boundaries, restart/recovery, and security tests.

## 24. Dead-control policy
Before production readiness, every interactive control must be **WORKING, DISABLED WITH EXPLANATION, PROVIDER BLOCKED WITH EXPLANATION, or INTENTIONALLY HIDDEN/REMOVED**. No silent dead buttons or operational-looking fake placeholders.

## 25. Evidence and no false verification
Never say “production ready”, “fully working”, “everything works”, or “all buttons work” without objective evidence. Separate **IMPLEMENTED, AUTOMATED TESTED, EMULATOR/SIMULATOR TESTED, PHYSICAL DEVICE TESTED, LIVE PROVIDER VERIFIED**.

Never claim a click/device/provider/API/payment/deployment test that did not occur. Unknown remains UNKNOWN; blocked remains BLOCKED; not tested remains NOT TESTED.

## 26. QA matrix and final report
For substantial apps track: Screen/Feature, Action, Expected Result, Actual Result, Status, Environment, Evidence, Fix, Retest. Allowed statuses: PASS, FAIL, PROVIDER BLOCKED, DISABLED BY DESIGN, NOT REACHABLE, NOT TESTED.

At each production QA phase report environment, app version/commit, target device/browser/OS, screens/controls tested, PASS/FAIL/provider-blocked/disabled/not-tested counts, defects found/fixed/unresolved, runtime/backend errors, automated/build/security results, provider status, physical-device status, and remaining production blockers.

## 27. Compute efficiency
Inspect first. Reuse still-valid evidence. Run targeted tests after targeted fixes. Avoid unnecessary dependency reinstalls/native rebuilds/repeated unchanged builds/repeated blocked-provider tests. Run broad regression at meaningful checkpoints and full release testing at the release gate.

## 28. Test personas
Preserve the non-production test-persona/test-admin workflows. Development/staging personas may support role testing and OTP bypass only under the existing server-enforced non-production safeguards. Never create production backdoors or expose credentials.

## Production gate
Interactive runtime/device/browser/API verification is required wherever the environment and tooling make it possible. Unavailable targets must be explicitly recorded, not simulated or implied.
