# Acme SaaS release notes

Synthetic release notes used by the instructor demo.

## v1.0.0 — 2025-10-31

Quarterly production drop.

- Initial public API package.
- Health endpoint for ops smoke tests.
- Metrics endpoint added for future monitoring.

Known risks:

- Build still run manually by the senior developer.
- No automated deploy gate.
- No documented rollback command.

## v1.0.1 — 2025-11-01

Urgent hotfix after v1.0.0.

- Payment timeout configuration corrected.
- Manual verification done with `curl`.

Incident note:

- Release window overran.
- Ops and dev disagreed on whether the issue was code or environment.

## v1.0.2 — 2025-11-02

Rollback release.

- Dashboard export change reverted.
- Production returned to normal after manual rollback.

Incident note:

- No automated post-deploy smoke test caught the issue.

## v1.1.0 — 2026-01-30

Quarterly production drop.

- User reporting improvements.
- Internal metrics naming cleanup.
- Dockerfile reviewed but not yet built in CI.

Known risks:

- Release still depends on one senior.
- Test command not required before deploy.

## v1.1.1 — 2026-02-01

Login regression hotfix.

- Session timeout fallback corrected.
- Added manual checklist item for login smoke test.

## v1.2.0 — 2026-04-30

Quarterly production drop.

- CI introduced for tests on pull requests.
- Docker build prepared.
- Trivy file scan added.

Known risks:

- Deployment is still manual.
- CI exists, but branch protection is not yet enforced.

## v1.2.1 — 2026-05-01

Deploy hotfix.

- Healthcheck response verified.
- Deployment runbook updated.
