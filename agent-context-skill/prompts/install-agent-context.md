# 提示词（Prompt）：初始化 Agent Context

在新项目中使用这段提示词，初始化轻量上下文系统（agent context system）。

```text
你正在为当前项目建立一套可复用的上下文系统（agent context system）。

目标：
创建轻量的 `agent-context/`，包含 `agent-context/AGENTS.md` 和 `agent-context/handoff/`。

执行要求：
1. 编辑前先扫描仓库（repository）或工作区（workspace）结构。可用时优先使用快速文件列表和搜索工具。
2. 只识别实际存在或用户明确提供的项目源资料（source material）类型。项目源资料可以是文档、代码、图片、表格、配置文件、参考资料、会议记录、设计稿、数据文件、日志、README、外部资料说明，或其他项目文件和输入材料。
3. 使用通用模板（template）创建 `agent-context/AGENTS.md`。保持短小、稳定、长期有效。
4. 创建 `agent-context/handoff/`，用于后续交接文档（handoff）。
5. 如果当前已有需要延续的活跃任务，创建一个聚焦的 handoff。否则只保留 handoff 目录备用。
6. 检查项目根目录是否已有 `AGENTS.md`。
7. 如果根目录没有 `AGENTS.md`，创建极简入口文件，只指向 `agent-context/AGENTS.md` 和 `agent-context/handoff/*.md`。
8. 如果根目录已经存在 `AGENTS.md`，不要覆盖。先检查内容，再建议用户是否合并或追加入口说明。
9. 只写路径和简短用途说明。不要把项目源资料正文塞进 `AGENTS.md`。
10. 不要编造不存在的项目源资料类型、路径、项目事实、规则或约束。
11. 不要过度设计目录结构。只添加当前确实需要的内容。

根目录入口文件示例：

```md
# AGENTS.md

本项目的详细 Agent 导航位于：

`agent-context/AGENTS.md`

开始重要任务前，请先读取该文件。

如果是从旧会话接续任务，请同时读取对应的：

`agent-context/handoff/*.md`
```

编辑前：
- 用 3-6 条说明将创建或更新哪些文件和目录。

编辑后：
- 输出最终文件结构。
- 简要说明每个文件的用途。
- 说明哪些项目源资料类型因为不存在或未确认而没有写入。
```
