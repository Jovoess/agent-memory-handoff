# agent-memory-handoff

> Keep a long-lived, multi-session, **multi-agent** software project
> continuously understandable to *any* AI coding agent — and to humans —
> without losing state between sessions, context compactions, or model
> switches.

One `SKILL.md` + four lightweight artifacts + one rule: **the AI proposes,
the human decides.**

English below · 中文版见后半部分（[跳到中文](#中文)）。

---

## Why

The biggest weakness of AI coding is not one-shot capability — it is **loss
of state**. When the context fills up, a session ends, or you switch
models/tools, the new agent starts from zero: where is the project, what was
already decided, why did the same bug come back?

This skill answers that with plain, human-readable Markdown **inside the
repo** — no vector database, no service, nothing hidden from the person in
charge. Memory stays visible, editable, and vetoable.

## The four artifacts + one rule

| Artifact | File (suggested) | Role |
|---|---|---|
| **Task journal** | `docs/journal/NN-slug.md` | One stateful log per task *type*, with a 3-line state block |
| **Backlog ledger** | `docs/BACKLOG.md` | The **single source of truth** for every unfinished item |
| **Iron laws** | `docs/IRON_LAWS.md` | Enforceable rules distilled from real failures |
| **Decision records** | `docs/DECISIONS.md` | What was decided — and **why** |
| **Human-in-the-loop** (rule) | — | AI output is a draft until a human explicitly approves it |

At a hand-off you also emit a **hand-off package** (state, open items,
decisions, key files, and a copy-pasteable *Next Session Prompt* — see
`references/handoff-package.md`).

## Layout

```
agent-memory-handoff/
├── SKILL.md                      # Skill body (open Agent Skills format)
├── README.md
├── LICENSE (MIT)
├── references/
│   ├── artifacts.md              # Field-level templates for the 4 artifacts
│   └── handoff-package.md        # Hand-off layout + Next Session Prompt
└── templates/
    ├── TASK-JOURNAL.md           # Copy-ready (bilingual)
    ├── BACKLOG.md
    ├── IRON-LAWS.md
    └── HANDOFF.md
```

## Install

Follows the open **Agent Skills** convention (one directory + one
`SKILL.md`), so the same skill works in Claude Code, Codex, Cursor, Trae,
Windsurf, and other compatible tools.

**Option 1 — copy the directory** into your tool's skills folder, e.g.:
- Claude Code: `~/.claude/skills/agent-memory-handoff/`
- Trae: `~/.trae-cn/skills/agent-memory-handoff/` (Windows: `%USERPROFILE%\.trae-cn\skills\`)
- Other tools: see their custom-skills path docs.

**Option 2 — just use the templates** without installing anything: copy the
files in `templates/` into your project's `docs/` and follow
`references/artifacts.md`.

## Usage in 30 seconds

1. Before coding in a new session, read: nav README → `BACKLOG.md` → the
   current task journal. Don't touch code before these three.
2. Open a new numbered journal for a new task *type*; register every task in
   the backlog first.
3. Move state as you work: registered → in progress → done.
4. When a real failure teaches a rule, add an enforceable iron law.
5. AI summaries/refactors/plans/memory edits are candidates — wait for
   human approval.
6. Context nearly full / switching AI / wrapping up → emit a hand-off package.

## Relationship to similar skills (honest note)

This is an independent practice, shaped by real incidents in a long-running
project. It overlaps in spirit with two popular workflows and is not meant to
replace them:

- **single-session hand-off skills** (e.g. `handoff`: objective / progress /
  next-prompt snapshot);
- **grilling & decision-record workflows** (e.g. grilling / ADR / GLOSSARY).

Beyond a single snapshot, this discipline adds three things:

1. **Numbered task journals** — parallel, long-lived, multi-session work
   streams, not just a compression of one chat;
2. **Iron laws** — each rule is born from a concrete incident, has an
   admission criterion and an executable check, so the same failure cannot
   quietly recur;
3. **Human-in-the-loop promotion** — AI output stays a draft until explicitly
   approved, with an authority order (human standing rules > in-session
   instruction > AI suggestion) that stops the model silently rewriting
   memory or making decisions.

If you only need an end-of-chat snapshot for the next session, a lighter
single-file hand-off skill is enough. This skill is for **serious projects
that run weeks or months with multiple AIs and people taking turns.**

## Design principles

- **File as source of truth** — everything is Markdown: diffable, backupable,
  readable by any tool;
- **human ownership** — memory belongs to the project owner: visible,
  editable, deletable;
- **evidence-driven** — tag claims observed vs assumed; "done" needs a
  reproducible check;
- **append, don't overwrite** — history is preserved; corrections are new
  records, so anything is traceable;
- **tool-neutral** — the hand-off package is plain text; paste it unchanged
  into another vendor's AI.

## License

MIT © Jovoess

---
---

<a id="中文"></a>
# agent-memory-handoff（中文）

> 让任何一个 AI 编程助手（Claude Code / Codex / Cursor / Trae /
> Gemini…）跨会话、跨模型地持续理解一个长期、多会话、**多 AI 协作**的
> 软件项目——也让人类随时看得见、能否决 AI「记住」的东西。

一个 `SKILL.md` ＋四个轻量产物＋一条铁律：**AI 只提候选，人拍板才生效**。

## 为什么需要它

AI 写代码最大的问题不是单次能力，而是**状态不连续**：上下文一满、一会话
结束、一换模型或工具，新 AI 就要重新问一遍——项目到哪了？哪些决定拍过板？
同一个坑为什么又踩了？

本技能用仓库内人可读的 Markdown 解决这件事，不依赖向量库或任何服务，并刻意
保持**人类可查看、可编辑、可裁决**。

## 四个产物 + 一条规则

| 产物 | 文件（建议） | 职责 |
|---|---|---|
| **任务卷 Task journal** | `docs/journal/NN-slug.md` | 一类任务一卷，断点三行，长期状态化 |
| **挂账 Backlog** | `docs/BACKLOG.md` | 所有未完成任务的**唯一清单**，带状态流转 |
| **铁律 Iron laws** | `docs/IRON_LAWS.md` | 从真实事故沉淀、可检查的硬规则 |
| **决策记录 Decisions** | `docs/DECISIONS.md` | 决定了什么，**以及为什么** |
| **人机裁决**（规则） | — | AI 产出是草稿，人类显式批准后才升级为正式内容 |

交接时再产出一个**交接包**（当前状态/未决/决策/关键文件/可直接粘贴的
Next-session prompt，见 `references/handoff-package.md`）。

## 目录结构

```
agent-memory-handoff/
├── SKILL.md                      # 技能主体（Agent Skills 通用规范）
├── README.md
├── LICENSE (MIT)
├── references/
│   ├── artifacts.md              # 四个产物的字段级模板与规则
│   └── handoff-package.md        # 交接包结构与 Next-session prompt
└── templates/
    ├── TASK-JOURNAL.md           # 复制即用（中英双语）
    ├── BACKLOG.md
    ├── IRON-LAWS.md
    └── HANDOFF.md
```

## 安装

遵循开放的 **Agent Skills** 约定（一个目录 + 一个 `SKILL.md`），Claude
Code、Codex、Cursor、Trae、Windsurf 等支持该约定的工具通用。

**方式一：复制目录**到对应工具的 skills 目录，例如：
- Claude Code：`~/.claude/skills/agent-memory-handoff/`
- Trae：`~/.trae-cn/skills/agent-memory-handoff/`（Windows：`%USERPROFILE%\.trae-cn\skills\`）
- 其余工具见其 custom skills 路径文档。

**方式二：不装技能，只用模板**——把 `templates/` 里的文件复制到项目
`docs/`，按 `references/artifacts.md` 维护即可。

## 怎么用（30 秒版）

1. 新会话开工前读：导航 README → `BACKLOG.md` → 当前任务卷，读完再动代码；
2. 新类型任务开新卷（编号），所有任务先登记进 Backlog；
3. 状态随做随流转：registered → in progress → done；
4. 踩了真实的坑 → 沉淀一条可检查的铁律；
5. AI 的总结/重构/计划/记忆修改一律标成候选，等人批准；
6. 上下文快满 / 换 AI / 收工 → 生成交接包。

## 与同类技能的关系（诚实声明）

这是作者在一个长期项目中独立摸索、用真实故障反复打磨形成的实践，与社区两类
流行工作法精神趋同，并非要取代它们：

- **单会话交接类技能**（如 `handoff`：objective/progress/next-prompt 快照）；
- **盘问与决策记录类工作法**（如 grilling / ADR / GLOSSARY）。

在「单次会话快照」之外，本技能额外提供三样东西：

1. **编号任务卷制**：并行、长期、跨多会话的多任务流管理，而不只是一次会话
   的压缩；
2. **铁律体系**：每条规则由真实事故催生、带准入条件与可执行检查，防止同类
   错误复发，而非零散的「注意事项」；
3. **人机裁决晋升**：AI 产出在人类显式批准前始终是草稿，配权威顺序
   （人写的规则 ＞ 当场指令 ＞ AI 建议），防止模型自作主张改写记忆或决定。

若只需「这一会话结束给下个会话留个快照」，用更轻的单文件交接技能即可；本技能
面向**持续数周数月、多个 AI/人交替参与的严肃项目**。

## 设计原则

- **文件即事实源**：一切在 Markdown 里，可 diff、可备份、可被任何工具读取；
- **人类主权**：记忆归项目所有者，可见、可改、可删除；
- **证据导向**：结论标 observed / assumed，「完成」要有可复现的验证；
- **追加而非覆写**：历史不抹除，纠偏用新记录，断案可追溯；
- **与工具无关**：交接包是纯文本，可原样粘贴进另一家厂商的 AI。

## 许可证

MIT © Jovoess
