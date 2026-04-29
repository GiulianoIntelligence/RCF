# RCF - Front-end / UX Testing

> End-to-end flows, accessibility audits, visual-regression suites. Consult this file before writing any new UX-level test from scratch.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Critical-path e2e (signup → first action)

**Project fit:** Any app where the signup flow is revenue-critical. Covers email entry, verification, onboarding, and the user's first meaningful action - fails the build if any step regresses.

**Value:**

> _(Add your tested Playwright/Cypress spec here. Include selectors, test data setup, and teardown.)_

---

## Context Relevancy: Accessibility audit on form components

**Project fit:** Apps with WCAG-AA obligations. Checks label association, focus visibility, error-message announcements, and keyboard-only completion of every form.

**Value:**

> _(Add your tested axe-core / pa11y / Playwright a11y harness here, plus the list of forms it iterates over.)_
