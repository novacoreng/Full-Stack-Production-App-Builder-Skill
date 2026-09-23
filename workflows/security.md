# Security

Use a risk-based application-security process aligned where applicable with OWASP ASVS and secure-development practices from NIST SSDF.

Audit:
- authentication and authorization;
- role boundaries and server-side authorization;
- RLS/access policies;
- secrets and credential lifecycle;
- API exposure and validation;
- CORS/CSRF where applicable;
- XSS/injection;
- uploads;
- rate limiting and abuse controls;
- sessions/tokens;
- dependencies and supply chain;
- logs and telemetry;
- third-party permissions;
- webhooks/signatures;
- cloud IAM;
- storage access;
- backups/recovery;
- incident response.

Run secret scanning, dependency/SCA checks, SAST, and other relevant security tests. Use SBOM/dependency inventory and container scanning when appropriate.

For admin functionality, verify that hiding an action in the UI is not the security control: direct API/backend authorization must enforce the same permission.

Never commit credentials, private keys, service accounts, environment secrets, generated test-admin passwords, or production access tokens.
