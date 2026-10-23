# Project Production Readiness Audit

**Project:**  
**Repository:**  
**Owner:**  
**Date:**  
**Reviewed commit:**  
**Reviewers:**  
**Environment:**  
**Expected traffic and critical workflows:**  

## Architecture overview

Describe entry points, data stores, trust boundaries, background jobs, external providers, and deployment environment.

## Security review record

**Mode:** Guidance / Full audit
**Profile:** Quick / Standard / Deep
**Scope and exclusions:**
**Reviewed source ref and worktree state:**
**Sandbox and local-only execution controls:**
**Coverage ledger / prior-run references:**

For every security candidate, record the lower-trust principal, accepted input or action, intended control, crossed boundary, affected resource, and observable result. Do not assign severity until the result is demonstrated.

| Candidate fingerprint | Principal and input | Boundary / intended control | Affected resource | Evidence and bounded result | Verdict |
| --- | --- | --- | --- | --- | --- |
| | | | | | `confirmed` / `needs_validation` / `rejected` |

**Security evidence notes:**

**Unknown deployment facts and owner-observed validation plans:**

**Out-of-scope or deferred coverage:**

## Evidence-based findings

| Topic | Status (PASS/FAIL/UNKNOWN/N/A) | Severity | Evidence / file / test | Owner | Due date |
| --- | --- | --- | --- | --- | --- |
| Authentication and authorization | UNKNOWN | High | | | |
| Database integrity and migrations | UNKNOWN | High | | | |
| Idempotent critical operations | UNKNOWN | High | | | |
| Security and secrets | UNKNOWN | High | | | |
| Tests and CI | UNKNOWN | Medium | | | |
| Backups and restoration | UNKNOWN | High | | | |
| Deployment and rollback | UNKNOWN | Medium | | | |
| Monitoring and incident response | UNKNOWN | Medium | | | |
| Bounded queries, pagination, and large-list rendering | UNKNOWN | Medium | | | |
| Page-load requests, image/media behavior, and layout stability | UNKNOWN | Medium | | | |

## Release decision

**GO / NO-GO / GO WITH EXCEPTIONS:**

**Blockers:**

**Accepted risks, reasons, and responsible owners:**

**Verification plan:**

**Rollback/recovery plan:**

**Approval:**
