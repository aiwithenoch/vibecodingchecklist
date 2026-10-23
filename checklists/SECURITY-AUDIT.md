# Security Audit Review — Evidence First

> A source-first, defensive review procedure for traditional developers and AI-assisted builders. This is a supplemental method for using the Vibe Coding Checklist; it is not a vulnerability scanner, penetration-test authorization, or security certification.

This guide adapts the operating discipline in Cloudflare's [`security-audit-skill`](https://github.com/cloudflare/security-audit-skill) at reference commit [`c1c8a8c`](https://github.com/cloudflare/security-audit-skill/commit/c1c8a8c). It keeps the Vibe Coding Checklist's existing topic inventory intact while making security reviews more reproducible, honest, and useful.

## The security-review standard

A security concern becomes a confirmed vulnerability only when the review can name all of these facts:

1. **Lower-trust principal:** who can send the input or take the action?
2. **Accepted input or action:** what exact request, message, file, token, model output, configuration, or workflow event is accepted?
3. **Intended control:** what authentication, authorization, validation, isolation, integrity, or resource bound should stop it?
4. **Crossed boundary:** which identity, tenant, resource, execution capability, or availability boundary is crossed?
5. **Affected target:** whose data, account, resource, service, quota, or operator spend is affected?
6. **Observable result:** what bounded local result or safe owner-observed deployment fact proves the security consequence?

A missing header, dependency version, rate limit, isolation layer, or defense-in-depth control is not automatically a vulnerability. If the source shows a complete control, the candidate is rejected. If a decisive proxy, cloud policy, identity provider, browser, broker, or production setting is not visible, record `needs_validation` rather than guessing.

## Choose the review mode

Do not run a full audit merely because this file was read.

- **Guidance mode** — use for a question, focused review, triage, or one suspected vulnerability. Read only the relevant domain sections and return source evidence, a bounded validation plan, and explicit unknowns.
- **Full audit mode** — use only when the owner explicitly asks for a full, comprehensive, end-to-end security audit, penetration test, or report artifacts. Run all phases below, keep the output outside the target repository by default, and state any partial or incomplete coverage.

The mode changes breadth and documentation, not the evidence bar. A quick or scoped review must never be presented as complete coverage.

## Phase 0 — Establish scope and safe execution

Record the following before hunting:

- repository, remote, reviewed commit/ref, dirty-worktree state, and date;
- target paths, excluded paths, companion systems, expected users, critical workflows, and data classes;
- local build/test commands and whether they can run without fetching dependencies;
- previous audit ledgers/findings, if any, and which source paths remain unchanged;
- chosen profile: `quick`, `standard`, or `deep`;
- output directory outside the target, with its write permissions and retention plan.

### Safety boundary

Run target-controlled code, tests, browsers, emulators, fuzzers, and fixture processors only when an OS-enforced sandbox provides all of the following:

- no external network, except an isolated loopback namespace when local client/server traffic is required;
- an empty, explicitly allowlisted environment with scratch-local `HOME`, temporary directories, and caches;
- a read-only target and toolchain, with target-controlled writes limited to an assigned scratch directory;
- explicit CPU, memory, process, file-size, disk, and wall-clock limits;
- dummy principals, fixtures, and secrets only.

If these controls cannot be enforced, do not execute target code. Keep the source evidence and record the missing capability as a `needs_validation` blocker with a safe validation plan.

Never probe deployed endpoints, production identities, shared infrastructure, other users' data, live control planes, paid APIs, or shared services. Never stress a live service. Do not change the audited source unless the owner separately authorizes a fix. Do not put credentials, private tokens, customer data, or authentication state in reports.

## Phase 1 — Reconnaissance before attack ideas

Build an architecture map from the actual repository, not from the README alone:

- entry points: HTTP routes, CLI commands, jobs, workers, message consumers, webhooks, browser routes, file parsers, and tool handlers;
- trust boundaries: anonymous/authenticated/admin, tenant/account, browser/server, service/provider, build/release, and model/tool boundaries;
- identities: user sessions, service accounts, workload roles, API keys, signing keys, broker peers, and delegated agents;
- stores and copies: primary database, caches, search indexes, object storage, logs/traces, exports, backups, replicas, queues, and durable memory;
- external controls: reverse proxies, CDN/cache, ingress, WAF, identity provider, cloud policy, broker ACL, container/runtime, signing service, and deployment overlays;
- security-relevant sinks: database writes, authorization decisions, file paths, URL fetches, HTML/Markdown/command execution, cloud APIs, messages, releases, and paid or shared resources.

