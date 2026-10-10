# Artifact field reference

Four Markdown artifacts. Adjust paths to your repo, keep the roles distinct.

## 1. Task journal — `docs/journal/NN-slug.md`

One journal per task *type* (not per day, not per chat). Numbered, never
reused for a different task type.

```markdown
# <NN> — <Task name>
STATE  (keep current, three lines)
  1. Current disk/runtime state: <what actually exists on disk / running>
  2. Accepted: <what the human already approved>
  3. Open / not wired: <decided but not implemented>

## Conclusion of this node (≤ half a page)
<Decisions taken, outcome, version/artifacts. Write first so a skimmer stops here.>

## Detail (append-only, newest node at top)
### YYYY-MM-DD — <node title>
- What changed (files, versions)
- Evidence: <how verified — command, screenshot, test>
- Incidents/risks and their resolution
```

Rules:
- Newest node at the top; never rewrite history, append a correction instead.
- Cite evidence for "done" (a command run, a test, an observation) — no
  unverified claims.
- A task journal closes when every backlog item under it is done/cancelled.

## 2. Backlog ledger — `docs/BACKLOG.md`

The ONLY authoritative open-item list.

Sections by state:

```markdown
# Backlog (single source of truth)

## In progress
| ID | Task | Journal | Notes |
|----|------|---------|-------|
| P3 | <task> | #03 | ... |

## Registered (idle, waiting for human "start")
| ID | Task | Notes |
|----|------|-------|

## Blocked / waiting on external
| ID | Task | Waiting on |
|----|------|-----------|

## Done (one line each, no detail)
| ID | Task | Closed where | Date |
|----|------|--------------|------|
| P1 | <task> | journal #02 | 2026-10-01 |
```

- Register → in progress (open journal) → done. Cancelled items get a
  "cancelled — reason" line, kept for traceability.
- Journals must not keep competing task lists; the ledger wins.

## 3. Iron laws — `docs/IRON_LAWS.md`

Short, numbered, enforceable.

```markdown
# Iron Laws

## IL-01 — <short name>
- Rule: <one precise, checkable behavior>
- Why: <the concrete incident that created it, date>
- Check: <how a reviewer/agent verifies compliance>
```

Only admit a rule that prevents a concrete failure and can be checked.
Re-evaluate rules when the underlying system changes; mark superseded laws
instead of deleting them.

## 4. Decision records — `docs/DECISIONS.md`

Record the choice and — more importantly — the reason.

```markdown
## YYYY-MM-DD — <decision title>
- Context: <the choice that had to be made>
- Decision: <what was chosen>
- Why: <reasoning; trade-offs considered>
- Approved by: <human>
- Supersedes: <earlier decision, if any>
```

## Suggested navigation — `README.md` (repo root or docs/)

- Current journal pointer
- Links to BACKLOG / IRON_LAWS / DECISIONS / journals index
- One-paragraph "read these before doing anything"
