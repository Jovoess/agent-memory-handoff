# agent-memory-handoff

**English** · [简体中文](#简体中文) · [한국어](#한국어) · [日本語](#日本語)

> Keep a long-lived, multi-session, **multi-agent** software project
> continuously understandable to *any* AI coding agent — and to humans —
> without losing state between sessions, context compactions, or model
> switches.

One `SKILL.md` + four lightweight artifacts + one rule: **the AI proposes,
the human decides.**

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

<a id="简体中文"></a>
# agent-memory-handoff

[English](#) · **简体中文** · [한국어](#한국어) · [日本語](#日本語)

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

---
---

<a id="한국어"></a>
# agent-memory-handoff

[English](#) · [简体中文](#简体中文) · **한국어** · [日本語](#日本語)

> 장기간에 걸친 **멀티 세션·멀티 에이전트** 소프트웨어 프로젝트를 어떤 AI
> 코딩 에이전트(Claude Code, Codex, Cursor, Trae, Gemini 등)와 사람이
> 세션 종료, 컨텍스트 압축, 모델 전환 후에도 상태를 잃지 않고 계속 이해할 수
> 있도록 합니다.

`SKILL.md` 하나 + 가벼운 산출물 네 개 + 규칙 하나: **AI는 제안만 하고,
결정은 사람이 합니다.**

## 왜 필요한가요

AI 코딩의 가장 큰 약점은 한 번의 성능이 아니라 **상태 불연속**입니다.
컨텍스트가 가득 차거나 세션이 끝나고 모델/도구를 바꾸면, 새 에이전트는
프로젝트 위치, 이미 내려진 결정, 같은 버그가 재발한 이유를 처음부터 다시
물어야 합니다.

이 스킬은 벡터 데이터베이스나 외부 서비스 없이, **저장소 내부의 사람이 읽을 수
있는 Markdown**으로 이 문제를 해결합니다. 기억은 항상 사람에게 보이고,
편집 가능하며, 거부할 수 있습니다.

## 네 가지 산출물 + 한 가지 규칙

| 산출물 | 파일(권장) | 역할 |
|---|---|---|
| **작업 저널** | `docs/journal/NN-slug.md` | 작업 *유형*당 하나의 상태 로그, 3줄 상태 블록 |
| **백로그** | `docs/BACKLOG.md` | 모든 미완료 항목의 **단일 진실 원천** |
| **철칙** | `docs/IRON_LAWS.md` | 실제 실패에서 추출한 강제 가능한 규칙 |
| **의사결정 기록** | `docs/DECISIONS.md` | 무엇을 결정했는지, 그리고 **왜** |
| **휴먼-인-더-루프**(규칙) | — | 사람이 명시적으로 승인하기 전 AI 결과물은 초안 |

인수인계 시 **핸드오프 패키지**(상태, 미결 항목, 결정, 핵심 파일, 바로 붙여넣는
Next Session Prompt — `references/handoff-package.md` 참고)를 생성합니다.

## 구성

```
agent-memory-handoff/
├── SKILL.md
├── README.md
├── LICENSE (MIT)
├── references/
│   ├── artifacts.md
│   └── handoff-package.md
└── templates/
    ├── TASK-JOURNAL.md
    ├── BACKLOG.md
    ├── IRON-LAWS.md
    └── HANDOFF.md
```

## 설치

개방형 **Agent Skills** 규약(디렉터리 + `SKILL.md`)을 따르므로 Claude Code,
Codex, Cursor, Trae, Windsurf 등 호환 도구에서 동일하게 동작합니다.

**옵션 1 — 디렉터리 복사**:
- Claude Code: `~/.claude/skills/agent-memory-handoff/`
- Trae: `~/.trae-cn/skills/agent-memory-handoff/`

**옵션 2 — 템플릿만 사용**: 설치 없이 `templates/` 파일을 프로젝트 `docs/`에
복사하고 `references/artifacts.md`를 따릅니다.

## 30초 사용법

1. 새 세션에서 코드 수정 전 README → `BACKLOG.md` → 현재 작업 저널 순으로 읽기;
2. 새 작업 유형은 번호가 매겨진 새 저널을 열고 모든 작업을 먼저 백로그에 등록;
3. 상태 이동: registered → in progress → done;
4. 실제 실패가 규칙을 알려주면 강제 가능한 철칙으로 추가;
5. AI 요약/리팩터링/계획/기억 수정은 모두 후보 — 사람 승인 후 반영;
6. 컨텍스트 부족 / AI 교체 / 마무리 시 핸드오프 패키지 생성.

## 유사 스킬과의 관계(솔직한 안내)

장기 프로젝트의 실제 사고로 다듬은 독립적 실천이며, 다음 널리 알려진
워크플로와 방향이 유사하지만 대체하려는 것은 아닙니다:

- **단일 세션 핸드오프 스킬**(예: `handoff`);
- **그릴링/의사결정 기록 워크플로**(grilling / ADR / GLOSSARY).

단일 스냅샷 너머의 세 가지 추가분:

1. **번호가 매겨진 작업 저널** — 병렬·장기·멀티 세션 작업 흐름;
2. **철칙 시스템** — 구체적 사고에서 태어난, 준수 기준과 실행 가능한 점검이 있는 규칙;
3. **휴먼-인-더-루프 승급** — 명시적 승인 전 AI 결과물은 초안이며,
   권한 순서(사람의 상시 규칙 > 현 세션 지시 > AI 제안)를 따름.

수 주~수 개월, 여러 AI와 사람이 번갈아 참여하는 진지한 프로젝트를
대상으로 합니다.

## 설계 원칙

- **파일이 진실 원천** — 모든 것이 Markdown, diff/백업/어떤 도구로도 읽기 가능;
- **사람 소유** — 기억은 프로젝트 소유자의 것: 보이고, 고치고, 삭제 가능;
- **증거 기반** — observed/assumed 표시, “완료”에는 재현 가능한 점검 필요;
- **덮어쓰지 않고 추가** — 이력 보존, 정정은 새 기록으로 추적 가능;
- **도구 비종속** — 핸드오프 패키지는 순수 텍스트, 다른 벤더 AI에 그대로 붙여넣기.

## 라이선스

MIT © Jovoess

---
---

<a id="日本語"></a>
# agent-memory-handoff

[English](#) · [简体中文](#简体中文) · [한국어](#한국어) · **日本語**

> 長期にわたる**マルチセッション・マルチエージェント**のソフトウェア
> プロジェクトを、どの AI コーディングエージェント（Claude Code /
> Codex / Cursor / Trae / Gemini など）と人間が、セッション終了・コンテキスト
> 圧縮・モデル切替の前後で状態を失わずに理解し続けられるようにします。

`SKILL.md` 1 つ＋軽量な成果物 4 つ＋ルール 1 つ：**AI は提案するだけ、
決めるのは人間です。**

## なぜ必要か

AI コーディングの最大の弱点は、一度きりの能力ではなく**状態の途絶**です。
コンテキストが満杯になる、セッションが終わる、モデルやツールを替える——
そのたび新しいエージェントは、プロジェクトの位置、決定済み事項、同じ
バグが再発した理由をゼロから聞き直します。

本スキルは、ベクタ DB や外部サービスに頼らず、**リポジトリ内の人間が
読める Markdown** でこれを解決します。記憶は常に可視・編集可能で、
人間が拒否することもできます。

## 4 つの成果物＋1 つのルール

| 成果物 | ファイル（推奨） | 役割 |
|---|---|---|
| **タスクジャーナル** | `docs/journal/NN-slug.md` | タスク*種別*ごとに 1 冊、3 行状態ブロック付き |
| **バックログ台帳** | `docs/BACKLOG.md` | 未完了項目すべての**唯一の事実源** |
| **鉄則** | `docs/IRON_LAWS.md` | 実際の失敗から抽出した強制可能なルール |
| **意思決定記録** | `docs/DECISIONS.md` | 何を決めたか、そして**なぜ** |
| **ヒューマン・イン・ザ・ループ**（ルール） | — | 人間が明示承認するまで AI 出力は下書き |

引き継ぎ時には**ハンドオフパッケージ**（状態・未解決事項・決定・重要
ファイル・貼り付け可能な Next Session Prompt。`references/handoff-package.md`
参照）を生成します。

## 構成

```
agent-memory-handoff/
├── SKILL.md
├── README.md
├── LICENSE (MIT)
├── references/
│   ├── artifacts.md
│   └── handoff-package.md
└── templates/
    ├── TASK-JOURNAL.md
    ├── BACKLOG.md
    ├── IRON-LAWS.md
    └── HANDOFF.md
```

## インストール

オープンな **Agent Skills** 規約（1 ディレクトリ＋`SKILL.md`）に従い、
Claude Code / Codex / Cursor / Trae / Windsurf など対応ツールで共通利用
できます。

**方法1 — ディレクトリをコピー**:
- Claude Code: `~/.claude/skills/agent-memory-handoff/`
- Trae: `~/.trae-cn/skills/agent-memory-handoff/`

**方法2 — テンプレートだけ使う**: インストール不要で `templates/` を
プロジェクトの `docs/` にコピーし、`references/artifacts.md` に従う。

## 30 秒の使い方

1. 新セッションでコードを触る前に README → `BACKLOG.md` → 現在の
   ジャーナルを読む；
2. 新しいタスク種別には採番ジャーナルを開き、まずバックログに登録；
3. 状態遷移: registered → in progress → done；
4. 実失敗がルールを教えたら、強制可能な鉄則として追加；
5. AI の要約/リファクタリング/計画/記憶編集はすべて候補——人間承認後に反映；
6. コンテキスト逼迫 / AI 切替 / 終了時にハンドオフパッケージを生成。

## 類似スキルとの関係（率直な注記）

長期プロジェクトでの実際のインシデントから独立に磨いた実践であり、
普及した次のワークフローと趣旨は重なるが、置き換えを意図したものでは
ありません:

- **単一セッション引き継ぎスキル**（例: `handoff`）；
- **グリリング/意思決定記録ワークフロー**（grilling / ADR / GLOSSARY）。

単発スナップショットを超える 3 つの追加要素:

1. **採番タスクジャーナル** — 並列・長期・マルチセッションの作業の流れ；
2. **鉄則システム** — 具体的インシデント由来で、採用基準と実行可能な
   チェックを持つルール；
3. **ヒューマン・イン・ザ・ループ昇格** — 明示承認まで AI 出力は下書き。
   権限順位（人間の定常ルール ＞ その場の指示 ＞ AI 提案）に従う。

数週間〜数か月、複数の AI と人間が交代する本格プロジェクト向けです。

## 設計原則

- **ファイルが事実源** — すべて Markdown。差分・バックアップ・任意
  ツールで読取り可能；
- **人間の所有権** — 記憶はプロジェクト所有者のもの: 可視・編集・削除可能；
- **証拠駆動** — observed/assumed を明示、「完了」に再現可能な検証を要求；
- **上書きせず追記** — 履歴を保持し、訂正は新規記録で追跡可能；
- **ツール非依存** — ハンドオフ資料はプレーンテキスト、他社 AI に
  そのまま貼り付け可能。

## ライセンス

MIT © Jovoess
