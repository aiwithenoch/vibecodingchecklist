# CONTEXT.md — Complete Project History, Requirements, Decisions, and Agent Handoff

**Repository:** https://github.com/aiwithenoch/vibecodingchecklist  
**Canonical clone URL:** https://github.com/aiwithenoch/vibecodingchecklist.git  
**Owner/account:** `aiwithenoch` / AI With Enoch  
**Primary branch:** `main`  
**License:** MIT, copyright 2026 AI With Enoch  
**Project form:** public, documentation-first GitHub repository (checklists, prompts, templates, CSV); **not** a deployed software application  
**Context record prepared:** 2026-10-19 (UTC; Ghana uses UTC)  
**Initial substantive publication:** 2026-10-17, Git commit [`49939675720dea81ff07b665f7f29d458d6064f2`](https://github.com/aiwithenoch/vibecodingchecklist/commit/49939675720dea81ff07b665f7f29d458d6064f2)

> **Purpose of this file:** Preserve the detailed decisions and implementation history so a newly assigned human or AI coding agent can resume the work without access to the original conversation. This is deliberately a **full handoff**, not a short abstract. It includes the original user request verbatim and the exact 139 checklist items as originally published. Read the referenced files in full before proposing or changing anything. When the live files change, the live files take precedence over the historical publication snapshot below; preserve history rather than silently rewriting it.

## 1. Direct user instructions and evolution of the idea

The discussion began with a dictated list of engineering terms. The user's original wording is reproduced exactly below, including repeated phrases and speech-transcription errors, so future agents can distinguish what the user actually requested from our editorial corrections.

### 1.1 Exact initial user request (verbatim, unedited)

```text
Write this whole list for me. Rate limiting, caching, load balancing, reverse proxies, API gateway, CI/CD, Docker, Kubernetes, service discovery, circuit breakers, timeout, retries, exponential backoffs, idempotency, message queues, pub/sub, event-driven architecture, distributed transaction saga. Distributed transactions, saga patterns, dead letter queues, cron job, WebSockets, long polling, long polling, okay. Server-sent events, database indexing, query optimization, N plus I queries, connection pooling, read replicas, sharding, partitioning, replication, leader election, CAP theorem, eventual consistency, optimistic locking, pessimistic locking, distributed locks, race conditions, deadlocks, memory leaks, garbage collection, thread safety, backup, pressure, auto-scaling, horizontal scaling, vertical scaling, CDN, edge caching, cache invalidation, feature flags, blue-green deployment, canary releases, rolling deployment, rollbacks, health checks, liveness and readiness probes, monitoring, logging, distributed tracing, metrics, alerts, SLOs, SLIs, error budgets, observability, secrets management, IAM OAuth, JWT rotation, TLS, encryption at rest, encryption in transit, WAF, DDoS protection, CORS, CSRF, SQL injection, XSS, SSRF, database migrations, schema versioning, disaster recovery, backups, failover, multi-region deployment, chaos engineering, cost optimization, cold start, serverless limits, latency, throughput, P99 latency, tail latency, network partitioning, clock skew, DNS, TCP versus UDP, HTTP/2 and HTTP/3 gRPC webhooks. API versioning, semantic versioning, infrastructure as code, Terraform, Helm charts, build caching, dependency hell, production incidents on call, postmortems
```

### 1.2 Subsequent user instructions (verbatim)

1. `What do you think about this?`
2. `I mean this is even followed by coders`
3. `So can we like put everything together and push to GitHub and call it vibe coding checklist?`
4. The user gave this target GitHub URL: `https://github.com/aiwithenoch/vibecodingchecklist.git`.
5. `is it in my vibe codeing check list ? make sure we have a chnagelos .md and context .md so aniother agent can undertstnd what we idid dint try to susmmrizw`

Interpretation of instruction 5: **Do not shorten the handoff to an overview.** Store the actual project decisions, original requirements, data inventory, file paths, history, terminology changes, current state, and limitations in the repository. `CHANGELOG.md` tracks dated changes. `CONTEXT.md` carries ongoing complete state. `AGENTS.md` provides instructions directing future agents to these materials.

### 1.3 Scope clarification: this is for traditional coders too

The user explicitly pushed back against treating the concepts as only for people who prompt AI to generate applications. Scope was broadened to **anyone building software**, including traditional software developers, software engineers, system architects, engineering teams, code reviewers, educators, and people using coding agents.

Do not equate "vibe coding" with a lack of engineering discipline. The chosen framing is:
- **Build it with AI. Understand it like an engineer. Ship it with confidence.**
- Writing code is one stage of software delivery; correctness, security, availability, performance, and maintainability matter regardless of whether a human or AI authored the code.
- Having all 139 concepts listed does **not** mean all 139 technologies belong in every project.
- A small business application and a globally distributed platform have different needs. Avoid unnecessary Kubernetes, microservices, sharding, event buses, or similar architectural machinery.
- Prefer clear testable requirements, measurements, simple architecture, and evidence-based reviews.
- A developer should be able to explain **when a concept is necessary and when it is inappropriate**, not merely memorize terminology.

## 2. What was actually built, and what was not

### 2.1 Published artifacts and counts

- **111 original unique concepts** from the dictated list, cleaned and organized into 10 engineering categories in `checklists/111-CONCEPTS.md`.
- **28 additional fundamentals** discovered as important omissions, in `checklists/ESSENTIALS.md`.
- **139 unique review topics** overall, with corresponding CSV dataset `checklists/TOPICS.csv` (140 rows including the CSV header).
- **Production launch checklist** for actual go/no-go decisions and evidence in `checklists/LAUNCH.md`.
- **Seven-stage learning roadmap** in `checklists/LEARNING-ROADMAP.md`.
- **One copyable AI agent audit prompt** in `prompts/AI-AUDIT-PROMPT.md`.
- **Reusable project audit report template** in `templates/PROJECT-AUDIT.md`.
- **Contributor guidance**, issue template, PR template, Git ignore patterns, and MIT license.
- **Repository README** identifying the audience, purpose, usage, and links.
- **Handoff additions dated 2026-10-19:** `CHANGELOG.md`, `CONTEXT.md`, `AGENTS.md`, plus discoverability links from `README.md`.

### 2.2 What has *not* been built or verified

- There is **no frontend web app, hosted checklist UI, database, API backend, CLI tool, dashboard, or mobile app** in this repository.
- There are **no application runtime tests** because the current artifact is documentation and checklists. Do not claim unit tests, integration tests, browser checks, deployment, load testing, or security penetration testing have run.
- The AI audit prompt is **instructions for another agent**, not a proven automated scanner. Running that prompt requires a coding agent with appropriate access to a separate target repository.
- Blank Markdown checkboxes are **not proof of implementation**. They represent review items. They must only be checked when the target application has evidence.
- This repository does not claim to audit another application's production environment by itself.
- GitHub links and a cloned repo are not a website, nor do they require a hosting stack.

## 3. Terminology normalization from the original speech

The user dictated terms rapidly. The initial published checklist intentionally normalizes technical spelling and duplicates without changing the technical objective:

| Original spoken wording | Published form | Reason |
| --- | --- | --- |
| `N plus I queries` | `N+1 queries` | Standard database-performance term |
| `backup, pressure` | `Backups` and `Backpressure` | Backpressure is the flow-control term; backups are separately covered |
| `timeout` | `Timeouts` | Common plural form for time limits throughout systems |
| `exponential backoffs` | `Exponential backoff` | Standard algorithm name |
| `distributed transaction saga. Distributed transactions, saga patterns` | `Distributed transactions` and `Saga patterns` | Separated concepts, removed overlapping duplicate |
| `long polling, long polling` | `Long polling` once | Eliminated repeated transcription |
| `backup` / `backups` | `Backups` once in original 111 | Removed repetition; restore testing also appears as an additional fundamental |
| `IAM OAuth` | `Identity and Access Management (IAM)` and `OAuth` | Distinct concepts |
| `HTTP/2 and HTTP/3 gRPC webhooks` | `HTTP/2 and HTTP/3`, `gRPC`, `Webhooks` | Separated concepts |
| `production incidents on call` | `Production incidents` and `On-call engineering` | Separated operational practices |
| `cron job` | `Cron jobs` | Standard plural category |
| `infrastructure as code` | `Infrastructure as Code (IaC)` | Conventional abbreviation |

Do not infer that normalizing wording changes the original user's intent. The exact original wording remains above as a reference.

## 4. Information architecture and all current files

This is the exact intended repository structure after the 2026-10-19 handoff update:

```text
vibecodingchecklist/
├── README.md
├── AGENTS.md
├── CONTEXT.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── .gitignore
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   └── checklist-improvement.md
│   └── PULL_REQUEST_TEMPLATE.md
├── checklists/
│   ├── 111-CONCEPTS.md
│   ├── ESSENTIALS.md
│   ├── LAUNCH.md
│   ├── LEARNING-ROADMAP.md
│   └── TOPICS.csv
├── prompts/
│   └── AI-AUDIT-PROMPT.md
└── templates/
    └── PROJECT-AUDIT.md
```

### 4.1 Purpose and behavior of each file

| Path | Exact responsibility and what future agents should know |
| --- | --- |
| `README.md` | Public entry point; title, tagline, 139-topic count, principle that relevance matters more than complexity, navigation, usage, practical completion evidence, community link, and pointers to handoff files. Keep accessible for new readers. |
| `AGENTS.md` | Repository-specific instructions for coding agents; requires reading the complete handoff and history, preserving facts, avoiding unwarranted implementation, keeping topic inventories in sync, and recording changes. |
| `CONTEXT.md` | This durable, detailed conversation and technical history. It preserves original phrasing, rationale, actual repository state, and the full publication inventory. Append meaningful decisions and operational context; do not shrink it. |
| `CHANGELOG.md` | Dated, factual log of changes (including the original Git history and handoff changes). Update whenever substantive files change. |
| `CONTRIBUTING.md` | Small focused PRs, reproduction evidence, measurable checks, and clear explanations of when a proposed practice is not necessary. |
| `LICENSE` | MIT license. Preserve attribution and licensing terms unless the repository owner asks to change them. |
| `.gitignore` | Conventional log, dotenv, OS, build, cache, and Node/Python artifact exclusions. Not a substitute for secret scanning. |
| `.github/ISSUE_TEMPLATE/checklist-improvement.md` | Request template covering proposed item, realistic failure scenario, testable check, applicability, and evidence. |
| `.github/PULL_REQUEST_TEMPLATE.md` | Contributor checklist asking what changed, why, evidence, topic/CSV sync, documentation review, and secret safety. |
| `checklists/111-CONCEPTS.md` | Original 111 concepts grouped into 10 categories, each with an actual verification action and one priority/applicability label. Each entry is an unchecked GitHub Markdown task box. |
| `checklists/ESSENTIALS.md` | Exact 28 foundational additions: requirements, testing, transactions, auth/access, data handling, reviews, docs, and AI-assisted coding security. |
| `checklists/LAUNCH.md` | Release-readiness checklist grouped into scope, correctness, security, reliability, deployment/recovery, and operation. Evidence and GO / NO-GO / GO WITH EXCEPTIONS decision. Not a certification. |
| `checklists/LEARNING-ROADMAP.md` | Seven practical stages from building to distributed systems; includes proof projects and a weekly learn/build/test/teach exercise. |
| `checklists/TOPICS.csv` | The *machine-readable* inventory for all 139 topics, one row per topic. Exact columns: `Type,Section,Topic,Priority,Practical check`. Contains 111 `Original` rows and 28 `Additional` rows. Double-quote CSV escaping is standard. |
| `prompts/AI-AUDIT-PROMPT.md` | Agent review script instructing a repository-aware agent to discover actual architecture, cite file/line evidence, classify PASS/FAIL/UNKNOWN/N/A, prioritize risks, and avoid code changes without permission. |
| `templates/PROJECT-AUDIT.md` | Fillable audit report with project/commit/environment, architecture map, topic/status/severity/evidence/owner/due date, risks, release decision, verification, and rollback. |

### 4.2 Source-of-truth hierarchy

For a future change, use this precedence:

1. **Current user instruction** — overrides earlier plans if explicitly changed.
2. **Live repository content** on the checked-out branch — the authoritative current documents.
3. **`AGENTS.md`** — rules for making edits and validating results.
4. **`CONTEXT.md` and `CHANGELOG.md`** — why changes happened and how the current state evolved.
5. **Historical publication snapshot below** — the exact first public release, deliberately preserved rather than silently updated.
6. Any guesses or unstated assumptions — **not** authoritative; ask or flag them.

For current topic counts and check wording, validate `checklists/111-CONCEPTS.md`, `checklists/ESSENTIALS.md`, and `checklists/TOPICS.csv` together. The snapshot in this file is historical and should not silently become a competing live dataset.

## 5. Editorial model, priorities, and product philosophy

### 5.1 Labels on the 111 original concepts

The original checklist uses three labels, which are **guidance about likely applicability, not universal rules**:

- **Baseline** — frequently relevant to production delivery, such as timeouts, idempotency, migration and rollback discipline, authorization, backups, and meaningful monitoring.
- **Contextual** — evaluate based on actual stack, threats, traffic, integrations, and service-level requirements.
- **Advanced** — distributed protocols or infrastructure options that should be justified by a measured need, not used as default decoration.

The 28 added essentials are practical foundations; the current Markdown file does not display those three labels per entry. The CSV uses `Contextual` as the value for those 28 additional rows; that CSV metadata must not be confused with an assertion that requirements or testing are unnecessary.

### 5.2 A checkbox means a justified, evidenced review

Each original item has a concise **practical check**, not only a concept name. For example:

- **Idempotency:** prove duplicate orders, payments, or jobs execute only once as a business effect.
- **Backups:** schedule them and verify restoring actual data.
- **Authorization:** verify users cannot read or modify someone else's data, including at server and database boundaries.
- **Health checks:** provide a status signal that is useful but not overly revealing.
- **Exponential backoff:** include caps and jitter to avoid retry storms.
- **Service-level objectives and error budgets:** use measurable objectives and operational response rather than aspirational promises.
- **Multi-region/Kubernetes/sharding:** mark N/A with rationale if the needs do not justify them.

An item is not automatically PASS because a related vendor or package name appears in a dependency manifest.

### 5.3 The 139-topic count

The user began with a spoken list that was normalized and de-duplicated to 111 original concepts. The project subsequently **expanded** the review model with 28 fundamentals the original terms did not cover. This is why both the README and CSV say **139**, while the core engineering concept file is named **`111-CONCEPTS.md`**. Do not rewrite the history as if all 139 came from the dictation.

### 5.4 Which ideas were added as fundamentals

The 28 additions include acceptance criteria, non-functional requirements, architecture decision records, data models/constraints, ACID and isolation, authentication/authorization separation, role and tenant isolation, input validation, pagination, unit/integration/end-to-end/contract/load tests, linting and scans, code review, accessibility, runbooks, environment separation, audit logs, retention/deletion, restore drills, provider outages, AI-generated code verification, and avoiding secret leakage into AI prompts. Their exact published wording is in Section 8.

## 6. The launch checklist's actual decision process

Read `checklists/LAUNCH.md` in full. It has the following named sections and requirements:

1. **Scope and architecture** — document user journeys, trust boundaries, dependencies/failure modes, appropriate complexity, privacy and obligations.
2. **Correctness and data** — passing tests, server-side authorization, tenant isolation, input validation, migrations, query behavior, concurrent or repeated payments, pagination.
3. **Security** — secrets, least privilege, TLS and storage protection, common web threats, dependency vulnerability review, safe sessions, webhook verification.
4. **Reliability and performance** — deadlines/retries, idempotent jobs, measured load, abuse protection, safe caches, provider outages.
5. **Deployment and recovery** — repeatable CI/release, environment separation, readiness, rollback, **verified backup restoration**, RTO/RPO.
6. **Operating in production** — non-sensitive logging/metrics/tracing, actionable alerts, budget/quotas, incident process, smoke testing.
7. **Release decision** — fill in GO / NO-GO / GO WITH EXCEPTIONS, blockers, accepted risks with owners, evidence links, and approver.

The user requested a checklist developers can actually check, not a list of fashionable tools. This document is designed for actual project reviews; `N/A — reason` is an accepted outcome.

## 7. AI coding-agent audit behavior (exact expectations)

See `prompts/AI-AUDIT-PROMPT.md`. Key required semantics, included here to prevent agents from misusing it:

1. Read the target application's real code; determine language, framework, infrastructure, DB, auth model, integrations, deployment, and likely scale. If unobservable, say UNKNOWN.
2. Use the checklist as criteria, not as a demand to install technologies.
3. Report evidence with exact file paths and line numbers wherever possible.
4. Categorize severity `Critical`, `High`, `Medium`, `Low`.
5. Use statuses `PASS`, `FAIL`, `UNKNOWN`, `N/A`, with explanation.
6. Describe a failure mode and minimally invasive improvement for every relevant risk.
7. State the test, command, or manual check that would prove an improvement.
8. Provide architecture map, executive findings, release recommendation, prioritized fixes, remaining unknowns, and non-applicable controls.
9. **Do not modify source code unless explicitly asked.**
10. Do not reveal secrets accidentally discovered. Do not falsely claim a test was executed.

The prompt is **meant to be copied into an AI coding agent operating on an app under review**. It is not an unattended security certification or built-in enforcement service.

## 8. Original publication — exact full checklist inventory (2026-10-17)

**Preservation note:** The following sections reproduce the initial publication's full topic names, categorization, labels, and practical checks. This deliberately duplicates the historical state *inside this handoff document* to avoid replacing it with a vague "139 topics" summary. When the checklists change later, keep this as a historical snapshot, add new dated context and CHANGELOG entries, and treat live checklist files as authoritative.

### 8.1 All 111 original concepts and their testable checks — exact published text

## Preserved source title: 111 System Design Concepts — Practical Checklist

> A decision checklist, **not** a requirement to add every technology. For each item, evaluate relevance, implement a proportionate solution if needed, and attach test or operational evidence.

**Labels:** Baseline = usually useful; Contextual = depends on product requirements; Advanced = adopt only for a clear need.

## 1. Architecture, networking & APIs

- [ ] **Domain Name System (DNS)** `[Contextual]` — Confirm DNS resolution, TTL, and recovery plan.  
- [ ] **TCP vs. UDP** `[Advanced]` — Choose transport based on ordering, delivery, and performance needs.  
- [ ] **HTTP/2 and HTTP/3** `[Contextual]` — Check protocol support and measure client impact.  
- [ ] **gRPC** `[Advanced]` — Justify typed service calls; test deadlines and compatibility.  
- [ ] **Webhooks** `[Contextual]` — Verify signatures, retries, replay resistance, and duplicate deliveries.  
- [ ] **API versioning** `[Contextual]` — Define compatibility, versioning, and deprecation policies.  
- [ ] **Semantic versioning** `[Contextual]` — Document breaking, minor, and patch changes.  
- [ ] **Reverse proxies** `[Contextual]` — Validate forwarded headers, TLS termination, and routing.  
- [ ] **API gateway** `[Advanced]` — Define gateway responsibility, security, and routing.  
- [ ] **WebSockets** `[Contextual]` — Authenticate sockets; test reconnection and resource limits.  
- [ ] **Long polling** `[Contextual]` — Bound request duration and concurrency, handle backoff.  
- [ ] **Server-Sent Events (SSE)** `[Contextual]` — Test reconnection, event IDs, and proxy buffering.  
- [ ] **Latency** `[Baseline]` — Measure end-to-end response time from real clients.  
- [ ] **Throughput** `[Contextual]` — Load test expected useful requests or events per second.  
- [ ] **P99 latency** `[Contextual]` — Set a measurable P99 target for critical endpoints.  
- [ ] **Tail latency** `[Contextual]` — Inspect and control the slowest end-to-end requests.  
- [ ] **Network partitioning** `[Advanced]` — Define behavior when dependencies cannot be reached.  
- [ ] **Clock skew** `[Advanced]` — Avoid relying on synchronized clocks for correctness.  

## 2. Application reliability & concurrency

- [ ] **Rate limiting** `[Contextual]` — Enforce safe limits per IP, user, or token and test 429 handling.  
- [ ] **Timeouts** `[Baseline]` — Set connect, read, and overall deadlines for external calls.  
- [ ] **Retries** `[Contextual]` — Retry only transient and safe operations with bounded attempts.  
- [ ] **Exponential backoff** `[Contextual]` — Apply capped backoff with jitter.  
- [ ] **Idempotency** `[Baseline]` — Prove duplicate payments, orders, and jobs execute only once.  
- [ ] **Circuit breakers** `[Advanced]` — Stop retry storms during dependency outages.  
- [ ] **Backpressure** `[Contextual]` — Bound concurrency, work queues, and memory usage.  
- [ ] **Connection pooling** `[Contextual]` — Set pool caps, timeouts, and cleanup rules.  
- [ ] **Race conditions** `[Baseline]` — Test concurrent writes to critical shared state.  
- [ ] **Deadlocks** `[Contextual]` — Limit lock duration and add safe recovery strategies.  
- [ ] **Thread safety** `[Contextual]` — Review shared state and framework concurrency.  
- [ ] **Memory leaks** `[Contextual]` — Inspect long-running memory growth and resource cleanup.  
- [ ] **Garbage collection** `[Advanced]` — Measure heap behavior and pauses if they affect users.  

## 3. Messaging & workflows

- [ ] **Message queues** `[Contextual]` — Set delivery guarantees, retries, and worker concurrency.  
- [ ] **Publish/Subscribe (Pub/Sub)** `[Contextual]` — Document ordering and duplicate event handling.  
- [ ] **Event-driven architecture** `[Advanced]` — Version events and trace producers and consumers.  
- [ ] **Distributed transactions** `[Advanced]` — Identify workflows that span transactional boundaries.  
- [ ] **Saga patterns** `[Advanced]` — Define compensation and compensation failure handling.  
- [ ] **Dead letter queues (DLQs)** `[Contextual]` — Alert on poison jobs and provide safe replay.  
- [ ] **Cron jobs** `[Contextual]` — Specify timezone, retries, missed runs, and overlaps.  

## 4. Databases & consistency

- [ ] **Database indexing** `[Baseline]` — Index measured query paths and inspect write costs.  
- [ ] **Query optimization** `[Baseline]` — Examine explain plans for critical slow queries.  
- [ ] **N+1 queries** `[Baseline]` — Detect query-per-row patterns and optimize loading.  
- [ ] **Read replicas** `[Advanced]` — Know lag and read-after-write behavior.  
- [ ] **Sharding** `[Advanced]` — Justify partition keys and cross-shard complexity.  
- [ ] **Partitioning** `[Advanced]` — Verify partition pruning and retention strategy.  
- [ ] **Replication** `[Contextual]` — Understand durability, lag, and replica promotion.  
- [ ] **Leader election** `[Advanced]` — Prevent split-brain and define failover guarantees.  
- [ ] **CAP theorem** `[Advanced]` — Explain system behavior during network partitions.  
- [ ] **Eventual consistency** `[Contextual]` — Identify acceptable staleness and UX implications.  
- [ ] **Optimistic locking** `[Contextual]` — Test version checks against concurrent updates.  
- [ ] **Pessimistic locking** `[Contextual]` — Keep transactions and row locks short.  
- [ ] **Distributed locks** `[Advanced]` — Use safe leases and fencing when necessary.  
- [ ] **Database migrations** `[Baseline]` — Test backward-compatible migrations and rollback plans.  
- [ ] **Schema versioning** `[Contextual]` — Preserve compatibility across rolling versions.  
- [ ] **Backups** `[Baseline]` — Schedule backups and verify a real restoration.  

## 5. Infrastructure & scaling

- [ ] **Load balancing** `[Contextual]` — Configure health-based routing and justify sticky sessions.  
- [ ] **CI/CD** `[Baseline]` — Run repeatable tests, checks, and deployment steps.  
- [ ] **Docker** `[Contextual]` — Build pinned, minimal, non-root images.  
- [ ] **Kubernetes** `[Advanced]` — Use only if justified; set resource limits and probes.  
- [ ] **Service discovery** `[Advanced]` — Find healthy dynamic services without hardcoded hosts.  
- [ ] **Auto-scaling** `[Contextual]` — Select signals and test scaling ceilings and warm-up.  
- [ ] **Horizontal scaling** `[Contextual]` — Eliminate unnecessary node-local assumptions.  
- [ ] **Vertical scaling** `[Contextual]` — Estimate machine limits and cost trade-offs.  
- [ ] **Infrastructure as Code (IaC)** `[Contextual]` — Review infrastructure changes in version control.  
- [ ] **Terraform** `[Advanced]` — Pin providers, safeguard state, and review plans.  
- [ ] **Helm charts** `[Advanced]` — Validate charts and pin images and dependencies.  
- [ ] **Build caching** `[Contextual]` — Verify cache correctness and avoid leaking secrets.  
- [ ] **Dependency hell** `[Baseline]` — Lock versions and maintain tested upgrade paths.  
- [ ] **Multi-region deployment** `[Advanced]` — Plan residency, routing, and failover.  
- [ ] **Cold starts** `[Contextual]` — Measure cold-path response time.  
- [ ] **Serverless limits** `[Contextual]` — Review execution, payload, connection, and quota limits.  
- [ ] **Cost optimization** `[Baseline]` — Measure cost drivers and configure budgets.  

## 6. Performance & caching

- [ ] **Caching** `[Contextual]` — Select cache keys, TTL, eviction, and privacy protections.  
- [ ] **Content Delivery Networks (CDNs)** `[Contextual]` — Confirm caching policies and origin safeguards.  
- [ ] **Edge caching** `[Contextual]` — Prevent per-user information leaking to other users.  
- [ ] **Cache invalidation** `[Contextual]` — Define and test stale-data refresh or purge.  

## 7. Deployment strategies

- [ ] **Feature flags** `[Contextual]` — Maintain kill switches and remove obsolete flags.  
- [ ] **Blue-green deployment** `[Advanced]` — Document traffic cutover and backwards compatibility.  
- [ ] **Canary releases** `[Contextual]` — Use rollout cohorts and abort criteria.  
- [ ] **Rolling deployment** `[Contextual]` — Test mixed-version app/schema compatibility.  
- [ ] **Rollbacks** `[Baseline]` — Rehearse restoring a healthy release safely.  
- [ ] **Health checks** `[Baseline]` — Provide reliable status without exposing internals.  
- [ ] **Liveness and readiness probes** `[Contextual]` — Separate process health from traffic readiness.  

## 8. Observability & operations

- [ ] **Monitoring** `[Baseline]` — Track uptime and critical service health.  
- [ ] **Logging** `[Baseline]` — Use structured logs with correlation IDs and redaction.  
- [ ] **Distributed tracing** `[Contextual]` — Connect traces across services and critical calls.  
- [ ] **Metrics** `[Baseline]` — Measure errors, traffic, saturation, and latency.  
- [ ] **Alerts** `[Baseline]` — Make alerts actionable with an owner and runbook.  
- [ ] **Service Level Objectives (SLOs)** `[Contextual]` — Choose realistic reliability objectives.  
- [ ] **Service Level Indicators (SLIs)** `[Contextual]` — Define how reliability is actually measured.  
- [ ] **Error budgets** `[Advanced]` — Use acceptable downtime to guide release priorities.  
- [ ] **Observability** `[Baseline]` — Diagnose unfamiliar failures using signals together.  
- [ ] **Production incidents** `[Contextual]` — Define response roles, severity, and communication.  
- [ ] **On-call engineering** `[Contextual]` — Provide ownership, escalation, and safe access.  
- [ ] **Postmortems** `[Contextual]` — Document lessons and accountable follow-up actions.  

## 9. Security & identity

- [ ] **Secrets management** `[Baseline]` — Keep secrets out of Git, clients, and logs; rotate them.  
- [ ] **Identity and Access Management (IAM)** `[Baseline]` — Enforce least privilege and scoped identities.  
- [ ] **OAuth** `[Contextual]` — Validate redirects, state, and PKCE where appropriate.  
- [ ] **JWT rotation** `[Contextual]` — Verify audience, expiry, keys, and revocation limitations.  
- [ ] **TLS (Transport Layer Security)** `[Baseline]` — Use valid certificates on external endpoints.  
- [ ] **Encryption at rest** `[Baseline]` — Protect stored sensitive data and keys.  
- [ ] **Encryption in transit** `[Baseline]` — Encrypt sensitive service and client traffic.  
- [ ] **Web Application Firewall (WAF)** `[Contextual]` — Evaluate protections and false positives.  
- [ ] **DDoS protection** `[Contextual]` — Understand provider protections and response procedures.  
- [ ] **Cross-Origin Resource Sharing (CORS)** `[Baseline]` — Allow intended origins and credential rules only.  
- [ ] **Cross-Site Request Forgery (CSRF)** `[Baseline]` — Protect cookie-authenticated browser mutations.  
- [ ] **SQL injection** `[Baseline]` — Parameterize SQL and test untrusted inputs.  
- [ ] **Cross-Site Scripting (XSS)** `[Baseline]` — Escape output and avoid unsafe DOM sinks.  
- [ ] **Server-Side Request Forgery (SSRF)** `[Contextual]` — Restrict URL fetches and internal metadata access.  

## 10. Resilience & recovery

- [ ] **Disaster recovery** `[Contextual]` — Define recovery time and data-loss objectives; practice.  
- [ ] **Failover** `[Contextual]` — Test switching to a healthy dependency or replica.  
- [ ] **Chaos engineering** `[Advanced]` — Run bounded, controlled failure exercises.  


### 8.2 All 28 additional fundamentals and their testable checks — exact published text

## Preserved source title: 28 Additional Engineering Fundamentals

These complement the 111 system-design concepts with essential correctness, security, and maintenance practices. Review relevance and evidence rather than checking boxes blindly.

- [ ] **Requirements and acceptance criteria** — Document expected behavior and pass/fail tests.  
- [ ] **Non-functional requirements** — Define availability, performance, privacy, and cost targets.  
- [ ] **Architecture decision records** — Document major alternatives and trade-offs.  
- [ ] **Data modeling and constraints** — Define keys, relationships, and invariants.  
- [ ] **ACID transactions** — Use transactions for coordinated related writes.  
- [ ] **Transaction isolation** — Test anomalies such as lost updates and write skew.  
- [ ] **Authentication vs. authorization** — Check identity and resource permissions separately.  
- [ ] **Role-based/access policies** — Enforce access rules on the server and database.  
- [ ] **Multi-tenancy and data isolation** — Verify cross-customer data cannot be accessed.  
- [ ] **Input validation** — Validate formats, size, and business rules at boundaries.  
- [ ] **Pagination and bounded queries** — Prevent unbounded API and database responses.  
- [ ] **Unit tests** — Cover critical logic and edge cases.  
- [ ] **Integration tests** — Test databases, queues, APIs, and authentication together.  
- [ ] **End-to-end tests** — Test essential user journeys in realistic environments.  
- [ ] **Contract tests** — Validate interfaces between services and clients.  
- [ ] **Load testing** — Identify peak load and first bottlenecks.  
- [ ] **Static analysis and linting** — Run code checks in CI.  
- [ ] **Dependency and image scanning** — Investigate known vulnerabilities.  
- [ ] **Code review** — Use human review for security and important logic.  
- [ ] **Accessibility** — Test keyboard support, labels, and contrast.  
- [ ] **Documentation and runbooks** — Document setup, deployment, and recovery.  
- [ ] **Environments and configuration** — Separate production settings and credentials.  
- [ ] **Audit logs** — Record sensitive changes with actor and timestamp.  
- [ ] **Data retention and deletion** — Define collection, retention, and deletion rules.  
- [ ] **Restore and recovery drills** — Prove a backup can actually be restored.  
- [ ] **External integrations and provider outages** — Handle third-party quotas and downtime.  
- [ ] **AI-generated code verification** — Review and test generated output instead of trusting claims.  
- [ ] **AI prompts and secret exposure** — Prevent secrets and personal data in prompts and logs.  


## 9. Learning plan and actual use cases

The current `checklists/LEARNING-ROADMAP.md` defines these **seven progressive stages** (the order matters more than memorizing buzzwords):

1. Build: Git, HTTP, API design, relational data, auth; build a two-role CRUD API.
2. Make it correct: test logic and data invariants, transactions, migrations and idempotency; simulate duplicate orders/concurrency.
3. Deploy: repeatable CI/CD, configuration and secrets, optional Docker, HTTPS, smoke tests.
4. Survive failure: simulate dependency outages, verify recovery and backups.
5. Improve performance: measure slow queries and traffic; tune indexes/caches/rate limits.
6. Add asynchronous behavior: use queues, DLQs, webhooks, cron, consistency only when needed; recover a failed job safely.
7. Go distributed when needed: learn CAP, sagas, elections, sharding, multi-region; demonstrate real trade-offs.

A short weekly exercise picks one topic, explains its failure mode and when not to use it, builds a tiny test, records evidence, and teaches the principle plainly. No course platform or interactive tracker has been built as part of this repository.

## 10. Git history, exact commits, and work sequence

### 2026-10-17 — repository before the full checklist

- The user identified `https://github.com/aiwithenoch/vibecodingchecklist.git` as the **target** repository. The actual GitHub namespace and spelling are `aiwithenoch/vibecodingchecklist` (not the earlier working title `vibe-coding-checklist`).
- The repo existed, public, under the user's own account and was writable.
- Initial commit: [`65592d10ef7843377eb78d8e3eee298d44932e89`](https://github.com/aiwithenoch/vibecodingchecklist/commit/65592d10ef7843377eb78d8e3eee298d44932e89). At inspection it contained a minimal `README.md` titled `# vibecodingchecklist`.
- Another GitHub repository called `aiwithenoch/system-design-for-vibe-coders` was seen during repository discovery, but **the user-selected `aiwithenoch/vibecodingchecklist` is the repository modified**.

### 2026-10-17 13:28:45 UTC — initial complete publication

- Commit: [`49939675720dea81ff07b665f7f29d458d6064f2`](https://github.com/aiwithenoch/vibecodingchecklist/commit/49939675720dea81ff07b665f7f29d458d6064f2).
- Exact commit message: `docs: publish complete Vibe Coding Checklist (139 topics)`.
- Parent: `65592d10ef7843377eb78d8e3eee298d44932e89`.
- Published **13 files**, exactly: `README.md`, `checklists/111-CONCEPTS.md`, `checklists/ESSENTIALS.md`, `checklists/LAUNCH.md`, `checklists/LEARNING-ROADMAP.md`, `checklists/TOPICS.csv`, `prompts/AI-AUDIT-PROMPT.md`, `templates/PROJECT-AUDIT.md`, `CONTRIBUTING.md`, `LICENSE`, `.gitignore`, `.github/ISSUE_TEMPLATE/checklist-improvement.md`, and `.github/PULL_REQUEST_TEMPLATE.md`.
- The Git ref `main` was updated non-forcefully and published content was then read back from GitHub for verification.
- The publication was a docs and data release, not an app deployment or exercise of the audit prompt against another project.

### 2026-10-19 — long-form agent handoff requested

- The user explicitly requested `CHANGELOG.md` and `CONTEXT.md` and said **not to summarize** the context another agent needs.
- GitHub's `main` head before this change was still `49939675720dea81ff07b665f7f29d458d6064f2`; the checked `CHANGELOG.md`, `CONTEXT.md`, and `AGENTS.md` paths were absent.
- This change **adds** these three root documents and **updates** `README.md` to link to them.
- It does **not** modify, reorder, mark complete, or remove any checklist items, audit instructions, or CSV rows.
- This documentation-only handoff is committed on `main`; the actual commit SHA is available in Git history. Do not invent a SHA before GitHub returns it.
- Validate after publishing that all three files exist, the README links resolve, and all 139 topics remain intact.

## 11. Precise change protocol for future agents

### 11.1 Before editing

1. Read `README.md`, **all** of `AGENTS.md`, **all** of `CONTEXT.md`, and **all** of `CHANGELOG.md`.
2. Inspect the target branch's current state and the exact user request. Never overwrite unexpected changes or force-push.
3. Read all affected files fully; do not operate from a search snippet or this historical inventory alone.
4. Preserve spelling of the chosen repo and named file paths exactly.
5. Decide whether requested work is editorial documentation, adding checklist entries, a software implementation, or an audit of an external project; these are different scopes.
6. Identify and disclose unanswered questions and unknowns instead of guessing.

### 11.2 When adding or changing checklist topics

1. Update the relevant Markdown file(s) with a concrete verification check and sensible grouping.
2. Update `checklists/TOPICS.csv` **in the same change** to reflect topic names, type, group, metadata, and practical check.
3. Recompute counts: original items, additions, CSV data rows and total. Do not leave an outdated `README.md` count.
4. Check for case-insensitive duplicates, unclear aliases, and conflicting recommendations.
5. Respect the philosophy: no recommendation of unjustified architecture merely to pass a checkbox.
6. Add a dated, specific `CHANGELOG.md` entry listing files and important behavior/content changes.
7. Append a dated section in `CONTEXT.md` capturing new decisions and why they were made; do not condense or erase the previous historical context.
8. If the new material changes how agents should work, update `AGENTS.md`.

### 11.3 Validation that another agent should perform

- Inspect the generated Markdown links (relative paths) and all new root documentation paths.
- Verify **111** checkbox topics in `checklists/111-CONCEPTS.md`, **28** checkbox topics in `checklists/ESSENTIALS.md`, and **139** data records in the CSV for the initial release. For future releases verify whatever the updated counts are.
- Verify CSV headers exactly: `Type`, `Section`, `Topic`, `Priority`, `Practical check`.
- Compare each CSV `Topic` and `Practical check` against the equivalent Markdown item, allowing only intentional, documented transformations.
- Ensure checked-off implementation items in user projects have real evidence; the reference project should not claim that it validated apps.
- Inspect the pushed commit and check that GitHub reads of affected files return the expected content. If a write fails, report the failure and **do not** claim success.

### 11.4 Suggested local validation command (Python standard library)

```bash
python - <<'PY'
import csv, pathlib, re
root = pathlib.Path(".")
original = (root / "checklists/111-CONCEPTS.md").read_text(encoding="utf-8")
additional = (root / "checklists/ESSENTIALS.md").read_text(encoding="utf-8")
with (root / "checklists/TOPICS.csv").open(encoding="utf-8", newline="") as f:
    rows = list(csv.DictReader(f))
assert len(re.findall(r"^- \[ \] ", original, re.M)) == 111
assert len(re.findall(r"^- \[ \] ", additional, re.M)) == 28
assert len(rows) == 139
assert sum(row["Type"] == "Original" for row in rows) == 111
assert sum(row["Type"] == "Additional" for row in rows) == 28
for path in ["README.md", "CONTEXT.md", "CHANGELOG.md", "AGENTS.md"]:
    assert (root / path).exists(), path
print("Documentation inventory checks passed")
PY
```

This command is **documentation inventory validation** only. It is not an automated security audit or test of any application. When the topic count changes, adjust the hard-coded initial release expectations and record the change.

## 12. Current collaboration, release, and licensing details

- GitHub repo is **public**, owner `aiwithenoch`. Follow normal GitHub branch/PR review practices where useful.
- The source and contribution terms are MIT, not a proprietary course license.
- The README links to AI With Enoch's learning community at https://community.aiwithenoch.com.
- The materials are designed to be forked, reused, or adopted in another repository; they should not imply the author officially certifies third-party apps.
- Future improvements can include examples, stack-specific reference implementations, learning exercises, GitHub template metadata, automated validation, or an interactive UI. **None are presumed approved or implemented merely because they sound useful.**
- The user may later wish to make this a GitHub template repository. A previous assistant **recommended** that, but there was no confirmation that the GitHub template setting was successfully enabled. Verify configuration before claiming it.
- Contributors should use realistic failure scenarios, honest trade-offs, and testable outcomes, without posting secrets or client data.

## 13. Full handoff: what a newly assigned agent must do next

For a request that starts with "continue the vibe coding checklist", do all of the following rather than giving an abbreviated recap:

1. Read these four root docs in full and determine which file(s) are authoritative for the user's specific request.
2. Read `checklists/111-CONCEPTS.md`, `checklists/ESSENTIALS.md`, and the CSV when the request changes the topic inventory.
3. Consult the live project's launch, roadmap, AI audit, and report template when the request pertains to audits, teaching, or evidence-based engineering.
4. Explain whether the work is already in GitHub before editing, and preserve the branch/repo path.
5. Carry out requested modifications with minimum unrelated changes.
6. Validate them in the actual repository and report commit hash/links once GitHub confirms the write.
7. Record a **specific, dated** change in `CHANGELOG.md` and append new decisions to `CONTEXT.md`.
8. Never replace this detailed document with a short summary, remove the original requirements, or falsely imply unimplemented functionality exists.

**End of original handoff record. Add new dated sections as the project evolves.**


## 14. 2026-10-20 — Performance transcript, Community code audit, and checklist extension

### 14.1 Exact user direction and repository identity

The user supplied a timestamped 29-minute transcript file, asked for it to be checked against the Community code and GitHub, and requested the selected checklist repository be updated without shortening away details or replacing history. The exact request was:

```text
check this transcript again my code adn also check my github and update my cibe coding checklist repo dont try to summerize pu tall detaisl and memefy globally so all my cidex session can use this
```

The user then identified the exact target repository:

```text
thisis the one https://github.com/aiwithenoch/vibecodingchecklist.git
```

Canonical target: `aiwithenoch/vibecodingchecklist`. This is distinct from any similarly named checklist or system-design repository. Only this user-selected documentation repository is changed by this task.

### 14.2 Supplied transcript provenance and full technical content

- Source attachment: `/Users/admin/.codex/attachments/f44eee22-7259-4ad6-bd54-805060355a42/Pasted text.txt`.
- The attachment is a timestamped transcript from 00:00 through 29:00, approximately 147 lines and 24,937 bytes. It describes a Lovable/React performance demonstration, not a measured audit of Enoch's deployed Community application.
- The full timecoded evidence map is in `checklists/PERFORMANCE-AND-RENDERING.md`. It preserves the complete sequence and the implementation failures/caveats rather than presenting only the video's final claim. Key phases:
  - 00:00–01:43: page seems slow/flashes; presenter inspects browser Network; separates hover-triggered image prefetch from first-load requests; reports many initial image requests.
  - 01:44–04:51: adds native lazy loading, then says requests/scroll behavior remain confusing; suggests possible prefetch and missing dimensions. Those are hypotheses until actual requests/markup are inspected.
  - 04:52–06:35: proposes width/height, CSS aspect ratio, optional IntersectionObserver; presenter later reports more progressive loading but provides no request totals or timings.
  - 06:36–12:21: host/camera slows; asks an AI to inspect rerenders, memory leaks, listeners, context and inline style objects; suspects React effect/state issues and claims listeners/recursive work exhaust memory. No profiler, heap timeline, controlled comparison, or leak proof is shown.
  - 12:22–15:23: sees roughly 100 DOM list items and suggests “never more than 12” via virtual scrolling; the first implementation has non-working scroll events, flashing, and poor behavior. The number is an example, not a universal target.
  - 15:24–18:30: reports animation replay on remount, staggered fade, state reset, closures, masonry/row-virtualizer geometry mismatch; proposes larger overscan and less animation.
  - 18:31–20:25: scroll appears stuck and more items stop loading; diagnosis is speculative and needs instrumentation at the visible-range/continuation boundary.
  - 20:26–22:29: suggests viewport-dependent overscan and loading ahead, while overgeneralizing that every app needs virtualization.
  - 23:09–25:32: later attempt adds skeletons but has sideways grid behavior; shifts to normal rows and complete-row/visible-range calculation.
  - 25:33–29:00: reports down/up scrolling and DOM recycling, inspects nodes, and ends by warning about cleanup/memory. These are qualitative claims, not measured before/after results.
- Important corrections encoded in the guide: intrinsic dimensions/aspect ratios reserve layout and reduce layout shift and can prevent zero-size lazy-image cases; they are not the sole explanation for every eager request. Native loading thresholds vary by browser. Check preload/prefetch, CSS backgrounds, mount behavior, actual viewport and request initiators. Lazy-load only appropriate offscreen content; do not delay the important LCP image.
- Virtualization is conditional on measured DOM/render work. It does not reduce database/API payload or full in-memory arrays by itself. There is no universal “12 items” cap or requirement to virtualize every app. Stable keys, complete row geometry, adaptive overscan, scroll-up/down, loading continuation, focus/accessibility, state preservation, remount animations, and observer/listener cleanup are required validation cases.
- The transcript does not contain controlled request counts, bytes, LCP/INP/CLS numbers, device/network configuration, heap evidence, production traffic, or a verified library. Its claims cannot be used as test results for Enoch's code.

### 14.3 Community application code audit scope and limitations

- The separate local application checkout audited read-only is `/Users/admin/Documents/Codex/2026-08-11/ne/frappe-lms`, branch `develop`, starting commit `91bc5478a766a111fc163d906274848c157bd978`. It already had 295 modified/untracked paths. Preserve all existing changes.
- The source-level evidence and detailed app-specific findings are appended to that project's `frontend/changelog.md`; the public checklist repo does not publish uncommitted application findings. No application source, database, payment state, provider configuration, or deployment was changed in this task.
- A separate GitHub source repo, `aiwithenoch/ai-with-enoch-community`, was inspected at main tree commit `e33ce865d106e7aa0e911a22d576ea0c6cbfbc9a`. Its README describes a Frappe LMS Community UI preview using sample data while the Frappe backend is not connected. Do not treat this preview commit as proof of the deployed application's runtime or backend.
- No browser Network/Performance recording, field Web Vitals, heap timeline, realistic load test, or performance change was run for this transcript review. Any previous build or production audit entry in the Community project's changelog is separate and should not be presented as if rerun here.
- Framework-specific caution: the user app is Vue 3, whereas the transcript's AI discussion references React hooks. Use lifecycle cleanup and profiling appropriate to the actual framework; do not cargo-cult useEffect/useState advice into Vue.

### 14.4 Exact checklist-repository changes

This documentation-only update is on branch `docs/performance-rendering-review`, based on main commit `67c3128bd6b643eea2129f1862a703e6237e22f6`:

- Added `checklists/PERFORMANCE-AND-RENDERING.md`: baseline methodology; request/asset measurement; cold/warm/cache and hover/prefetch separation; image sizing/responsive loading; media/iframe handling; N+1 versus large batch responses; DB/API/UI bounds and cursor pagination; measured virtualization; scroll/geometry/accessibility tests; profiler-guided re-rendering; lifecycle cleanup; acceptance matrix; transcript timecode evidence map; and primary technical references.
- Updated `README.md` with a resource link.
- Updated `AGENTS.md` to require evidence-first performance review and link the new guide.
- Updated `checklists/LAUNCH.md` with critical resource, pagination/render, lifecycle, and justified-virtualization checks.
- Updated `templates/PROJECT-AUDIT.md` with page-load/media and bounded-data/rendering evidence rows.
- Updated `prompts/AI-AUDIT-PROMPT.md` with the new guide and specific performance evidence requests.
- Appended this detailed record to `CONTEXT.md` and a dated entry to `CHANGELOG.md`; prior content remains intact.
- Left `checklists/111-CONCEPTS.md`, `checklists/ESSENTIALS.md`, and `checklists/TOPICS.csv` untouched. The pre-edit counts were 111, 28, and 139 records respectively. This is a deeper practical guide to existing topics, not an expansion of the taxonomy.
- Primary references reviewed: MDN image/lazy-loading/observer/listener documentation, Vue performance guidance, and Chrome DevTools Network/Performance guidance.

### 14.5 Validation record and next agent actions

- Before editing, read all 528 lines of `CONTEXT.md`, all of `AGENTS.md`, all of `CHANGELOG.md`, the full README, and all affected launch checklist, essentials, AI prompt, report template, original topic file, and CSV. Repository instructions require this complete-read workflow.
- Confirmed GitHub repository owner/account `aiwithenoch`, public visibility, write permission, default branch `main`, and no open PR at the time of inspection.
- Created branch `docs/performance-rendering-review` from `67c3128bd6b643eea2129f1862a703e6237e22f6`. Main was not directly edited. Each of the eight documentation writes must be read back before the PR is described as complete.
- Re-validate relative Markdown links and the existing inventory counts 111 + 28 = 139. Confirm the CSV header and data rows are unchanged. Check all staged branch file contents against intended content.
- Open a pull request only after read-back verification. The public main branch will remain unchanged unless that PR is merged. Do not claim the app was made faster; this work updates the review process only.
- Memfy must store the original user request/correction, supplied transcript provenance, complete relevant conversation evidence, application audit scope/results, precise repository/branch/files, validation, and final PR status so other Codex sessions can retrieve it without replacing the raw historical record.


### 14.6 Final GitHub outcome after verification

- PR: [#1 — Add measured performance and rendering review](https://github.com/aiwithenoch/vibecodingchecklist/pull/1). The PR was opened from `docs/performance-rendering-review` and merged by squash.
- GitHub returned merge commit `4a41807ca37478df5b5ab5da8b54baa20b70df9d`; the merged files were read back from `main`.
- Read-back: all 11 checked files matched their intended contents. Relative Markdown paths in the changed docs resolved. The 111 and 28 Markdown checklist counts and 139-record CSV stayed unchanged; no inventory file was modified.
- GitHub reported no workflow runs for the PR head. Documentation/static link/count checks were performed; no application test suite, browser performance trace, or production load benchmark was run.
- The selected repository's main branch now contains the documentation update. The Community application's working tree remains unchanged by this checklist work, and no deployment occurred.
