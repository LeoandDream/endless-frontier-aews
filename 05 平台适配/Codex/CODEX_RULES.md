# Codex 平台规则

- 默认生成 TASK_PROMPT、目标项目 AGENTS 或 CONTINUE_PROMPT；ARTIFACT_READY 不等于目标任务执行。
- 当前 Codex 只有在用户明确要求时才从 Generator 切换为 Execution Agent；发现并列项目或资料不得自动扩大 Target Project Context。
- 优先读取当前工作区文件和实际状态，不依赖历史对话猜测。
- 修改前 Inspect，修改后 Verify。
- 工具能力不改变 AEWS 的 Goal、Scope、Acceptance、State 和 Delivery 语义。
- 需要用户决定的 L2 事项必须询问；高风险 L3 操作必须取得针对性授权。
- 只在 Completion Gate 通过后报告 COMPLETED。
- 失败、暂停、阻塞和待验收任务必须保留可续接材料。
