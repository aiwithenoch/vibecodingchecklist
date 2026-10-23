# Vibe Coding Checklist

**Build it with AI. Understand it like an engineer. Ship it with confidence.**

An open-source **production engineering and system design checklist** for people who write code manually *and* people who use AI coding tools such as Codex, Claude Code, Cursor, or others.

**139 review topics:** the original **111 system design concepts** plus **28 fundamental engineering practices**.

> **Important:** This is a review framework, **not a shopping list**. A simple business app may need secure authorization, idempotent payments, safe database migrations, monitoring, and backups without ever needing Kubernetes, sharding, or distributed sagas.

## Project history & agent handoff

**Continuing work with a coding agent?** First read [AGENTS.md](AGENTS.md), then the complete [CONTEXT.md](CONTEXT.md) and [CHANGELOG.md](CHANGELOG.md). These files preserve the original requested list, all initial 139 published checks, the exact GitHub history, editorial decisions, existing work, current limitations, and the required change protocol. **Do not replace the handoff with a short summary.**

## Start here

| Resource | What it does |
| --- | --- |
| [🚀 Production launch checklist](checklists/LAUNCH.md) | Practical release-readiness checks |
| [🛡️ Security audit review](checklists/SECURITY-AUDIT.md) | Evidence-first security review, safe validation, coverage, and reporting |
| [⚡ Performance and rendering review](checklists/PERFORMANCE-AND-RENDERING.md) | Measure image, data, rendering, virtualization, and lifecycle risks |
| [🧩 111 system design concepts](checklists/111-CONCEPTS.md) | Grouped, testable engineering topics |
| [🧱 28 additional essentials](checklists/ESSENTIALS.md) | Testing, data integrity, AI code verification, and more |
| [📚 Learning roadmap](checklists/LEARNING-ROADMAP.md) | Build skills progressively through projects |
| [🤖 AI coding-agent audit prompt](prompts/AI-AUDIT-PROMPT.md) | Analyze actual code rather than trusting generated claims |
| [📋 Project audit template](templates/PROJECT-AUDIT.md) | Evidence, owner, release decision, and exceptions |
| [📊 Topics dataset](checklists/TOPICS.csv) | Searchable 139-topic CSV |

## How to use this checklist

1. Copy the [project audit template](templates/PROJECT-AUDIT.md) into your project.
2. Review the [launch checklist](checklists/LAUNCH.md) before production.
3. Use the detailed topics to investigate your actual risk and architecture.
4. Link evidence from tests, configuration, query plans, CI results, or dashboards.
5. Mark non-applicable items **N/A with a reason**; do not add technology just to tick a box.

## What counts as done?

- **Idempotency:** retry an order/payment and verify only one real-world effect.
- **Backups:** restore the latest backup in an isolated environment and inspect its data.
- **Authorization:** confirm a user cannot read or modify another user's records.
- **Rate limiting:** exceed the threshold and confirm predictable throttling.
- **Monitoring:** trigger a safe failure and verify the owner receives the signal.

## Who this is for

**Vibe coders, traditional developers, engineering teams, code reviewers, educators, and AI-assisted builders.** The essential skill is understanding and verifying engineering decisions, regardless of who typed the code.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md). Strong contributions add measurable checks, real failures, and clear trade-offs.

Released under the [MIT license](LICENSE). Educational guidance; adapt it to your technology and legal obligations.

---

Made for the **AI With Enoch** learning community. [Join here](https://community.aiwithenoch.com).
