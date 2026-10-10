---
name: agent-memory-handoff
description: >-
  Keep a long-lived, multi-session, multi-agent software project continuously
  understandable to ANY AI coding agent (Claude Code, Codex, Cursor, Trae,
  Gemini, etc.) and to humans, without losing state between sessions. Maintains
  four lightweight, human-readable artifacts — task journals, a single
  backlog ledger, a rules (iron laws) file, and human-in-the-loop decision
  records — and produces a hand-off package when switching agents/sessions.
  Use this whenever the user says "handoff", "take over", "new session",
  "onboarding", "context is full", "summarize where we are", "write the
  journal / backlog", "which task next", "another AI needs to continue",
  "交接", "接手", "断点", "挂账", "换个 AI / 换模型继续", "上下文满了",
  "记录进度", or starts/continus serious multi-session work on a project and
  asks how to keep state. Do NOT use for one-off questions or a single chat
  with no continuity need.
---

# Agent Memory Handoff

A minimal, file-based **project memory and hand-off discipline** so that work
survives context resets, model switches, and different AI agents — and so a
human can always see and override what the AI "remembers".

It is four artifacts plus one rule. Nothing is hidden in a vector database or
in the model; everything is Markdown in the repository.

## When to use

- A project spans more than one chat session, or more than one AI tool/model.
- A fresh agent must get productive fast without re-asking everything.
- Several tasks run in parallel and you need one authoritative task list.
- The same class of bug keeps recurring and you want rules that stop it.
- You are about to compact, close the session, switch agents, or hand to a
  teammate.

Do **not** use it for a one-off question, or to log every trivial chat.

## The four artifacts

| Artifact | File (suggested) | One-line role |
|---|---|---|
| **Task journal** | `docs/journal/<NN>-<slug>.md` | One running, stateful log **per type of task** |
| **Backlog ledger** | `docs/BACKLOG.md` | The **single source of truth** for every unfinished item |
| **Iron laws** | `docs/IRON_LAWS.md` | Hard-won, non-negotiable rules distilled from real failures |
| **Decision records** | `docs/DECISIONS.md` (+ inside journals) | What was decided and **why**, with who approved |

Plus the one rule — **Human-in-the-loop**: the AI proposes candidates; the
human decides. AI output is a draft until a human promotes it.

## How to run it

1. **Onboarding / session start**: read `README.md` (navigation) →
   `BACKLOG.md` (what is open) → the *current* task journal. Do not touch
   code before these three are read.
2. **Starting a new task type**: create a new numbered journal; never mix two
   task types in one journal.
3. **During work**: register every task in `BACKLOG.md` first; move it
   `registered → in progress → done`; append to the journal's journal as you
   go. Keep the journal's top "state" block current.
4. **When a failure reveals a rule**: add a short, testable Iron Law with the
   incident that caused it. No vague aphorisms.
5. **AI suggestions** (summaries, refactors, plans, memory edits) are
   *candidates*: label them as such and wait for explicit human approval
   before they become canonical.
6. **Handoff / context full / switching agent**: emit a hand-off package —
   current state, open items, decisions, key files, and a copy-pasteable
   **Next Session Prompt** (see `references/handoff-package.md`).

## Journal shape (state block at the top)

Every task journal opens with a three-line state block, kept current:

```
STATE
  1. Current disk/runtime state (what exists on disk right now)
  2. Accepted (what the human already approved)
  3. Open / not wired (what is decided but not built)
```

Then a **conclusion ≤ half a page** for that task node, then the running
detail. Newest node at the top; older nodes appended below.

## Backlog lifecycle

`registered (idle)` → `in progress (journal opened)` → `done (one line:
id / where / date)`. Cancelled items stay with a "cancelled + reason" line —
never silently deleted. One backlog file is authoritative; journals must not
keep private competing task lists.

## Iron laws criteria

A rule earns "iron law" status only when:

- it prevents a *concrete* recurring failure (cite the incident), and
- it is phrased as an enforceable check, not a value judgment.

Good: "Never write memory when the extractor returned 0 facts (caused the
empty-overwrite incident)."
Bad: "be careful with memory."

## Authority order (human-in-the-loop)

```
human-written config / standing rules
        >  human instruction in this session
             >  AI-generated suggestion (draft only)
```

The AI never silently overrides level 1 or 2. Tag every load-bearing claim as
**observed** (verified this session) vs **assumed** — the next agent must
know the difference.

## Reference files

- `references/artifacts.md` — exact field-level templates for the four artifacts.
- `references/handoff-package.md` — hand-off file layout + Next Session Prompt template.
- `templates/TASK-JOURNAL.md`, `templates/BACKLOG.md`,
  `templates/IRON-LAWS.md`, `templates/HANDOFF.md` — copy to start.

## Relationship to similar skills

Independent practice. It overlaps in spirit with single-session "handoff"
skills (objective/progress/next-prompt snapshot) and with grilling/ADR
workflows (decision logging). Beyond a single snapshot, this discipline adds:

1. **Numbered task journals** for parallel, long-lived work streams;
2. **Iron laws** — enforceable rules distilled from real incidents;
3. **Human-in-the-loop promotion** — AI output stays a draft until approved.

See the repository README for details and install instructions.
