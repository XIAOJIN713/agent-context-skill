# 提示词（Prompt）：更新 Handoff

当当前会话（session）变长、任务中断或准备切换到新会话时，使用这段提示词更新交接文档（handoff）。

```text
你正在为当前任务更新 handoff 状态。

目标：
在 `agent-context/handoff/` 中创建或更新相关 handoff，让新会话能以最小上下文损失继续工作。

执行要求：
1. 如果存在 `agent-context/AGENTS.md`，先读取它。
2. 判断当前任务是否已有匹配的 handoff。有则更新；没有则用清晰、稳定的文件名新建 handoff。
3. 只记录继续当前会话或任务所需的信息。
4. 删除或修订过期、已解决、重复或会误导后续工作的内容。
5. 将已确定结论与卡点、待确认问题分开。
6. 按执行顺序写清楚下一步。
7. 列出新会话应该读取的关键文件，并为每个文件写一句原因。
8. 不要复制 `AGENTS.md` 中的全局规则。
9. 不要复制项目源资料（source material）正文。
10. 不要写长篇背景、原始讨论记录、全项目总结或宽泛仓库（repository）索引。

Handoff 命名规则：
- 推荐文件名：`agent-context/handoff/{topic}-{YYYYMMDD}.md`
- `topic` 使用简短英文、拼音或稳定项目代号均可。
- 优先更新已有 handoff，不要为同一任务反复创建多个 handoff。
- 不同任务新建独立 handoff。
- 已完成、重复或过期的 handoff 应标记 obsolete 或删除。
- Handoff 文件名要稳定，不要每次随意变化。

编辑前：
- 说明将更新已有 handoff，还是新建 handoff。
- 说明目标 handoff 路径。

编辑后：
- 概括当前状态、下一步和关键文件。
```
