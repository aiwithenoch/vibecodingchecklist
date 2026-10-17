# Learning Roadmap — Build, Test, Break, Improve

Do not memorize buzzwords. Learn concepts by building something, testing failures, and explaining trade-offs.

| Stage | Topics | Proof project |
| --- | --- | --- |
| 1. Build | Git, HTTP, API design, relational data, authentication | CRUD API with two roles |
| 2. Make it correct | Unit/integration tests, ACID, constraints, migrations, idempotency | Simulate duplicate orders and concurrent edits |
| 3. Deploy | CI/CD, configuration, secrets, Docker if needed, HTTPS | Repeatable deployment with smoke tests |
| 4. Survive failure | Timeouts, retries, monitoring, backups and restore | Disable dependencies; recover and measure |
| 5. Improve performance | Indexing, query plans, cache, load testing, rate limits | Benchmark before and after |
| 6. Add async | Queues, DLQs, webhooks, cron, eventual consistency | Recover a failed job without duplicate effects |
| 7. Go distributed when necessary | CAP, sagas, leader election, sharding, multi-region | Explain and test a specific distributed failure |

**A simple, reliable monolith often beats a needlessly complex microservice system.**

## Weekly exercise

1. Pick one item from [111-CONCEPTS.md](111-CONCEPTS.md).
2. Explain the failure mode and when the concept is unnecessary.
3. Build a tiny test or example.
4. Record metrics, evidence, and trade-offs.
5. Teach it in plain English.
