# Authentication
Implement secure sessions/tokens, signup, login, logout, recovery, OTP/social auth where specified, session expiry, authorization, role/permission enforcement, and abuse protections. Validate authorization at backend boundaries.

## Required email verification flow when email/password signup is enabled
Follow `workflows/secure-email-verification-cross-device.md` end-to-end. Verification uses expiring, single-use tokens and `/auth/confirm`, branded email, protected resend, and a non-authenticating pending-registration status check approximately every five seconds to update the original signup device after cross-device confirmation. Never transfer credentials or sessions between devices. Require explicit sign-in after verification and validate database permissions and redirects before deployment.
