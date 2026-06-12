# Security Policy

## Reporting a vulnerability

Please do **not** open public issues or pull requests for security vulnerabilities.

Preferred: report privately using GitHub Security Advisories for this repository.

If private reporting is not available for you, contact the maintainers via the Drupal.org project page and clearly indicate that the report is security-sensitive.

## What to include

- A clear description of the vulnerability and impact
- Steps to reproduce (or a proof of concept)
- Affected versions (Drupal core version, module version, and relevant config)
- Any suggested mitigation or fix (if you have one)

## Endpoint access model

The module exposes two public endpoints, both following the JSON:API core
pattern of `_access: TRUE` with authorization enforced in code:

- `/jsonapi/resolve` — resolves a path to its JSON:API URL. Entity view
  access is enforced; unpublished/restricted content does not resolve for
  anonymous callers. Covered by
  `PathResolutionTest::testUnpublishedNodeNotResolved`.
- `/jsonapi/routes` — routes feed for headless builds. Gated by a configurable
  shared secret (`X-Routes-Secret`); returns 404 when disabled, 403 on secret
  mismatch, never exposing data without the secret. Covered by
  `RoutesFeedControllerTest` (404/500/403 cases).
