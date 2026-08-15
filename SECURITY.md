# Security Policy

Thanks for helping keep OpenSumai and the people who rely on it safe.

## Reporting a vulnerability

**Please don't open a public issue, pull request, or discussion for a security problem** —
that discloses it to everyone before there's a fix.

Report it privately via **GitHub — Report a vulnerability** on this repo's
**Security ▸ Advisories** tab (where private reporting is enabled). This keeps the report
and the fix in one place.

Helpful to include:

- What the issue is and what an attacker could do with it.
- Steps to reproduce, or a proof of concept.
- The affected surface: web, mobile, API/MCP, or infra; app version / commit; platform.

## What to expect

We're a small team, so this is best-effort rather than an SLA: we aim to **acknowledge a
report within a few business days**, keep you updated on remediation, and credit you if
you'd like once a fix ships. Please give us a reasonable window before any public
disclosure — we'll work with you on timing (coordinated disclosure).

## Scope

OpenSumai holds semi-sensitive data — users' saved listings, budgets, notes, and their
BYOK LLM keys. Anything that threatens that is squarely in scope, alongside the usual
classes (auth, injection, secret exposure, RCE):

- **Tenant isolation bypass** — reading or writing another project's listings/notes
  (IDOR, missing/misapplied RLS).
- **Upload handling** — exfiltration, path traversal, unsigned access to stored files.
- **BYOK key exposure** — keys readable in transit, at rest, in logs, or via the API.
- **Auth** — account or admin-impersonation takeover.
- **Unintended ingestion** — any path that fetches listings server-side on the user's
  behalf (against the bring-your-own-listings posture).
- XSS / injection that could run on a user's device, and secret exposure in CI or the repo.
