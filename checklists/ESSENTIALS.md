# 28 Additional Engineering Fundamentals

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
