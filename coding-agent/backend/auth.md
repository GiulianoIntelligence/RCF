# RCF - Back-end / Auth

> Authentication and session-related code: sign-in flows, token issuance, middleware, password handling. Consult this file before writing any new auth path.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Email + magic-link sign-in

**Project fit:** Consumer app where passwordless is acceptable. Sends a single-use token by email, redeems it on click, issues a session cookie.

**Value:**

> _(Add your tested magic-link issuer + verifier here, including token TTL, single-use guarantee, rate limit per email, and the cookie flags you set on the resulting session.)_

---

## Context Relevancy: JWT session middleware (server-side)

**Project fit:** Node/TypeScript API that validates an HttpOnly JWT cookie on every request and attaches `req.user`. Rejects expired or tampered tokens with 401.

**Value:**

> _(Add your tested middleware here, including the verification key source, clock-skew tolerance, and how `req.user` is shaped.)_