For an AI/agent system, draw four additional maps: each execution identity, each capability, every writable prompt/memory/retrieval source, and every output or side-effect sink. For a data-heavy system, follow one protected record through primary storage, derived copies, exports, deletion, revocation, migration, backup, and restore. For a release system, trace source to resolved dependency, build worker, artifact, test result, signature/attestation, promotion, and update consumer.

## Phase 2 — Make coverage countable

In a full audit, create a deterministic coverage ledger before assigning hunters. The parent/coordinator is the only writer of the shared ledger. A unit should identify a concrete:

`surface × boundary × attack class × lifecycle mode`

Use at least these fields:

| Field | What to record |
| --- | --- |
| `unit_id` | Stable lowercase identifier that survives reruns |
| `surface` | Route, subsystem, store, workflow, deployment, or artifact |
| `boundary` | Principal, tenant, identity, capability, data, or shared resource boundary |
| `attack_class` | Specific class being reviewed, not just “security” |
| `status` | `planned`, `covered`, `candidate`, `blocked`, `deferred`, or `out_of_scope` |
| `reviewed_paths` | Repository-relative files and line ranges actually inspected |
| `agent_id` / `reviewer_id` | Who performed the check and who independently verified it |
| `decision` | Fingerprint and final disposition, when one exists |

Useful profiles are:

- **Quick:** one bounded hunter wave, one final coverage critic, and one fresh verifier per candidate; clearly partial.
- **Standard:** separate reconnaissance, hunting, critic, candidate validation, and final record verification.
- **Deep:** split by subsystem and lifecycle, repeat critic waves until clean, and give unchanged prior confirmations an independent second pass.

If earlier runs exist, compare their evidence with the current source. Carry a prior confirmation only when the relevant source and conditions are unchanged, then re-verify it in the current run. Re-open changed-source findings and all prior `needs_validation`, `deferred`, `blocked`, and `out_of_scope` gaps. A prior ledger never proves that the current source is covered.

## Phase 3 — Hunt by concrete attack class

Use the existing 111 concepts and 28 essentials as the topic inventory, then apply the following source-first lenses to the relevant surfaces. Do not force every class onto every application; mark `N/A` with a reason.

### Web, API, and authentication boundaries

- Trace every route and alternate route to authentication, authorization, tenant checks, and sensitive operations.
- Verify OAuth/OIDC redirect ownership, state, PKCE, issuer, audience, nonce, session binding, and account-linking behavior.
- Check password reset, recovery, MFA, passkey, API-key, logout, revocation, and account-switch paths for the intended assurance and one-time binding.
- Compare request parsing across proxy, gateway, framework, and application for duplicate headers, length/framing, normalization, forwarded headers, host, origin, redirects, and response headers.
- Test cookie scope/transport, CSRF for ambient browser credentials, CORS with credentials, cache key/private-response behavior, WebSocket origin or channel binding, and clickjacking only where a sensitive action is actually exposed.
- Trace URL fetches, redirects, file uploads, parsers, and response rendering to SSRF, path traversal, XSS, unsafe schemes, or command sinks.

Do not treat a missing security header or a generic “no rate limit” observation as a finding without an accepted invalid request and a concrete security result.

### Browser and client-side boundaries

- Trace attacker-influenced URL fields, referrers, `window.name`, storage, cached content, DOM attributes, and `postMessage` data to executing or disclosing sinks.
- Verify exact origin and source checks for cross-window messages; substring/prefix/suffix checks are not origin allowlists.
- Review service-worker scope/update paths, Cache Storage, local/session storage, IndexedDB, broadcast channels, and stale-tab behavior across logout, account switch, and role change.
- Confirm DOM injection, prototype pollution, navigation, opener, XS-Leak, WebSocket, and UI-redress claims have a victim-session or cross-origin impact.
- Treat framework escaping, same-origin policy, CSP, COOP/CORP, cookie policy, and safe link defaults as controls to verify, not assumptions to ignore.

### Data isolation and lifecycle

- Check direct, nested, list, count, aggregate, bulk, import, admin, background, and legacy queries for owner/tenant binding.
- Compare ORM scopes, raw/service clients, row-level policies, views, joins, caches, search indexes, object paths, signed URLs, exports, backups, analytics, logs, and replicas.
- Follow ACL changes, membership removal, consent withdrawal, secret revocation, soft deletion, tombstones, retries, queued work, restore, and undelete through every copy.
- Verify composite keys, deduplication keys, cache keys, global uniqueness, and object namespaces cannot collide across tenants or environments.
- Require a concrete cross-principal read, write, disclosure, stale authorization, or lifecycle violation; a tenant field stored on a row is not enforcement by itself.

