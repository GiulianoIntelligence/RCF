# RCF - Back-end / APIs

> Route handlers, request validation, response shapes, error formats. Consult this file before adding any new endpoint or webhook.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Idempotent REST POST handler

**Project fit:** Any write endpoint where the client may retry on network failure (payments, order creation, anything that mutates billable state). Honors an `Idempotency-Key` header and returns the original response on retry.

**Value:**

> _(Add your tested idempotency wrapper here - header parsing, key→response cache, TTL, and the locking strategy you use to serialize concurrent retries with the same key.)_

---

## Context Relevancy: Stripe webhook handler

**Project fit:** SaaS using Stripe Billing. Verifies the signature, dispatches by event type, returns 200 within the timeout, defers heavy work to a queue.

**Value:**

> _(Add your tested Stripe webhook receiver here, including signature verification, event-type router, replay guard via `event.id`, and the queue handoff for long-running side effects.)_
