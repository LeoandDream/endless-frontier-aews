# Generator State 与 Execution Task State

> AEWS v0.2.0 · Normative Specification

## 1. 两类状态不得混同

AEWS Generator 的状态描述 Artifact 构建能否继续；下游 Execution Agent 的状态描述目标任务在真实环境中的执行、验证和交付。二者不得互相代替。

`ARTIFACT_READY` 不等于 `IN_PROGRESS`、`VERIFYING` 或 `COMPLETED`。历史 `PROMPT_READY` 是 v0.1.x 的状态名称；从 v0.2.0 起由 `ARTIFACT_READY` 取代，但历史记录不自动迁移。

## 2. Generator State

| State | 含义 | Generator 必须交付 |
| --- | --- | --- |
| REQUIREMENT_DRAFT | 对下游 Intended Task 的初步理解尚未收敛 | Draft、Artifact 假设、未知和 Context Gap |
| CONTEXT_ACQUISITION | 正在获得生成 Artifact 所需的最小上下文 | 已核验事实、来源、剩余调查边界 |
| AWAITING_USER | 需要用户决定 Artifact / Goal / Scope / Acceptance 的材料性事项 | 澄清问题、影响、选项和推荐 |
| REQUIREMENT_READY | 已有足够信息生成可靠 Artifact | Readiness 判断和 CTS |
| ARTIFACT_READY | Artifact 已生成并通过质量门 | TASK_PROMPT、目标项目 AGENTS 或 CONTINUE_PROMPT；执行授权说明 |
| CANCELLED | 用户终止 Artifact 构建 | 当前 Draft、已知事实和终止原因（如有价值） |

Generator 只能使用上述状态描述自己当前阶段。用户显式要求直接回答或当前 Agent 直接执行时，必须说明 Override，而不是伪造 `ARTIFACT_READY`。

## 3. Execution Task State（Downstream）

| State | 含义 | Execution Agent 必须交付 |
| --- | --- | --- |
| IN_PROGRESS | 已开始目标任务，仍有工作 | 检查点和下一步 |
| VERIFYING | 产物已产生，正在验证 | 验证计划和中间 Evidence |
| COMPLETED | Execution Completion Gate 全部通过 | Completion Report + Reproduction |
| UNVERIFIED | 产物存在，但关键证据不足 | 缺失证据和验证计划 |
| AWAITING_USER | 等待目标项目用户决定或验收 | 决策问题或可观察结果 |
| BLOCKED | 外部条件或依赖阻止继续 | Blocker + CONTINUE_PROMPT |
| PAUSED | 用户或策略主动暂停 | Checkpoint + Resume 条件 + CONTINUE_PROMPT |
| FAILED | 任务已确认无法达到目标或明确终止 | 失败证据、后续建议和续接信息 |

Attempt Failure 不自动触发 FAILED。

## 4. 状态流转

~~~text
Generator:
REQUIREMENT_DRAFT
→ CONTEXT_ACQUISITION
→ AWAITING_USER（如需要）
→ REQUIREMENT_READY
→ ARTIFACT_READY

Downstream Execution Agent:
ARTIFACT_READY（作为输入，不是其状态）
→ IN_PROGRESS
→ VERIFYING
→ COMPLETED / UNVERIFIED / AWAITING_USER / BLOCKED / PAUSED / FAILED
~~~

Generator 为下游任务生成 Artifact 后不能自行宣布 `COMPLETED`。只有下游 Agent 取得实际证据并通过 Completion Gate，才可将目标任务标记为 COMPLETED。

## 5. Generator Artifact Gate

Generator 可以标记 `ARTIFACT_READY` 的条件：

- [ ] Artifact 类型符合用户目标；
- [ ] Goal、Deliverables、Scope、Constraints、User Decisions 和 Context Sources 足够明确；
- [ ] 所有阻止可靠构建的 Material Unknown 已解决；
- [ ] 下游需要现场检查、询问或授权的事项已写入 Artifact；
- [ ] Artifact 包含适用的 Acceptance、Verification、Decision Boundary、Stop / Replan 和 Delivery 语义；
- [ ] 没有把 Generator 的分析或推断表示为下游执行结果；
- [ ] 没有无授权修改目标项目。

## 6. Execution Completion Gate

Execution Completion Gate 由 [验证与验收规范](VERIFICATION_PROTOCOL.md) 定义。它只适用于下游目标任务，至少要求 Goal、Deliverables、Acceptance、Evidence、Authority、Material Unknown、复现材料和交付报告均满足。

## 7. 历史状态

v0.1.x 历史 Prompt、PROMPT_READY 和 COMPLETED 记录保留其原版本语义。除非用户明确要求重新生成 Artifact 或重新执行验证，v0.2.0 不自动迁移或降级历史任务。
