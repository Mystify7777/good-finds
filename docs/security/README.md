# Security and Privacy

Security is a product requirement, not a post-MVP patch.

## Trust boundaries

- Public browser to application.
- Authenticated member to application.
- Application to database and auth provider.
- Application/background worker to marketplace provider.
- User-submitted URL to server-side network retrieval.
- Member content to public rendering.
- Administrator actions to privileged data.

## Initial security controls

### Identity and authorization
- Verify identity server-side for every protected mutation.
- Enforce ownership checks for edits and deletions.
- Enforce administrator/moderator permissions independently of UI visibility.
- Apply database row-level access policies where supported.
- Test both allowed and denied paths.

### URL ingestion / SSRF
- Explicit marketplace host allowlist.
- HTTPS-only.
- DNS/IP validation, including redirect revalidation.
- Reject private, loopback, link-local, multicast, and reserved IP targets.
- Bounded redirects, timeouts, and response sizes.
- No arbitrary URL proxy endpoint.
- Treat marketplace responses as untrusted input.

### Content safety
- Encode output and sanitize any allowed rich text.
- Never render marketplace HTML directly.
- Validate URLs before rendering outbound links.
- Use safe image delivery policies.
- Prevent XSS and injection.
- Do not place provider secrets or personal data in logs.

### Abuse prevention
- Rate limits by account and IP.
- Endpoint-specific submission, rating, and discussion quotas.
- Suspicious activity signals and moderation workflow.
- Avoid invasive device fingerprinting.

### Privacy
- Email and private profile fields are not public.
- Minimize IP/security log retention.
- Provide account deletion request handling.
- Define content retention/anonymization behavior.
- Avoid collecting purchase evidence until a concrete verification feature exists.

### Operations
- Secrets stored in deployment secret manager.
- Separate development, test, and production credentials.
- Database backups and restore procedure.
- Admin actions are audited.
- Dependencies are scanned and updated.
- Incident response contact and process documented before public launch.

## Required pre-release checks

- Authorization and RLS tests.
- SSRF test suite with redirects and DNS edge cases.
- XSS/input handling tests.
- Rate-limit behavior.
- Secrets scan.
- Dependency vulnerability scan.
- Backup restore rehearsal.
