---
name: agent-context-skill
description: 创建和维护通用上下文系统（agent context system），以 AGENTS.md 和交接文档（handoff）管理跨会话项目上下文。适用于任意仓库（repository）、工作区（workspace）或项目（project）中初始化 agent-context/、编写或审查 AGENTS.md、更新 handoff、从 handoff 开启新会话、清理上下文膨胀（context bloat）或上下文漂移（context drift），不绑定行业、业务类型、文档类型或技术栈。
---

# Agent Context Skill

这个 skill 用于建立一套可复用的轻量上下文系统（agent context system），帮助代理 / AI 代理（agent）在不同会话（session）、任务和长期维护过程中保持必要上下文。

这个 skill 只属于方法和模板层。不要在这里存放任何具体项目事实、任务进度、项目源资料正文、实现细节或会话状态。

具体项目事实应留在目标项目自己的 `agent-context/`、项目源资料（source material）或其他项目文件中。这个 skill 只保存工作流、模板（template）、提示词（prompt）、通用规则和检查标准。

## 这个 Skill 做什么

使用这个 skill，帮助任意仓库（repository）、工作区（workspace）或项目（project）维护：

- `agent-context/AGENTS.md`：长期稳定的项目导航和 agent 协作规则。
- `agent-context/handoff/`：短小的会话或任务交接文档（handoff）。
- 项目源资料引用：只记录路径和用途，不复制正文或完整内容。

项目源资料是指项目中任何提供事实、约束、上下文或参考价值的输入材料。它可以是文档、代码、图片、表格、配置文件、参考资料、会议记录、设计稿、数据文件、日志、README、外部资料说明，或其他项目文件和输入材料。不要假设项目一定存在其中某一种。

## 快速使用

- 新项目初始化：使用 `prompts/install-agent-context.md`，扫描项目并创建轻量 `agent-context/`。
- 当前会话快满 / 任务中断：使用 `prompts/update-handoff.md`，创建或更新当前任务的 handoff。
- 新会话接续：使用 `prompts/start-from-handoff.md`，从 `AGENTS.md` 和指定 handoff 继续工作。
- 定期审查上下文系统：使用 `prompts/review-agent-context.md`，清理上下文膨胀（context bloat）、上下文漂移（context drift）和过期内容。

用户不需要每次重新组织提示词，按场景使用对应 prompt 即可。

## 适用场景

- 在新项目中初始化 `agent-context/`。
- 为项目建立或整理 `AGENTS.md`。
- 在当前会话变长、任务中断或需要切换会话时更新 handoff。
- 新会话从指定 handoff 接续工作。
- 定期检查 `AGENTS.md` 和 handoff 是否出现上下文膨胀（context bloat）、上下文漂移（context drift）、重复、冲突或过期内容。

这个 skill 必须保持通用，不绑定任何行业、业务类型、文档类型、技术栈、工具链或项目组织方式。

## 标准工作流

1. 先扫描目标项目结构，不要直接编写上下文文件。
2. 只识别实际存在或用户明确提供的项目源资料类型。
3. 使用 `templates/AGENTS.template.md` 创建或更新 `agent-context/AGENTS.md`。
4. 创建 `agent-context/handoff/` 用于存放交接文档。
5. 当会话变长、任务暂停或需要转入新会话时，创建或更新相关 handoff。
6. 定期审查 `AGENTS.md` 和 handoff，清理膨胀、重复、过期路径和被复制进来的项目源资料正文。

## 根目录 `AGENTS.md` 与 `agent-context/AGENTS.md`

为了兼容 Codex / Agent 的自动读取习惯，目标项目可以在根目录保留一个极简 `AGENTS.md` 作为入口文件。

- 根目录 `AGENTS.md`：只负责指向 `agent-context/AGENTS.md` 和相关 handoff，不承载复杂规则或项目资料。
- `agent-context/AGENTS.md`：承载详细但仍轻量的项目导航、目录说明、协作规则和 handoff 规则。

如果根目录已经存在 `AGENTS.md`，不要覆盖。先读取内容，再建议用户是否合并或追加入口说明。

## 信息优先级

当不同信息来源出现冲突时，按以下优先级处理：

1. 用户当前明确指令
2. 项目源资料（source material）的当前内容
3. 根目录 `AGENTS.md` 与 `agent-context/AGENTS.md`
4. 指定交接文档（handoff）
5. 旧聊天记录、旧摘要或旧交接内容

