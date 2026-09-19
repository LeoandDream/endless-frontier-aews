# 通用工程任务 Workflow（Downstream Execution Agent）

> AEWS v0.2.0 · ACTIVE · REQUIRED when applicable

## Applicability

本 Workflow 由 AEWS Generator 写入涉及代码、配置、集成、重构、测试、文档实现或工程产物的 `TASK_PROMPT.md`。它约束下游 Execution Agent；Generator 默认不执行其中的修改阶段。

## Required Context

下游 Agent 执行前必须检查：

- Artifact 中指定的目标项目目录、文件和调用链；
- 当前实现、配置、测试、文档、Git 状态和已有改动；
- 用户已确认的 Goal、Scope、Constraints、Acceptance 与 Decision Boundary；
- 相关环境、依赖、服务、数据、硬件和已知失败信息；
- Artifact 区分的 AEWS Reference Context 与 Target Project Context。

## Inspect

1. 识别目标组件、入口、调用链、配置和相关测试。
2. 检查当前实际行为，不以 Artifact 的历史摘录替代现场证据。
3. 记录影响范围、已有改动和可能的回归面。
4. 修改前确认 Scope、Out of Scope、L2/L3 与执行授权。

## Understand

明确区分 Observed Facts、Known Constraints、Expected Behavior、Actual Behavior、Unknowns 与 Hypotheses。关键假设被新证据推翻时，停止当前分支并重新规划。

## Plan

计划至少说明最小有效修改、受影响文件和接口、Acceptance 与 Verification、增量顺序、中间验证、回滚或停止点，以及需要用户决定或授权的事项。

## Execute

- 只修改 In Scope 内容；
- 遵循 Correct → Scoped → Minimal；
- 不顺带升级无关依赖、重构无关模块或降低验收；
- 复杂任务增量实施并保留必要的命令、配置和中间证据；
- 发现 Scope 扩大、公共语义变化、L2/L3 或环境变化时停止并重新规划。

## Verify / Evaluate

验证必须逐项对应 Acceptance Criteria，可包含静态检查、单元/集成/端到端测试、运行观察、用户验收和复现。代码写完、命令返回 0 或局部测试通过不代表 COMPLETED。

依据 Verification Protocol 判断：全部强制条件通过为 COMPLETED；证据不足为 UNVERIFIED；需用户确认为 AWAITING_USER；外部依赖阻塞为 BLOCKED；主动暂停为 PAUSED；单次失败只记录 Attempt Failure。

## Delivery

下游 Agent 按状态交付 Completion Report、Reproduction Information 或 CONTINUE_PROMPT。AEWS Generator 的 `ARTIFACT_READY` 不替代这些交付。