### Cloud, infrastructure, and deployment

- Render each maintained environment and compare effective overlays, ingress, ports, network peers, workload identity, mounted secrets, storage policy, and runtime configuration.
- Trace lower-trust requests, objects, labels, events, or user-selected resources to cloud IAM and the final operation; application authorization and cloud IAM are separate controls.
- Review metadata/internal-service reachability, trusted-proxy headers, alternate ports, debug/metrics/admin routes, containers, host mounts, runtime sockets, namespace/label trust, and admission paths.
- Check signed URLs and object policies for exact object, operation, principal, audience, and expiry binding; check event envelopes for provider/source/account/topic and replay binding.
- Review secret mount, renewal, rotation, revocation, readiness, reconnect, and outage fallback behavior. A secret reference is not a secret disclosure without a lower-trust reader or unsafe output path.

If a needed firewall rule, cloud attachment, proxy, provider policy, or runtime admission decision is not in the repository, keep the candidate `needs_validation` and name the exact owner-observed fact.

### Supply chain and release

- Trace dependency source/namespace, lockfile/checksum, submodule, downloaded tool, code generator, container/image, build context, cache, artifact, signing/attestation, release promotion, and updater.
- Treat CI configuration as authorization code: compare triggers, checkout refs, fork/PR behavior, protected environments, token permissions, secrets, artifacts, caches, and publish destinations.
- Require immutable identity across build, test, signing, promotion, architecture merge, and install; a mutable tag or same-location checksum is not independent integrity.
- Check branch names, commit messages, issue fields, matrices, artifact names, generated outputs, and paths for shell/template/expression injection.
- Review revoked keys, missing attestations, registry outages, failed downloads, partial releases, rollback, plugin install/update, and downgrade behavior.

A vulnerable dependency alone is not a confirmed finding. Identify who can influence resolution, which trusted build consumes it, and what code execution, release, secret, or privilege boundary follows.

### AI, LLM, agent, and MCP boundaries

- Prompt injection alone is not a finding. Trace attacker-controlled content to another principal's context, a capability the requester lacks, private data, or an unrequested side effect.
- Check retrieval filters and cache keys for tenant/ACL scope; check persistent memory writers/readers, provenance, deletion, and cross-session reuse.
- Treat model output, tool descriptions, MCP metadata, schemas, retrieval results, and tool responses as untrusted inputs.
- Re-authorize every tool at the handler's final decision point. Validate SQL, shell, file, URL, resource, amount, batch, and tenant arguments after normalization.
- Bind approvals to the normalized tool, complete arguments, requester, target, amount, expiry, and batch; compare direct, queued, retry, resume, and delegated paths.
- Check tool-schema/dispatcher disagreement, excessive agency, confused deputy, delegated credential scope, MCP server/tool/request correlation, and output rendering.
- Bound delegated loops, paid calls, retries, queue work, and cancellation. A system prompt is guidance, not an authorization boundary.

### Protocols, messaging, and availability

- For RPC and messages, record authenticated peer at each hop; schema shape does not prove provenance, tenant, authority, or safe values.
- Compare envelope and payload identity, schema versions, duplicate/unknown/default fields, stream-item authorization, callback correlation, broker ACLs, dead-letter/diagnostic access, and gateway-transcoded routes.
- Test bounded duplicate, missing, unknown, replayed, reordered, and delayed messages; verify commit/ack ordering, inbox/outbox behavior, idempotency, and stale-state rejection.
- Build an input-to-cost table for body/file/cardinality limits, work before auth, parser expansion, downstream fan-out, storage, queues, pools, quotas, deadlines, cancellation, cleanup, and recovery.
- Review unbounded buffering, decompression/representation amplification, expensive pre-authentication work, quota/reset confusion, worker starvation, retry storms, poison records, fatal errors, deadlocks, and unsafe recovery.

Never validate availability by saturating a live or shared service. Use asymptotic reasoning, small local growth fixtures, mocked paid calls, and strict resource limits.

## Phase 4 — Validate every candidate

Give each unique candidate to a fresh reviewer who did not find it. The reviewer must re-read every current source path and try to refute the claim before accepting it.

### Candidate verdicts

