# agent-memory-handoff

> Keep a long-lived, multi-session, **multi-agent** software project
> continuously understandable to *any* AI coding agent — and to humans —
> without losing state between sessions, context compactions, or model
> switches.
>
> 让任何一个 AI 编程助手（Claude Code / Codex / Cursor / Trae / Gemini…）
> 都能跨会话、跨模型无缝接手一个长期项目；也让人类随时看得见、能否决
> AI「记住」的东西。全部是仓库里的 Markdown 文件，不依赖向量库或任何服务。

一个 `SKILL.md`＋四个轻量产物＋一条铁律：**AI 只提候选，人拍板才生效**。

---

## 为什么需要它

AI 写代码最大的问题不是单次能力，而是**状态不连续**：上下文一满、一会话结束、
一换模型/换工具，新的 AI 就要重新问一遍——项目当前到哪了？哪些决定拍过板？
同一个坑为什么又踩了？本技能用仓库内人可读的文件解决这件事，并刻意保持
**人类可查看、可编辑、可裁决**。

## 四个产物 + 一条规则

| 产物 | 文件（建议） | 职责 |
|---|---|---|
| **任务卷 Task journal** | `docs/journal/NN-slug.md` | 一类任务一卷，断点三行，长期状态化 |
| **挂账 Backlog** | `docs/BACKLOG.md` | 所有未完成任务的**唯一清单**，带状态流转 |
| **铁律 Iron laws** | `docs/IRON_LAWS.md` | 从真实事故沉淀的、可检查的硬规则 |
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
    ├── TASK-JOURNAL.md           # 复制即用（中英）
    ├── BACKLOG.md
    ├── IRON-LAWS.md
    └── HANDOFF.md
```

## 安装

本技能遵循开放的 **Agent Skills** 约定（一个目录 + 一个 `SKILL.md`），
Claude Code、Codex、Cursor、Trae、Windsurf 等支持该约定的工具通用。

**方式一：复制目录**
把本目录复制/软链到对应工具的 skills 目录，例如：
- Claude Code：`~/.claude/skills/agent-memory-handoff/`
- Trae：`~/.trae-cn/skills/agent-memory-handoff/`（Windows: `%USERPROFILE%\.trae-cn\skills\`）
- 其余工具见其文档的 custom skills 路径。

**方式二：在项目里用模板**
不安装技能也能用——把 `templates/` 里的四个文件复制到项目 `docs/`，
按 `references/artifacts.md` 维护即可。

## 怎么用（30 秒版）

1. 新会话开工前读：导航 README → `BACKLOG.md` → 当前任务卷，读完再动代码；
2. 新类型任务开新卷（编号），所有任务先登记进 Backlog；
3. 状态随做随流转：registered → in progress → done；
4. 踩了真实的坑 → 沉淀一条可检查的铁律；
5. AI 的总结/重构/计划/记忆修改一律标成候选，等人批准；
6. 上下文快满 / 换 AI / 收工 → 生成交接包。

## 与同类技能的关系（诚实声明）

这是作者在一个长期项目中独立摸索、用真实故障反复打磨形成的实践。它与社区
两类流行工作法在精神上趋同，并非要取代它们：

- **单会话交接类技能**（如 `handoff`：objective/progress/next-prompt
  快照）；
- **盘问与决策记录类工作法**（如 grilling / ADR / GLOSSARY）。

在「单次会话快照」之外，本技能额外提供三样东西：

1. **编号任务卷制（Numbered task journals）**：并行、长期、跨多会话的
   多任务流管理，而不只是一次会话的压缩；
2. **铁律体系（Iron laws）**：每条规则由真实事故催生、带准入条件与
   可执行检查，防止同类错误复发，而不是零散的「注意事项」；
3. **人机裁决晋升（Human-in-the-loop promotion）**：AI 产出在人类
   显式批准前始终是草稿，配权威顺序（人写的规则 ＞ 当场指令 ＞ AI 建议），
   解决「AI 自作主张改写记忆/决定」的问题。

如果只需要「这一会话结束给下个会话留个快照」，用更轻的单文件交接技能
即可；本技能面向的是**持续数周数月、多个 AI/人交替参与的严肃项目**。

## 设计原则

- 文件即事实源：一切在 Markdown 里，可 diff、可备份、可被任何工具读取；
- 人类主权：记忆归项目所有者，可见、可改、可删除；
- 证据导向：结论标 observed / assumed，「完成」要有可复现的验证；
- 追加而非覆写：历史不抹除，纠偏用新记录，断案可追溯；
- 与工具无关：交接包是纯文本，可原样粘贴进另一家厂商的 AI。

## License

MIT © Jovoess
