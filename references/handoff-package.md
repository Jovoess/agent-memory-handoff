# Hand-off package

Used at: context window filling up, ending a session, switching AI
tool/model, or handing to a teammate.

Produce **two** artifacts: a dated hand-off file (source of truth) and a
short pointer so the next session auto-discovers it.

## File layout — `docs/handoffs/YYYY-MM-DD-slug.md`

Required headings in this order. Objective / Progress / Important files /
Next-session prompt are never skipped. Blocked / Decisions / Open issues are
omitted only when genuinely empty.

```markdown
# Handoff: <topic> — YYYY-MM-DD

## Objective
<1–3 sentences: what is being built/fixed/investigated and why.>

## Progress
**Completed:**
- <done item>
**In progress:**
- <mid-flight item> — verified: <how observed> / assumed: <blast radius if wrong>
**Blocked:**
- <blocker> — <on whom/what>

## Decisions
- <decision> — <why; the reasoning matters more than the choice>

## Important files
- `<path>` — <one line: what changed / why it matters>

## Open issues
- <unresolved item> — observed|assumed: <evidence or risk>

## Next-session prompt
> Copy-paste into the new chat.

Read `docs/handoffs/<this-file>.md` first.

**Goal:** <one-sentence resume goal>
**Start by reviewing:**
1. `<path>`
2. `<path>`
**Then:**
- <next concrete step>
- <verification command, e.g. `npm test`>
```

## Quality bar for the Next-session prompt

- ❌ "Continue working on auth, finish the rest." — a fresh agent cannot act.
- ✅ Name the file, the failing test, the exact next edit, and the command
  that proves it worked. A brand-new agent with zero prior context must be
  able to start immediately.

## Tag every claim

`observed` (verified this session — ran it, read it, saw it) vs `assumed`
(inferred, not yet checked). Cross-check with `git status` /
`git diff --stat`; do not trust memory alone for "what changed".

## Pointer for auto-discovery

Add a one-line pointer to your project memory/index file (e.g.
`README.md` navigation or an agent memory file) so a new session finds the
latest hand-off:

```markdown
- Active hand-off for <topic>: docs/handoffs/2026-10-10-slug.md
```

## Multi-agent note

The hand-off file is plain Markdown and tool-neutral — paste the
Next-session prompt into a different vendor's agent (Claude Code, Codex,
Cursor, Trae, Gemini…) unchanged. Secrets/keys are never written into it.
