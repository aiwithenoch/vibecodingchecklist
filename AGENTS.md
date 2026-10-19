# AGENTS.md — Required Reading and Editing Contract

These instructions apply to the **entire** `aiwithenoch/vibecodingchecklist` repository and to every AI agent working in it.

## Read in this exact order before edits

1. Read **all of** [CONTEXT.md](CONTEXT.md), **including the verbatim user request, full original 139-item publication snapshot, decisions, chronology, file inventory, scope constraints, and handoff protocol**. Never treat a short excerpt or summary as equivalent.
2. Read **all of** [CHANGELOG.md](CHANGELOG.md) to understand what was changed, when, and why.
3. Read [README.md](README.md) and every checklist/prompt/template affected by the current request.
4. Inspect the actual repository/branch state and current user instructions. The live files take precedence over historical snapshots for present wording.

## Hard requirements

- **Do not compress, summarize away, or erase existing historical context or changelog entries.** Append dated factual history; revise factual errors explicitly, without hiding what happened.
- The project is **for both traditional developers and AI-assisted/vibe coders**; keep both audiences visible.
- It is currently a **documentation/checklist repository**, not a deployed scanner or application. Never claim an app exists or checks were run without evidence.
- Preserve the original **111-topic** inventory and **28 extra fundamentals** unless the user explicitly requests a change. Keep Markdown topics, CSV rows, and README counts synchronized.
- Every check should be understandable, testable, and relevant to real production risks. **N/A with rationale** is valid. Do not demand Kubernetes, microservices, distributed sagas, caching, etc. for every application.
- In audits, distinguish `PASS`, `FAIL`, `UNKNOWN`, and `N/A`, give file/line evidence, and never invent proof. Do not modify an audited user's project without authorization.
- Never put secrets, private tokens, user/customer data, or credentials in examples, prompts, documentation, or logs.
- Keep changes scoped and inspect unexpected existing modifications. Avoid force-pushing or overwriting concurrent edits.
- Update `CHANGELOG.md` with dates, precise affected files, rationale and verification for every meaningful change. Update `CONTEXT.md` with decisions and handoff facts.

## Topic changes checklist

- [ ] Read the live `checklists/111-CONCEPTS.md` / `checklists/ESSENTIALS.md`.
- [ ] Maintain `checklists/TOPICS.csv` alongside changed topics.
- [ ] Check case-insensitive duplicates and terminology precision.
- [ ] Confirm counts and update `README.md` if the inventory changed.
- [ ] Validate relevant relative Markdown links.
- [ ] Record factual change details in `CHANGELOG.md` and durable decisions in `CONTEXT.md`.
- [ ] Verify the changed files in GitHub or the checked-out repository before reporting success.

## Main resource map

- [Original 111 topics](checklists/111-CONCEPTS.md)
- [28 additional fundamentals](checklists/ESSENTIALS.md)
- [Production launch review](checklists/LAUNCH.md)
- [Learning roadmap](checklists/LEARNING-ROADMAP.md)
- [AI audit prompt](prompts/AI-AUDIT-PROMPT.md)
- [Audit template](templates/PROJECT-AUDIT.md)
- [Machine-readable topic inventory](checklists/TOPICS.csv)
- [Contributor guide](CONTRIBUTING.md)

**If you are a new agent: read the full CONTEXT.md rather than asking the user to retell this project's history.**
