# 111 System Design Concepts — Practical Checklist

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
