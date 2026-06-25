# Agent Context Skill

一个中文优先、通用的上下文系统（agent context system）模板包，用于帮助 Codex 和其他代理 / AI 代理（agent）在任意仓库（repository）、工作区（workspace）或项目（project）中维护长期上下文。

这个项目只提供方法、模板（template）、提示词（prompt）和通用规则，不存放任何具体项目事实、任务进度或项目源资料正文。

## 解决什么问题

长任务、跨会话协作和长期维护项目时，agent 容易遇到这些问题：

- 新会话不知道项目稳定规则和边界。
- 旧交接文档（handoff）被当成最新事实。
- `AGENTS.md` 越写越重，变成资料库、日志库或全文索引。
- 交接文档（handoff）变成长篇背景、会议纪要或全项目总结。
- 项目源资料（source material）被复制到上下文文件里，造成重复和过期。

这个 skill 的目标是把长期稳定信息、当前任务交接状态和项目源资料分开管理。

## 适用范围

适用于任意 repository / workspace / project。

不绑定具体行业、业务类型、文档类型、技术栈、工具链或项目组织方式。

## 核心概念

### `AGENTS.md`

项目长期导航文件，记录稳定的项目目标、顶层目录、工作规则、常见误区和 handoff 使用规则。

它不应该记录单个任务进度、长篇背景、项目源资料正文或原始讨论记录。

### 交接文档（handoff）

单个会话（session）或任务线程的最小接续状态，通常放在 `agent-context/handoff/`。

它只记录当前状态、已确定结论、卡点、下一步和关键文件。

### 项目源资料（source material）

为项目提供事实依据、上下文、约束或参考价值的任何材料。它可以是文档、代码、图片、表格、配置、日志、README、外部资料说明或其他项目文件。

`AGENTS.md` 和 handoff 可以引用项目源资料路径，但不要复制大段正文。

## 推荐目录结构

```text
agent-context-skill/
  SKILL.md
  templates/
    AGENTS.template.md
    handoff.template.md
  prompts/
    install-agent-context.md
    update-handoff.md
    start-from-handoff.md
    review-agent-context.md
```

在目标项目中推荐生成：

```text
AGENTS.md
agent-context/
  AGENTS.md
  handoff/
    {topic}-{YYYYMMDD}.md
```

根目录 `AGENTS.md` 负责让 Codex / Agent 自动发现入口。`agent-context/AGENTS.md` 负责承载详细但仍轻量的项目导航。

## 快速使用

- 新项目初始化：使用 `prompts/install-agent-context.md`，扫描项目并创建 `agent-context/`。
- 当前会话快满 / 任务中断：使用 `prompts/update-handoff.md`，更新当前任务的 handoff。
- 新会话接续：使用 `prompts/start-from-handoff.md`，从 `AGENTS.md` 和指定 handoff 继续工作。
- 定期审查上下文系统：使用 `prompts/review-agent-context.md`，清理上下文膨胀（context bloat）和上下文漂移（context drift）。

用户不需要每次重新组织提示词，直接使用对应 prompt 即可。

## 信息优先级

当不同信息来源出现冲突时，按以下优先级处理：

1. 用户当前明确指令
2. 项目源资料（source material）的当前内容
3. 根目录 `AGENTS.md` 与 `agent-context/AGENTS.md`
4. 指定交接文档（handoff）
5. 旧聊天记录、旧摘要或旧交接内容

如果 handoff 与当前项目源资料冲突，应明确报告冲突，并以当前项目源资料为准，除非用户另有说明。

## 新项目如何初始化 `agent-context/`

使用 `prompts/install-agent-context.md`：

1. 先扫描项目结构。
2. 判断实际存在的项目源资料类型。
3. 创建轻量 `agent-context/AGENTS.md`。
4. 创建 `agent-context/handoff/`。
5. 如果根目录没有 `AGENTS.md`，创建极简入口文件指向 `agent-context/AGENTS.md`。
6. 如果根目录已有 `AGENTS.md`，不要覆盖，先检查并建议合并或追加入口说明。

## 当前会话快满 / 任务中断时如何更新 handoff

使用 `prompts/update-handoff.md`。

推荐文件名：

```text
agent-context/handoff/{topic}-{YYYYMMDD}.md
```

`topic` 可以使用简短英文、拼音或稳定项目代号。同一任务继续更新原 handoff，不同任务新建独立 handoff。已完成、重复或过期的 handoff 应标记 obsolete 或删除。

## 新会话如何从 handoff 接续

使用 `prompts/start-from-handoff.md`：

1. 先读根目录 `AGENTS.md`，如果它指向 `agent-context/AGENTS.md`，继续读取后者。
2. 再读指定 handoff。
3. 再按 handoff 中的关键文件读取必要项目源资料。
4. 读取后先复述当前状态、下一步计划和需要查看的文件。
5. 用户确认前不要直接大规模修改。

## 如何定期审查上下文系统

使用 `prompts/review-agent-context.md`，重点检查：

- `AGENTS.md` 是否变成资料库、日志库或全文索引。
- `AGENTS.md` 是否混入具体会话进度。
- Handoff 是否复制了 `AGENTS.md` 或项目源资料正文。
- 是否有过期路径或重复 handoff。
- 是否需要合并、拆分、删除或标记 obsolete。
- 根目录 `AGENTS.md` 是否仍保持极简入口职责。

## 禁止事项

- 不要把这个 skill 写成某个具体项目的说明。
- 不要在 skill 本体中存放项目事实、任务进度或项目源资料正文。
- 不要把 `AGENTS.md` 变成全文索引、资料库或任务日志。
- 不要把 handoff 写成长篇背景、会议纪要、源资料复述或全项目总结。
- 不要为同一任务反复创建多个 handoff。
- 不要编造不存在的路径、资料类型、项目事实或约束。
- 不要擅自加入网络调用、遥测或与上下文管理无关的复杂机制。

## Codex Skill 推荐安装位置

作为 Codex skill 使用时，推荐将 `agent-context-skill/` 放到：

```text
~/.codex/skills/agent-context-skill/
```

如果设置了 `CODEX_HOME`，则放到：

```text
$CODEX_HOME/skills/agent-context-skill/
```

也可以把本仓库作为模板，在其他项目中复制 `templates/` 和 `prompts/` 使用。
