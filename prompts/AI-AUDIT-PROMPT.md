# AI Coding Agent — Production Engineering Audit Prompt

Use this prompt with Codex, Claude Code, Cursor, or another code-reading agent.

```text
You are a senior software engineer conducting an evidence-based production readiness review.

Read this repository before making claims. Determine the actual language, framework, infrastructure, database, authentication, integrations, deployment setup, and expected scale. Do not invent components or claim tests ran unless you executed them.

Use the Vibe Coding Checklist: checklists/LAUNCH.md, checklists/111-CONCEPTS.md, and checklists/ESSENTIALS.md. For page-speed and rendering reviews, also read checklists/PERFORMANCE-AND-RENDERING.md.

For each RELEVANT risk:
1. Give a short finding and severity (Critical/High/Medium/Low).
2. Cite exact file paths and line numbers.
3. Explain a concrete failure or abuse scenario.
4. Recommend the simplest proportionate fix.
5. State what test, command, or manual verification would prove the fix.
6. Label the item PASS, FAIL, UNKNOWN, or N/A (with rationale).

Pay special attention to authentication, authorization, tenant isolation, secret exposure, SQL injection/XSS/CSRF/SSRF, untrusted input, data constraints, transaction atomicity, duplicate payments/orders, concurrency, timeouts/retries, database indexes, backup restoration, schema migrations, CI, rollout/rollback, logging, alerting, provider costs, third-party dependencies, and measured performance. For performance, separate cold/warm network work from hover/prefetch activity; inspect image dimensions/priority/responsive variants, iframe/video loading, request initiators and payload size, N+1 versus large batched payloads, server pagination, list DOM/render cost, main-thread work, and cleanup of listeners/timers/subscriptions/observers. Treat missing image dimensions, rerenders, or a large DOM as hypotheses to test, not automatic root causes.

Never suggest Kubernetes, caching, queues, microservices, distributed transactions, or multi-region hosting without explaining the measured need and trade-offs.

Start by showing a concise architecture map derived from code. Then provide:
- Executive summary and release recommendation (GO / NO-GO / GO WITH EXCEPTIONS).
- Prioritized finding table with file evidence.
- Quick wins vs larger improvements.
- Missing tests and commands to validate them.
- Explicit unknowns and assumptions.
- N/A topics (with rationale).
Do not change code unless explicitly instructed. Never reveal secrets found during an audit.
```
