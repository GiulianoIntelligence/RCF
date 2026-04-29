# RCF - Runtime Context Fine Tune

> A novel database pattern for retrieval-grounded AI. **V0** is a concept release: structure, prompt, and example files. No UI, no runtime, no fork required - copy what you need.

RCF is a folder of markdown files that an AI agent reads **before it generates output**. Each entry pairs a **Context Relevancy** (what kind of thing the agent is about to make) with a **Value** (a known-good, tested artifact for that thing). If the agent finds a match, it copies the Value verbatim instead of generating. If it doesn't, it generates as normal.

That's the whole idea.

---

## Why this exists

In 2023 I built RCF V0 for the **Airbnb Guest Interactions Chatbot**. The chatbot was hallucinating answers about pool depth, Wi-Fi passwords, fire-emergency procedures, check-out times - anything where being *almost right* is worse than admitting "I don't know."

I stopped trying to fine-tune the model. I wrote the answers down as markdown, keyed by the kind of question being asked, and told the model to **look up first, generate second**. Hallucinations on covered topics dropped by **over 90%**.

See [`examples/airbnb-2023/`](./examples/airbnb-2023/) for the original files, reformatted in RCF's `Context Relevancy → Value` shape.

## Why this matters for coding agents

Coding agents have the same problem in a different costume. Ask an agent for a sidebar and it will reinvent one - sometimes well, often with subtle bugs, never the same way twice. You already have a sidebar that works. You shouldn't be paying tokens to re-derive it.

**RCF for coding agents** flips the default:

1. Agent decides it needs to build *X* (a sidebar, an auth flow, a rate limiter).
2. Agent opens the relevant RCF section file based on domain (frontend/components, backend/auth, etc.).
3. If a Context Relevancy matches the project, agent **copies the Value** into the codebase.
4. If nothing matches, agent generates from scratch - same as today.

Less generation. Fewer bugs. Tested code reused. The agent becomes a *librarian first, author second.*

---

## How to set it up

### 1. Drop this folder into your project

```
your-project/
├── RCF/
│   ├── coding-agent/
│   │   ├── frontend/
│   │   │   ├── components.md
│   │   │   ├── ui.md
│   │   │   ├── typography.md
│   │   │   ├── ux-testing.md
│   │   │   └── media.md
│   │   └── backend/
│   │       ├── auth.md
│   │       ├── db.md
│   │       ├── apis.md
│   │       └── backend-ux.md
│   └── SYSTEM_PROMPT.md
└── CLAUDE.md   (or AGENTS.md, .cursor/rules, memory.md, etc.)
```

The frontend/backend split matters: it lets the agent open *one section file* - not the whole library - when it knows what kind of thing it needs. Less context wasted, faster lookups.

### 2. Paste the system prompt into your agent's memory file

Open [`SYSTEM_PROMPT.md`](./SYSTEM_PROMPT.md) and paste its contents into whatever memory file your agent reads on startup:

- **Claude Code** → `CLAUDE.md`
- **Cursor** → `.cursor/rules`
- **Codex / OpenAI Agents SDK** → `AGENTS.md`
- **Aider** → `.aider.conf.yml` `read:` entry pointing at the prompt
- **Continue / Cline / Roo / etc.** → their respective memory file

### 3. Fill in your own Values

Most files in `coding-agent/` ship with **placeholder Values** (`_(Add your tested X here)_`). That's intentional - RCF is your library, not mine. Replace the placeholders with code you have actually shipped and trust.

A few entries ship with **real, populated Values** so you can see what a finished entry looks like and use them as test fixtures:

- `coding-agent/frontend/ui.md` → shadcn `Sidebar` layout
- `coding-agent/frontend/components.md` → primary button, destructive button with confirm dialog, sonner toast wrapper, Next.js error boundary, react-hook-form + zod form

### 4. That's it

The agent will check RCF on every front-end or back-end task before generating. If your library grows, retrieval gets better.

---

## File format

Every entry in every section file uses the same shape:

```markdown
## Context Relevancy: <what kind of thing this is>

**Project fit:** <one line on when to use this Value vs. another>

**Value:**

​```<lang>
<the code, prompt, schema, or asset the agent should copy>
​```
```

A single section file can hold many Context Relevancy entries. The agent picks the one whose **Project fit** best matches the current project's stack and constraints. If none fit, it falls back to generation.

---

## Repository layout

```
.
├── README.md                       - this file
├── LICENSE                         - MIT
├── SYSTEM_PROMPT.md                - paste into your agent's memory file
├── examples/
│   └── airbnb-2023/                - the original V0 use case, in Context Relevancy format
│       ├── pool.md
│       ├── wifi.md
│       ├── fire-safety.md
│       ├── check-out.md
│       ├── medical.md
│       ├── security.md
│       ├── rules-and-fees.md
│       └── travel-stay-info.md
└── coding-agent/                   - the new use case
    ├── frontend/
    │   ├── components.md           - populated: button, toast, form, error boundary, destructive button
    │   ├── ui.md                   - populated: shadcn sidebar layout
    │   ├── typography.md           - placeholders
    │   ├── ux-testing.md           - placeholders
    │   └── media.md                - placeholders
    └── backend/
        ├── auth.md                 - placeholders
        ├── db.md                   - placeholders
        ├── apis.md                 - placeholders
        └── backend-ux.md           - placeholders
```

---

## What V0 is *not*

- Not a server, daemon, vector DB, or runtime.
- Not a package - there is nothing to install.
- Not a framework - your agent does the lookup, RCF is just the data.
- Not opinionated about file count, depth, or naming inside each section. Use what works.

V1 will add a retrieval layer (embeddings, scoring, conflict resolution between competing Values). V0 is intentionally just files and a prompt, because that's all the Airbnb version was, and that's what made it work.

---

## License

[MIT](./LICENSE). Fork if you want, but most people will just copy. That's fine.

## Author

**Giuliano Szarkezi**
- X: [@AICEOGiuliano](https://x.com/AICEOGiuliano)
- LinkedIn: [giuliano-szarkezi](https://www.linkedin.com/in/giuliano-szarkezi-a7046a290/)