- **`confirmed`** — complete source trace plus bounded observed result. Include root cause, intended behavior, conditions, target-native execution, impact, severity, confidence, and the smallest effective fix.
- **`needs_validation`** — source-grounded candidate with a precise unresolved deployment/local fact and an exact safe plan to resolve it. It has no severity and is not reported as a confirmed vulnerability.
- **`rejected`** — source, local behavior, an effective control, missing impact, or an impossible prerequisite disproves the claim. Keep the record so the same unsupported claim is not repeated without changed evidence.

Every record should have a stable fingerprint and repository-relative paths. A multi-step trace starts at a real lower-trust entry point, shows propagation, and ends at the claimed sink or boundary effect. Do not repair malformed reviewer output by guessing; rerun with a fresh reviewer when possible.

### Evidence contract for `confirmed`

- exact file and line evidence for entry point, control/decision, propagation, and sink;
- the real input shape and the affected dummy principal/resource;
- every relevant parser, identity, authorization, normalization, lifecycle, framework, and containment control;
- a bounded target-native reproduction that stops at the minimum meaningful result;
- likelihood, impact, and overall severity calibrated to demonstrated impact;
- a remediation that enforces the invariant at the last trusted decision point, plus a regression case.

### Evidence contract for `needs_validation`

- exact source trace supporting only the claimed root cause;
- the decisive missing fact, such as an ingress attachment, IdP policy, browser behavior, secret, broker ACL, cache rule, cloud identity, or production route;
- a bounded local plan and/or safe owner-observed deployment plan that resolves that fact;
- no severity, exploit instructions against a live system, or claim that the control is absent.

## Phase 5 — Produce a review that can be trusted

For a full audit, keep these artifacts outside the target by default:

```text
run-metadata.json
architecture.md
coverage-ledger.json
findings.json
REPORT.md
FINDINGS-DETAIL.md
NEEDS-VALIDATION.md
```

The parent/coordinator alone writes shared run files. Each delegated reviewer gets a unique scratch directory and cannot write the target, another reviewer's directory, or retained artifacts. Promote only predeclared, regular, non-symlink files after the sandbox exits; enforce per-file and total size limits and reject changing files, hard links, devices, sockets, and unexpected paths.

`findings.json` is structured data, not a prose dump. Validate it against the selected schema/validator before deriving reports. The report must separate confirmed findings, needs-validation leads, rejected records, hardening notes, positive patterns, covered units, blocked/deferred units, and explicit out-of-scope areas. A clean report means no confirmed findings under the reviewed scope and evidence—not that the application is certified safe.

## Practical project-review worksheet

- [ ] Mode, scope, source ref, dirty state, target paths, and expected critical workflows are recorded.
- [ ] Architecture, trust boundaries, identities, data stores/copies, external controls, and sensitive sinks are mapped.
- [ ] Every in-scope surface has a ledger unit or a documented `N/A`/`out_of_scope` reason.
- [ ] Candidate records name a lower-trust principal, accepted input, intended control, crossed boundary, affected resource, and observable result.
- [ ] Local execution, if used, ran in an isolated sandbox with dummy data and bounded resources.
- [ ] Live endpoints, production identities, shared services, real customer data, and paid quotas were not probed.
- [ ] Every candidate was independently challenged by a fresh reviewer.
- [ ] `confirmed`, `needs_validation`, and `rejected` are not conflated; only confirmed records have severity.
- [ ] Source paths and line evidence were read back; findings and coverage artifacts passed their validators.
- [ ] The final report states partial coverage, unknown deployment facts, deferred work, and exclusions honestly.
- [ ] No secrets, tokens, personal data, or unverified claims appear in retained artifacts.

## Relationship to the rest of this repository

- Use [111 System Design Concepts](111-CONCEPTS.md) and [28 Additional Engineering Fundamentals](ESSENTIALS.md) for the topic inventory and practical checks.
- Use [Production Launch Checklist](LAUNCH.md) for release decisions; this guide supplies the deeper security-review method.
- Use [AI Coding Agent Audit Prompt](../prompts/AI-AUDIT-PROMPT.md) to instruct an agent; it should not be treated as proof that an audit ran.
- Use [Project Production Readiness Audit](../templates/PROJECT-AUDIT.md) to record evidence, ownership, and the release decision.
- For exact delegated-agent prompts, write isolation, coverage ledger rules, and schema validators, use the upstream [Cloudflare security-audit-skill](https://github.com/cloudflare/security-audit-skill). Do not copy secrets or live-target results into this public checklist repository.

This guide adds review procedure and coverage discipline; it does **not** add topics to the existing 111 + 28 taxonomy or claim that any external application has passed an audit.
