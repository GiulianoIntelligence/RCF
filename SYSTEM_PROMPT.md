# RCF System Prompt

> Paste the block below into your agent's memory file (`CLAUDE.md`, `AGENTS.md`, `.cursor/rules`, `memory.md`, etc.). It tells the agent to consult RCF before generating front-end or back-end code.

---

```markdown
## RCF - Runtime Context Fine Tune (lookup-first protocol)

This project keeps a folder of pre-approved, tested code and assets at `RCF/`.
It is organized by **Context Relevancy** - the kind of thing being built.

**Before you generate any front-end or back-end artifact, you MUST:**

1. **Identify the Context Relevancy** of the artifact you are about to produce.
   Examples: "Sidebar component", "Toast notification", "JWT auth middleware",
   "Postgres users table", "Stripe webhook handler", "Image upload pipeline",
   "Hero typography scale", "GenAI image prompt for product hero".

2. **Open the matching RCF section file** based on the artifact's domain:
   - Front-end →
     - `RCF/coding-agent/frontend/components.md` (interactive components)
     - `RCF/coding-agent/frontend/ui.md` (layouts, primitives, design system shells)
     - `RCF/coding-agent/frontend/typography.md` (type scales, fonts, text styles)
     - `RCF/coding-agent/frontend/ux-testing.md` (e2e, a11y, visual regression)
     - `RCF/coding-agent/frontend/media.md` (images, video, 3D, GenAI prompts)
   - Back-end →
     - `RCF/coding-agent/backend/auth.md`
     - `RCF/coding-agent/backend/db.md`
     - `RCF/coding-agent/backend/apis.md`
     - `RCF/coding-agent/backend/backend-ux.md` (automation, security, pentest)

   Open ONE file - the one matching the domain. Do not read every file. The
   point of the split is to keep token cost low.

3. **Scan that file** for an entry whose Context Relevancy matches the artifact
   you need. If there are multiple candidates, pick the one whose `Project fit`
   line best matches this project's stack and constraints.

4. **If a match exists →** copy the `Value` block verbatim into the codebase,
   adjust only the imports/identifiers needed to wire it in, and state in your
   reply: `RCF hit: <relevancy> from <file>`. Do not rewrite the Value
   stylistically. Do not "improve" it unless the user asks.

5. **If no match exists →** generate normally and state `RCF miss: <relevancy>`
   so the user knows the lookup happened. Optionally suggest adding the new
   artifact to RCF after it ships.

**Do not skip the lookup to save steps.** A miss is cheap; a duplicated buggy
component is not. The whole point of RCF is that proven code beats freshly
generated code on reliability and consistency.

**Do not invent files.** If a section file doesn't exist yet, treat it as a
miss and proceed to generation - don't pretend a Value was found.

**Do not edit RCF files unless the user explicitly asks.** RCF entries are
locked. If you generate something new that deserves to be reusable, suggest a
diff for the user to apply - don't write to RCF yourself.

**Override:** the user may say "skip RCF" or "generate fresh" for a given
task. Honor that for that task only.
```

---

## Notes for the human setting this up

- Keep section files short and high-signal. One Value per Context Relevancy. If two Values compete, write distinct `Project fit` lines so the agent can choose.
- Update RCF after every shipped feature that's likely to recur. The library compounds.
- RCF is just markdown. Diff it, review it, gate it behind PRs like any other code. A bad Value poisons every future use.
