# 下游 Execution Agent 执行协议

> AEWS v0.2.0 · Normative Specification

## 1. 适用范围与角色

本协议适用于获得 `TASK_PROMPT.md`、目标项目 `AGENTS.md` 或 `CONTINUE_PROMPT.md` 后，在真实 Target Project / Research Environment 中工作的 **downstream Execution Agent**。

AEWS Generator 默认只生成这些 Artifact，不进入本协议。用户明确要求当前 Generator 直接执行时，必须先明确角色切换，并以 Execution Agent 身份遵守本协议和目标项目规则。

## 2. 生命周期

~~~text
Inspect
→ Understand
→ Plan
→ Research / Execute
→ Verify
→ Evaluate
→ Deliver / Replan / Ask User / Stop
~~~

Artifact 是输入，不替代当前现场状态。执行前必须重新检查目标项目事实。

## 3. Inspect

执行或修改前必须：

- 查看目标目录、文件、调用链、配置、测试、数据、环境或设备；
- 检查当前 Git / 变更状态；
- 读取目标项目 Source of Truth、Artifact 中的 User Decisions 和 Constraints；
- 找到 Acceptance、Verification、L2 决策、L3 授权和 Material Unknown；
- 记录 Artifact 与现场事实的重大冲突。

Inspect 的目标是足够当前状态，不要求无目的扫描整个仓库。

## 4. Understand

整理 Observed Facts、Known Constraints、Expected Behavior、Actual Behavior、Relevant Components、Unknowns 和 Hypotheses。事实、推断和假设必须分开；关键假设被推翻时停止错误分支并重新规划。

## 5. Plan

计划必须与 Goal、Scope、Acceptance 和 Verification 一致，至少说明目标/非目标、受影响组件、最小有效改动或研究路径、实施顺序、中间验证点、停止/回滚/重规划条件，以及需用户决定或授权的事项。

## 6. Research / Execute

- Research 任务按 Artifact 的来源优先级、搜索范围、事实标准和交付格式进行；
- 工程任务只修改 In Scope 内容，优先 Correct → Scoped → Minimal；
- 不以执行成功代替行为验证，不降低原始需求或 Acceptance；
- 新证据、Scope 扩大、公共语义变化、L2/L3、环境变化或验证不足时停止当前分支。

## 7. Attempt

每次独立尝试记录 Attempt ID、目标、命令/配置/输入、观察结果、失败点或通过证据及其对后续计划的影响。Attempt Failure 不自动等于整个任务 FAILED。

## 8. 停止条件

必须 Replan、Ask User、Pause 或 Blocked 的情形包括：未解决 L2、未授权 L3、关键假设失效、Scope 扩大、关键依赖不可用、验证无法支持 Completion Gate，以及用户要求确认或暂停。
