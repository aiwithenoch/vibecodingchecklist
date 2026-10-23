# Production Launch Checklist

**Project:** __________  **Owner:** __________  **Date:** __________  **Commit:** __________

Use `N/A — reason` for controls that do not apply. Include links to tests, config, dashboards, or logs as evidence.

## Scope and architecture
- [ ] Essential user journeys and acceptance criteria are documented.
- [ ] Data flows, trust boundaries, dependencies, and failure cases are understood.
- [ ] Simpler architecture was preferred unless complexity is justified.
- [ ] Privacy, ownership, retention, and applicable legal requirements were reviewed.

## Correctness and data
- [ ] Critical paths are covered by passing unit/integration tests.
- [ ] Authentication and **server-side authorization** have been tested.
- [ ] Tenant boundaries and access policies were verified, if relevant.
- [ ] Untrusted input is validated and errors are safe.
- [ ] Schema migrations were tested on representative data.
- [ ] Slow queries, indexes, and N+1 query patterns were checked.
- [ ] Concurrent and repeated orders/payments cannot corrupt state.
- [ ] API/database queries are bounded and paginated.

## Security
- [ ] A source-first security review mapped lower-trust inputs to sensitive operations and recorded exact evidence; see [Security Audit Review](SECURITY-AUDIT.md).
- [ ] Security candidates are separated into `confirmed`, `needs_validation`, and `rejected`; only confirmed findings receive severity.
- [ ] Unknown proxy, identity-provider, cloud, broker, browser, or deployment controls are recorded as unknowns with an owner-observed validation plan rather than guessed.
- [ ] No secrets in repositories, client code, or logs.
- [ ] Production access follows least privilege.
- [ ] HTTPS/TLS is configured; stored sensitive data is protected.
- [ ] Relevant SQL injection, XSS, CSRF, SSRF, and CORS risks are mitigated.
- [ ] Dependencies and images were scanned; critical findings reviewed.
- [ ] Sessions, password recovery, and abuse protections are appropriate.
- [ ] Webhooks verify authenticity and handle replay/duplicates if used.

## Reliability and performance
- [ ] External calls have deadlines and safe bounded retries.
- [ ] Critical image/media requests, layout reservation, and first-screen loading are measured on cold and warm visits.
- [ ] Large API/database results and rendered lists are bounded or paginated; limits do not silently hide required records.
- [ ] Main-thread/rendering cost and long-session resource cleanup are profiled for critical user journeys.
- [ ] Virtualization is used only when measured DOM/render cost justifies it, and scrolling, focus, accessibility, state, and loading have been tested.
- [ ] Detailed evidence recorded using [Performance and Rendering Review](PERFORMANCE-AND-RENDERING.md).
- [ ] Scheduled and queued jobs are idempotent, when used.
- [ ] Expected traffic and bottlenecks are measured or documented.
- [ ] Sensitive public endpoints have abuse protections.
- [ ] Caches have TTL/invalidation and privacy-safe keys.
- [ ] External provider outages produce reasonable degraded behavior.

## Deployment and recovery
- [ ] Release process is repeatable and tied to a commit.
- [ ] Dev, staging, and production are isolated.
- [ ] Readiness and health checks work.
- [ ] Rollback is documented and safely practiced.
- [ ] Backups are enabled **and restoration tested**.
- [ ] Recovery contacts, RTO, and RPO are documented.

## Operating in production
- [ ] Logs, metrics, and traces reveal errors and latency without sensitive data.
- [ ] Actionable alerts have a recipient and runbook.
- [ ] Cost budgets and provider quotas are monitored.
- [ ] Incident severity, escalation, and customer communication are defined.
- [ ] Post-deployment smoke tests pass.

## Release decision
- **Decision:** GO / NO-GO / GO WITH EXCEPTIONS
- **Blocking risks:**
- **Accepted exceptions and owners:**
- **Evidence links:**
- **Approver:**
