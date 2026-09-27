# Non-Production Test Persona Authentication

## Purpose

At the end of the build, before production release, provision dedicated test personas so the builder/developer can exercise the application without waiting for incomplete external OTP integrations.

This is a testing mechanism only. It is never a production authentication bypass.

## Mandatory environment boundary

The OTP bypass is permitted ONLY when all applicable non-production safeguards are true:

- environment is development, test, preview, or staging;
- test-persona feature is explicitly enabled;
- the test account is marked as a test account server-side;
- production configuration cannot inherit the bypass accidentally;
- real production authentication remains mandatory.

Recommended configuration:

```text
TEST_AUTH_BYPASS_ENABLED=true   # non-production only
TEST_AUTH_BYPASS_ENABLED=false  # production
```

The backend must enforce the environment boundary. A frontend flag alone is insufficient.

## Test personas

Create only the personas required by the application's authorization model, for example:

- Test Admin
- Test User
- Test Moderator
- Test Organization/Company
- Test Creator/Provider
- Test Guest

Each persona should have the minimum permissions required to test its intended flows.

## Test Admin credentials

At the end of the build, provide a dedicated non-production Test Admin account when an admin role exists.

The account should include:
- username or email;
- securely generated password;
- role;
- environment;
- authentication method used for testing;
- expiration/rotation information where supported.

Never use universal credentials such as `admin/admin` or a predictable password. Never hardcode credentials in source code, tests, documentation, screenshots, logs, or Git history. Deliver secrets through the platform's secure secret mechanism or another approved secure channel.

## OTP bypass behavior

The test flow may bypass the external OTP provider in non-production so the builder can test the application before Twilio, email OTP, WhatsApp OTP, or another production verification service is fully configured.

The bypass must still exercise normal authorization/session logic. It must not create a hidden unrestricted login route.

Prefer a server-side test-auth endpoint or provider-supported test credential mechanism that:
- requires an explicitly enabled test environment;
- accepts only designated test personas;
- issues normal application sessions/tokens;
- applies normal role/authorization checks;
- emits an auditable test-auth event;
- is unavailable or hard-fails in production.

## Production safety tests

Before production release, verify:
- test bypass is disabled;
- test-persona credentials cannot authenticate through the bypass;
- test-only routes/endpoints are not exposed;
- test flags cannot be changed from the client;
- production requires real OTP/MFA where specified;
- test credentials are excluded from production data;
- staging/test secrets are separated from production secrets.

If any of these checks fail, production release is blocked.

## Final verification

Use the personas to test positive and negative authorization cases:

```text
Test Admin → allowed admin actions
Test Admin → denied actions outside role
Test User → allowed user actions
Test User → denied admin actions
Test Guest → public actions only
Unauthenticated → protected resources denied
Expired session → reauthentication required
```

Record the test results in the final build report. Re-run relevant tests after any authentication/authorization change.
