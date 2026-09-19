# 验证与验收规范

> AEWS v0.2.0 · Normative Specification

## 1. 核心原则

本规范约束 downstream Execution Agent 的目标任务验证。AEWS Generator 的 `ARTIFACT_READY` 只表示指令已生成，不表示代码、研究或实验已完成。代码写完不等于 COMPLETED；每条强制 Acceptance Criterion 都必须有对应 Verification Requirement、实际结果和可追溯 Evidence。验证结果不足时必须使用 UNVERIFIED、AWAITING_USER、BLOCKED 或其他准确状态。

## 2. Acceptance Chain

~~~text
Acceptance Criteria
→ Verification Method
→ Actual Result
→ Evidence
→ Authority
→ Completion Gate
→ Task State
~~~

Acceptance Criteria 定义“什么算完成”；Verification 定义“如何检查”；Evidence 记录“实际发生了什么”；Authority 定义“谁有权确认”；Completion Gate 决定能否完成。

## 3. 验收来源

- Agent：客观测试、静态检查、构建、文件和命令结果。
- 用户：主观效果、视觉质量、体验、研究方向和明确要求人工确认的结果。
- 项目或外部权威：协议、合规、硬件验收、正式发布要求或实验标准。

缺少必要 Authority 时，不得用 Agent 自己的推断代替确认。

## 4. 验证层级

根据任务风险选择最小充分验证：

1. 结构验证：文件、路径、配置和产物存在且格式正确。
2. 静态验证：语法、类型、格式、链接、规则编号和文档一致性。
3. 单元验证：局部函数或组件行为。
4. 集成验证：组件之间的接口和数据流。
5. 端到端验证：真实入口、环境和完整用户路径。
6. 用户验收：必须由用户或指定权威确认的主观或领域结果。
7. 复现验证：在记录的环境、版本、命令和输入下重现结果。

低层级通过不自动代表高层级通过。用户要求正式接入时，import 成功不能代替集成验证。

## 5. Evidence 要求

Evidence 至少包含：

- 验证时间和环境；
- 使用的命令、测试或观察方式；
- 实际结果和通过标准；
- 输出位置、日志、截图、报告或用户确认；
- 未验证项、失败项和限制。

只写“已测试”“无报错”而没有方法和结果，不构成充分 Evidence。

## 6. Completion Gate

下游 Execution Agent 可以标记 COMPLETED 的条件：

- [ ] Goal 已满足；
- [ ] 所有强制 Deliverables 已产生；
- [ ] 所有强制 Acceptance Criteria 已通过；
- [ ] 每条强制条件都有实际 Evidence；
- [ ] 必要的用户或外部权威已确认；
- [ ] 没有未解决的 Material Unknown、L2 决策或关键阻塞；
- [ ] 没有发生 No Semantic Downgrade；
- [ ] 复现所需信息已记录；
- [ ] 交付报告完整。

任一条件不满足，都不得宣布 COMPLETED。

## 7. 不同结果

- 所有 Gate 通过：COMPLETED。
- 产物存在但关键验证不足：UNVERIFIED。
- 等待用户决定或验收：AWAITING_USER。
- 外部环境或依赖阻塞：BLOCKED。
- 用户主动停止当前工作：PAUSED。
- 任务目标明确无法满足且已确认终止：FAILED。
- 一次尝试失败但任务仍可继续：记录 Attempt Failure，不改变整体状态。
