# TASK_PROMPT.md 模板

> AEWS v0.2.0 · Instruction Artifact Template

本模板是 Generator 输出给 downstream Execution Agent 的默认单次任务 Artifact。按适用性省略章节或填 `N/A`；不要为了填满模板编造执行要求。

~~~markdown
# Task

AEWS: v0.2.0
Artifact: TASK_PROMPT.md
Task Type: [Research / Analysis / Engineering / Debug / Integration / Experiment / Documentation / Environment / Review / Reproduction]
Artifact Status: ARTIFACT_READY
Target Role: Downstream Execution Agent

## 1. Goal

[要由下游 Agent 完成的问题、原因和期望结果。]

## 2. Deliverables

- [必须交付的代码、报告、配置、研究结论、证据或交接材料]

## 3. Current Context

[当前已知背景；明确 Generator 未执行目标任务。]

## 4. Generator Verified Facts

- [FACT：事实、来源、核验范围]
- [Target Project Context 必须由你在现场重新检查。]

## 5. User Decisions

- [已确认的材料性决定及来源]
- [无则写“无”；不得把推断写成决定]

## 6. Scope

### In Scope

- [必须处理的内容]

### Out of Scope

- [明确不处理的内容]

## 7. Constraints

- [平台、兼容性、依赖、性能、安全、时间、工作区约束]

## 8. Context to Inspect

- [AEWS Reference Context：路径 / URL / 来源权威性 / 使用目的]
- [Target Project Context：需要在真实环境中检查的文件、配置、测试、日志、数据、设备]

## 9. Research / Investigation Requirements

[适用时：研究问题、来源优先级、检索范围、证据标准、输出格式；不适用则 N/A。]

## 10. Planning / Execution Requirements

[适用时：Inspect → Understand → Plan → Research / Execute → Verify → Evaluate → Deliver 的要求；不适用则 N/A。]

## 11. Decision Boundary

- L0：[可自主处理的低风险局部事项]
- L1：[可自主选择并记录的事项]
- L2：[必须询问用户的材料性决定]
- L3：[必须获得针对性明确授权的高风险操作]

## 12. Acceptance Criteria

- [ ] [必要完成条件]

## 13. Verification Requirements

- 方法：[测试、构建、检查、观察、来源核验或用户验收]
- 通过标准：[可判断标准]
- Evidence：[日志、报告、输出位置或用户确认]

## 14. Stop / Replan Conditions

- [Material Unknown、L2/L3、Scope 扩大、关键事实冲突、验证不足或环境阻塞时的处理]

## 15. Delivery Requirements

- [最终交付、Completion Report、Reproduction Information 或 CONTINUE_PROMPT 的要求]
~~~

## 使用约束

1. Generator 不得在生成时重写 Goal、Scope、User Decisions、Acceptance 或 Verification 的真实语义。
2. `ARTIFACT_READY` 表示该 Prompt 已就绪，不表示目标任务已执行或完成。
3. 下游 Agent 必须以 Target Project 当前状态为准；Artifact 中与现场冲突的事实必须记录并重新收敛。
4. 没有 Execute 阶段的任务仍应生成 Prompt；将 Execution Requirements 省略或写 `N/A`。
