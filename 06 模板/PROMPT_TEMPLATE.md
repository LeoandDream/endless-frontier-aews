# TASK_PROMPT 模板

> AEWS v0.2.0  
> 用途：由 AEWS Generator 为单次目标任务生成、供下游 Execution Agent 使用的正式执行指令。  
> 适用边界：这是 `TASK_PROMPT.md` 模板，不是执行记录，也不授权 Generator 直接执行目标任务。

## 0. Artifact Metadata

| 字段 | 内容 |
|---|---|
| Artifact Type | `TASK_PROMPT.md` |
| Generator State | `ARTIFACT_READY` |
| Target Project / Workspace | <!-- target --> |
| Task Type | <!-- research / analysis / engineering / documentation / other --> |
| Generated At | <!-- date/time --> |
| Source Requirement | <!-- requirement draft or user request reference --> |

## 1. Goal

<!-- 用一句可验证的话说明下游 Agent 要达成的目标。 -->

## 2. Deliverables

<!-- 明确需要交付的研究结果、代码、配置、报告、证据、复现或续接材料；无则写 N/A。 -->

## 3. Scope

### In Scope

<!-- 明确本任务允许处理的对象、目录、系统或问题。 -->

### Out of Scope

<!-- 明确不可处理的对象和不应擅自扩张的工作。 -->

## 4. Verified Facts and Context

<!-- 仅记录 Generator 已获得、可追溯且对任务必要的事实。 -->

| Fact / Context | Source | Confidence / Limitation |
|---|---|---|
| <!-- fact --> | <!-- source --> | <!-- limit --> |

### Required Target-Context Inspection

<!-- 写明下游 Agent 必须先自行检查的目标项目上下文、README、AGENTS、官方资料或现状。不要把 Generator 未完成的深度研究伪装成事实。 -->

## 5. User Decisions and Constraints

<!-- 只记录用户已作出的材料性决定、硬约束与偏好。未决定项不要由 Generator 擅自补全。 -->

## 6. Execution Decision Boundary

- L0 — Autonomous: <!-- low-risk, local, reversible work -->
- L1 — Autonomous + Record: <!-- equivalent choices that must be recorded -->
- L2 — Ask User: <!-- material project choices -->
- L3 — Explicit Authorization: <!-- destructive / high-risk actions -->

## 7. Acceptance Criteria

<!-- 每条应可由下游 Agent 以证据验证；区分 mandatory 与 optional。 -->

| Priority | Criterion | Evidence Required |
|---|---|---|
| Mandatory | <!-- criterion --> | <!-- test / inspection / artifact --> |
| Optional | <!-- criterion --> | <!-- test / inspection / artifact --> |

## 8. Required Execution Workflow

1. Inspect：检查目标项目、约束、现状和必要上下文。
2. Understand：确认需求、风险、依赖和事实边界。
3. Plan：提出可执行计划；材料性分歧依照任务约束处理。
4. Research / Execute：按需要调研、实现或分析，不将实现细节无意义上抛给用户。
5. Verify：运行或执行与 Acceptance Criteria 相匹配的验证，并记录证据。
6. Evaluate：判断每项 mandatory criterion 是否通过；不可客观判断时进入 `UNVERIFIED` 或 `AWAITING_USER`。
7. Deliver：按交付要求输出结果、限制、复现和续接信息。

## 9. Execution Constraints

<!-- 填写安全、兼容性、时间、依赖、禁止修改范围、资料来源或平台限制。按适用性保留。 -->

## 10. Stop / Replan Conditions

<!-- 说明 Material Unknown、现场事实冲突、L2/L3 操作、范围扩大、环境阻塞或证据不足时应停止、重规划或向用户提问的条件。 -->

## 11. Verification Plan

| Acceptance Criterion | Verification Method | Passing Evidence |
|---|---|---|
| <!-- criterion --> | <!-- method --> | <!-- evidence --> |

## 12. Delivery Requirements

<!-- 说明下游 Agent 最终必须交付的文件、报告、链接、命令、证据和用户需验证事项。 -->

## 13. Continuation Requirements

<!-- 若任务可能暂停，要求记录 Checkpoint、已完成/未完成、下一步、风险和 Continue Prompt 所需上下文。若不适用可标记 N/A。 -->

## 14. Open Questions / User Validation

<!-- 仅记录无法由 Agent 客观判定或需要用户作材料性决定的事项；无则写 N/A。 -->

---

## Generator Quality Check

- [ ] Artifact Type 与任务类型匹配，且不是对目标任务的直接执行。
- [ ] Goal、Scope、Verified Facts、User Decisions、Acceptance Criteria、Verification、Delivery 均已覆盖或明确 N/A。
- [ ] Deliverables、Decision Boundary 与 Stop / Replan 条件已覆盖或明确 N/A。
- [ ] 没有将猜测、未调查的目标上下文或 AI 擅自补充的重要需求写成事实。
- [ ] 下游 Agent 获得足以开始 Inspect 的 Minimum Sufficient Prompt Context。
- [ ] 所有深度目标调研都作为下游执行要求表达，而不是被 Generator 越权完成。
- [ ] 生成后状态为 `ARTIFACT_READY`；这不等同于目标任务 `COMPLETED`。
