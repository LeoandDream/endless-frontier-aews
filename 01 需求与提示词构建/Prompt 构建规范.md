# Instruction Artifact 构建规范

> AEWS v0.2.0 · Normative Specification

## 1. 定位

本规范定义 AEWS Generator 如何从 Requirement READY 的 CTS 生成可交给下游 Execution Agent 的 Instruction Artifact。文件名保留“Prompt 构建规范”以保持导航兼容；其正式含义已经扩展为 Artifact Construction。

核心链路：

~~~text
Natural Language Request
→ Requirement Draft
→ Necessary Prompt Context
→ Requirement Readiness
→ Canonical Task Specification
→ Instruction Artifact Generation
→ ARTIFACT_READY
→ Downstream Execution Agent
~~~

## 2. Artifact Types

### TASK_PROMPT.md

默认的单次任务 Artifact，适用于 Research、Analysis、Engineering、Debug、Integration、Experiment、Documentation、Environment、Review、Reproduction 等。它描述下游 Agent 应如何检查、研究、计划、执行、验证和交付。

### Target Project AGENTS.md

用于长期项目或实验环境治理。它可直接放入目标项目根目录，约束未来进入该项目的 Execution Agent。它不是 AEWS Repository 的 Generator `AGENTS.md`，也不得覆盖后者。

### CONTINUE_PROMPT.md

用于下游任务的 PAUSED、BLOCKED、PARTIAL、UNVERIFIED、FAILED 或 Agent 切换后的恢复。它向后续 Execution Agent 提供检查点、事实、已完成工作、阻塞、尝试、恢复条件和下一步。

## 3. 前置条件与默认生成

Requirement READY 的含义是 Generator 已有足够信息生成可靠 Artifact。READY 后 MUST 自动生成最合适的 Artifact；用户不需要说“生成 Prompt”“进入 BUILD”或“给另一个 Agent 用”。

Generator 默认不完成目标任务本身。用户明确要求直接回答、直接分析或当前 Agent 直接执行时，才覆盖默认行为；覆盖不应被误标为 `ARTIFACT_READY`。

## 4. TASK_PROMPT 必备语义

按任务适用性，`TASK_PROMPT.md` 必须包含以下语义；章节可省略或写 `N/A`，但语义不能缺失：

1. `Task`：任务标题、任务形态和目标受众；
2. `Goal`：下游 Agent 要解决的问题与期望结果；
3. `Deliverables`：必须交付的代码、研究结果、报告、配置、证据或续接材料；
4. `Current Context`：已知背景和目标环境边界；
5. `Verified Facts`：Generator 已确认的事实及来源；
6. `User Decisions`：已确认的材料性决定；
7. `Scope` / `Out of Scope`：必须处理与明确排除的内容；
8. `Constraints`：兼容性、依赖、安全、性能、工作区和时间约束；
9. `Context to Inspect`：Target Project Context、Reference Context、检查目的和来源优先级；
10. `Research / Investigation Requirements`：研究问题、来源范围、检索和验证方式；
11. `Planning / Execution Requirements`：适用时的 Inspect、Understand、Plan、Execute、Evaluate；
12. `Decision Boundary`：L0–L3 下游决策和授权规则；
13. `Acceptance Criteria` / `Verification Requirements`：完成判断、证据和 Authority；
14. `Stop / Replan Conditions`：Material Unknown、L2/L3、Scope 扩大、证据冲突或环境阻塞时的行为；
15. `Delivery Requirements`：Completion、Reproduction、Continuation 和报告要求。

纯研究 Prompt 可强调 Research、Source、Verification、Delivery，并将 `Execution Requirements` 省略或标记 `N/A`。代码任务通常需要 Inspect、Plan、Execute、Verify 与 Delivery。

## 5. 信息编排原则

### 5.1 事实、推断与目标环境分离

把 Generator Verified Facts、Assumptions、Unknowns 和 Target Project Context 分开。不得用确定语气包装推断，也不得把将由下游 Agent 检查的目标项目事实写成 Generator 已验证事实。

### 5.2 重要语义直接嵌入

Goal、Deliverables、Scope、Out of Scope、User Decisions、关键 Constraints、Acceptance、Verification、Decision Authority 和 Delivery 必须直接写入 Artifact。

### 5.3 引用而不是复制

大型源码、配置、日志、论文、数据集和官方文档应给出路径、URL、范围、来源权威性和使用目的。不要复制整个项目或把 Reference Index 当作当前项目快照。

### 5.4 Minimum Sufficient Prompt Context

Artifact 必须足以启动可靠下游工作，但不要求 Generator 先执行下游调查或研究。缺少目标环境事实时，写明 Execution Agent 的 Inspect / Research 要求，而不是编造答案。

## 6. Target Project AGENTS 生成

当用户请求长期项目治理时，Generator 生成目标项目 `AGENTS.md`，至少包含：Project Goal、Project Context、Source of Truth、Context Sources、Research / Coding / Experiment Rules、Decision Boundary、Inspect / Plan / Execute Expectations、Verification、Evidence、Completion Gate、Failure Handling、Delivery 和 Continuation。

该 Artifact 必须显式写明它属于目标项目，避免与 AEWS Generator `AGENTS.md` 混淆。详见 [Target Project AGENTS 生成规范](Target%20Project%20AGENTS%20生成规范.md)。

## 7. Artifact 质量门

输出前检查：

- [ ] Artifact 类型符合用户目标，且没有无理由生成多个 Artifact；
- [ ] Artifact 面向下游 Execution Agent，而不是把 Generator 的工作描述为目标执行；
- [ ] Goal、Deliverables、Scope、事实和 User Decisions 真实且分离；
- [ ] Reference Context 与 Target Project Context 已区分；
- [ ] Material Unknown 已解决，或成为下游明确的 Inspect / Stop / Ask User 条件；
- [ ] 适用的 Research / Execution / Verification 要求完整；
- [ ] 不适用章节已省略或 `N/A`，而非强制填充；
- [ ] 每条必要 Acceptance 都有 Verification / Authority；
- [ ] L2/L3 规则没有被静默绕过；
- [ ] Delivery、Continuation 与复现语义符合下游任务；
- [ ] Generator 状态可标记为 `ARTIFACT_READY`，但未把目标任务标为 COMPLETED。

## 8. Artifact 与下游生命周期

Artifact 是下游工作输入，不替代当前项目状态、目标项目约束或用户显式指令。Execution Agent 使用 Artifact 后，遵循：

~~~text
Inspect → Understand → Plan → Research / Execute → Verify → Evaluate → Deliver / Replan / Ask User / Stop
~~~

如果下游当前事实与 Artifact 冲突，Execution Agent 必须记录差异、停止静默执行并重新收敛；不得让 Generator 的历史推断覆盖现场事实。
