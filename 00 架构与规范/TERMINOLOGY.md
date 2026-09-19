# 术语表

> AEWS v0.2.0 · Informative / Normative Reference

| 术语 | 定义 |
| --- | --- |
| AEWS Generator | 将用户自然语言转换为 Instruction Artifact 的当前 AEWS Agent / 会话角色 |
| Downstream Execution Agent | 接收 Artifact 后在真实 Target Project / Research Environment 中研究、实现、验证和交付的 Agent |
| Instruction Artifact | Generator 的正式产品：`TASK_PROMPT.md`、目标项目 `AGENTS.md` 或 `CONTINUE_PROMPT.md` |
| TASK_PROMPT.md | 默认单次任务 Artifact，给 Execution Agent 的可执行任务指令 |
| Target Project AGENTS.md | 放入目标项目根目录的长期 Agent 工作契约，不是 AEWS Generator AGENTS |
| CONTINUE_PROMPT.md | 供后续 Execution Agent 恢复中断任务的续接 Artifact |
| Task Interpretation | Generator 对用户希望未来 Agent 完成什么的明确理解 |
| Requirement Draft | 尚未通过 Artifact Readiness Gate 的任务草案 |
| Requirement READY | Generator 已有足够信息生成可靠 Artifact，不表示目标任务可直接执行 |
| ARTIFACT_READY | Artifact 已生成并通过 Generator Artifact Gate；不表示下游任务已开始或完成 |
| Minimum Sufficient Prompt Context | 足以可靠生成 Artifact 的最小上下文；不包括下游任务本身应完成的深度研究 |
| AEWS Reference Context | 供 Generator 定位事实、路径、URL 和资料的上下文，不自动成为目标项目 Scope |
| Target Project Context | 下游 Agent 必须在真实项目或研究环境中检查的当前代码、配置、数据、测试、设备等 |
| Execution Workflow | 下游 Agent 的 Inspect、Understand、Plan、Research / Execute、Verify、Evaluate、Deliver 生命周期 |
| Generator Decision Boundary | Generator 调查、澄清、Artifact 选择和任务语义的权限边界 |
| Execution Decision Boundary | 写入 Artifact 的下游 L0–L3 自主、询问和授权规则 |
| L0 / L1 / L2 / L3 | 分别表示自主、记录型自主、用户材料性决策和针对性明确授权 |
| Completion Gate | 下游 Execution Agent 标记 COMPLETED 前必须通过的验收、证据、Authority、复现和交付条件 |
| Execution Task State | IN_PROGRESS、VERIFYING、COMPLETED、UNVERIFIED、AWAITING_USER、BLOCKED、PAUSED、FAILED 等下游状态 |
| Source of Truth | 对 Artifact 或目标项目事实有最终权威的用户指令、正式规范、现场状态或项目资料 |
| System Maintenance Workflow | 修改 AEWS 自身时使用的受控维护流程 |
| Explicit User Override | 用户明确要求直接回答、跳过 Artifact 或当前 Agent 直接执行时对默认行为的覆盖 |
