# 提示词（Prompt）：审查 Agent Context

定期使用这段提示词，检查 `AGENTS.md` 和交接文档（handoff）是否变重、重复、冲突，或混入项目源资料正文。

```text
你正在审查项目的上下文系统（agent context system），重点检查上下文膨胀（context bloat）和上下文漂移（context drift）。

范围：
- `agent-context/AGENTS.md`
- `agent-context/handoff/`
- 必要时检查被引用的项目源资料（source material）路径，以确认是否过期

检查项：
1. `AGENTS.md` 是否仍是轻量导航，还是已经变成资料库、日志库、任务流水账或仓库（repository）全文索引？
2. `AGENTS.md` 是否写入了应属于 handoff 的具体会话（session）进度？
3. 是否有 handoff 复制了 `AGENTS.md` 的全局规则？
4. 是否有 handoff 复制了项目源资料正文，而不是引用路径？
5. 是否存在过期、缺失或已改名的路径？
6. 是否存在覆盖同一活跃任务的重复 handoff？
7. 旧 handoff 是否需要合并、拆分、删除或标记为过期？
8. 当前上下文系统是否相对项目需要显得过度设计？
9. 是否存在没有项目依据的项目源资料类型、项目事实或约束？
10. 根目录 `AGENTS.md` 是否存在，并且只作为极简入口？
11. 根目录 `AGENTS.md` 是否错误承载了大量规则、项目资料或任务状态？
12. `agent-context/AGENTS.md` 是否仍保持轻量？
13. 是否存在多个 handoff 覆盖同一个任务？

执行要求：
1. 读取 `agent-context/AGENTS.md`。
2. 列出 `agent-context/handoff/` 下的 handoff 文件。
3. 只检查本次审查需要的 handoff。
4. 对可疑路径，先在仓库中验证，再判断是否过期。
5. 先输出问题，按严重程度排序。
6. 推荐最小必要修改。
7. 如果用户要求编辑，只做小而聚焦的修改，不要整体重写。

输出：
- 问题清单
- 建议修改
- 应更新、合并、拆分、删除或保持不变的文件
- 需要用户确认的不确定项
```
