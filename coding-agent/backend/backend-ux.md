# RCF - Back-end / Back-end UX Design

> The infrastructure that keeps the back-end pleasant to operate: automation, security health checks, pentest harnesses. Consult this file before bolting on a new background job, CI gate, or security check.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Pre-deploy security health check (CI gate)

**Project fit:** Production deploy pipeline. Runs dependency-vuln scan, secret scan, IaC linter, and a smoke pentest against a staging URL. Fails the pipeline on any HIGH finding.

**Value:**

> _(Add your tested CI workflow here - the exact `.github/workflows/security.yml` or equivalent, including which scanners you trust, severity thresholds, and the report format you publish to PRs.)_

---

## Context Relevancy: Background job queue with retry + exponential backoff

**Project fit:** Any service that handles webhooks, sends email, or runs long-tail work outside the request lifecycle. Retries on transient failure, dead-letters after N attempts, exposes a metrics endpoint.

**Value:**

> _(Add your tested queue worker here - driver choice, retry curve, DLQ handling, idempotency contract for handlers, and the observability hooks you depend on.)_