如果 handoff 与当前项目源资料冲突，应明确报告冲突，并以当前项目源资料为准，除非用户另有说明。

## 职责边界

### `AGENTS.md`

`AGENTS.md` 是某个项目的长期导航文件。它应该稳定、轻量、面向后续 agent 协作。

它应该包含：

- 项目定位和长期边界。
- 项目源资料类型的简要说明。
- 顶层目录导航。
- Agent 工作规则。
- 常见误区和禁止事项。
- Handoff 使用规则。

它不应该包含：

- 单个任务的临时进度。
- 单个会话状态。
- 大段项目源资料正文。
- 应留在项目文件或项目源资料中的详细实现说明。
- 长篇版本历史。
- 原始讨论记录全文。
- 与长期协作无关的临时说明。

### `handoff/`

`handoff/` 存放交接文档，用于保留另一个会话继续某个具体任务所需的最小状态。

Handoff 应该包含：

- 当前状态。
- 已确定结论。
- 卡点或待确认问题。
- 下一步。
- 新会话需要读取的关键文件。

Handoff 不应该包含：

- 从 `AGENTS.md` 复制来的全局规则。
- 项目源资料正文。
- 长篇背景说明。
- 大段文件内容。
- 原始讨论记录全文。
- 与当前任务无关的全项目索引。
- 已经过期或不再影响后续工作的内容。

### 项目源资料

项目源资料是事实依据。`AGENTS.md` 和 handoff 可以引用项目源资料的路径，并简要说明用途，但不要复制大段正文或完整内容。

当事实可能已经变化时，重新读取项目源资料，不要依赖过期摘要。

## 当前会话如何更新 Handoff

1. 判断当前任务应更新已有 handoff，还是新建一个 handoff。
2. 只保留继续当前任务所必需的信息。
3. 删除已解决、过期或会误导后续工作的内容。
4. 用简短条目记录已确定结论。
5. 将卡点和待确认问题与结论分开。
6. 按执行顺序写清楚下一步。
7. 只列与当前任务强相关的关键文件，并说明为什么要读。

推荐 handoff 文件名：

```text
agent-context/handoff/{topic}-{YYYYMMDD}.md
```

- `topic` 使用简短英文、拼音或稳定项目代号均可。
- 同一任务继续更新原 handoff。
- 不同任务新建独立 handoff。
- 已完成、重复或过期的 handoff 应标记 obsolete 或删除。
- 不要为同一任务反复创建多个 handoff。
- Handoff 文件名要稳定，不要每次随意变化。

需要可复用提示词时，使用 `prompts/update-handoff.md`。

## 新会话如何从 Handoff 接续

1. 先读 `agent-context/AGENTS.md`。
2. 再读指定的 handoff 文件。
3. 按 handoff 中的关键文件读取必要资料。
4. 先复述当前状态、下一步计划和需要查看的文件。
5. 用户确认接续计划前，不要直接进行大规模修改。
6. 接续工作后，如果任务状态发生实质变化，及时更新 handoff。

需要可复用提示词时，使用 `prompts/start-from-handoff.md`。

## 内置资源

- `templates/AGENTS.template.md`：通用项目级 Agent 导航模板。
- `templates/handoff.template.md`：通用短交接模板。
- `prompts/install-agent-context.md`：在新项目中初始化 `agent-context/` 的提示词。
- `prompts/update-handoff.md`：创建或更新 handoff 的提示词。
- `prompts/start-from-handoff.md`：从 `AGENTS.md` 和指定 handoff 接续工作的提示词。
- `prompts/review-agent-context.md`：审查上下文膨胀、上下文漂移和过期 handoff 的提示词。

## 禁止事项

- 不要在这个 skill 中存放具体项目事实。
- 不要假设项目属于某个固定行业、业务类型、文档类型、项目源资料类型、框架、语言或工具链。
- 不要编造不存在的项目源资料类型、路径、约束或项目事实。
- 不要把 `AGENTS.md` 变成仓库全文索引、资料库、日志库或任务流水账。
- 不要把 handoff 变成长篇背景、全项目总结、原始记录全文或项目源资料副本。
- 不要在多个 handoff 中重复应属于 `AGENTS.md` 的全局规则。
- 不要保留过期、已完成或会误导后续工作的 handoff 内容。
- 不要增加复杂分类、状态体系或目录结构，除非目标项目确实已经需要。
