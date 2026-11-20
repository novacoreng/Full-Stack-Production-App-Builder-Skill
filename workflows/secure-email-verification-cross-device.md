# Secure Signup, Email Verification and Cross-Device Redirect

## Applicability and release rule
Mandatory for applications that offer email/password registration. Use the application's existing authentication provider and technology stack. If the app uses only another approved authentication method, document NOT APPLICABLE and do not introduce email/password auth without approval. Preserve existing branding, UX, database/project isolation and security. Do not deploy the email-signup feature until delivery, database permissions, verification, redirect and failure scenarios have been verified with evidence.

## Required end-to-end experience
1. Create an accessible signup page with email, password, password confirmation, appropriate validation and clear safe error messages. Never log passwords or echo secrets in errors.
2. After registration, show a branded "Check Your Email" screen with guidance and resend controls. Avoid account enumeration in public endpoints.
3. Send a branded verification email through the configured provider containing a cryptographically secure, expiring, single-use confirmation link. Use the real approved brand assets and email templates.
4. Direct confirmation to `/auth/confirm` on the correct environment's trusted origin. Validate the token server-side or using the authentication provider, and reject missing, invalid, expired and already-used tokens with understandable errors and a protected resend option.
5. On successful confirmation, show "Email verified successfully" and navigate the confirming device toward `/auth/sign-in`. Do not automatically sign in solely because email ownership was confirmed.
6. Cross-device: if registration started on desktop and the link opens on mobile, the original desktop detects the account's verified state through secure polling approximately every five seconds while the pending verification screen is active. The same applies in reverse. Stop polling on success, navigation, expiry or unmount; bound retries and use backoff when the network fails.
7. The verification-status mechanism must not transfer passwords, access tokens, refresh tokens or authenticated sessions between devices. Use a short-lived, scoped, non-authenticating pending-registration status capability or an equivalent provider-supported mechanism; prevent guessing, enumeration, status leakage and abuse. Server-side checks must independently establish verification state.
8. Show "Email verified successfully" on the original device and redirect it to Sign In. Require a normal secure sign-in after verification.
9. Resend confirmation with rate limiting, cooldowns, abuse protection and provider-specific rules. Do not expose whether arbitrary addresses exist.
10. Keep environment-specific trusted redirect origins for local development, preview and production. Validate allowlists and prohibit open redirects. Use HTTPS in production.
11. Ensure tokens expire, cannot be replayed or reused and are never logged, leaked to analytics, or persisted in unsafe client storage. Protect callback handling against token disclosure in URL referrers/history where applicable.
12. Ensure database access controls and authorization are correct. An unverified account must not gain privileges requiring verified email.

## Configuration contract
- Example production site URL: `https://yourapp.com` (placeholder only, replace with the application's verified domain).
- Example verification callback: `https://yourapp.com/auth/confirm`.
- Sign-in destination: `/auth/sign-in`.
- Define separate allowed site/callback URLs for development, preview and production. Never deploy the example domain as a literal configuration.
- Keep mail provider credentials, signing keys and authentication secrets in the correct environment's secret store, not source control.

## Verification matrix
- Same-device signup and confirmation.
- Desktop signup -> mobile email confirmation -> desktop status update -> sign in.
- Mobile signup -> desktop email confirmation -> mobile status update -> sign in.
- Missing, malformed, expired, consumed and tampered confirmation links.
- Resend success, cooldown, rate limits and duplicate submissions.
- Network interruption, delayed email, polling timeout, recovery and retry.
- Redirect allowlists, HTTPS, session separation and cross-environment isolation.
- Server-side authorization and database permission checks before and after verification.
- Real test email delivery and template branding, including link origin and sign-in destination.
- Mobile responsiveness, keyboard accessibility and iPhone/Android safe-area behavior.

## Acceptance and evidence
Acceptance requires a user to register on one device, verify email on another, see the original device automatically reflect verified status and sign in without registering again. Record actual provider setup, deployed environment, test devices, test account scope, network/error results, email delivery, access-control verification, outstanding blockers and rollback plan. Do not claim delivery or security tests passed without observing them. An unresolved critical flow or permission issue blocks release.

Integrate with `workflows/authentication.md`, `workflows/security.md`, `workflows/device-interactive-qa.md`, `workflows/consumer-trust-privacy.md`, `templates/TESTING.md` and the phase reporting checklist.
