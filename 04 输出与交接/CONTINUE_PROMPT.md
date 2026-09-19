# Continue Prompt 模板

> AEWS v0.2.0 · Instruction Artifact Template

将以下内容交给后续的 downstream Execution Agent。只保留已确认事实；未确认内容必须标为 Unknown 或 User Decision。

~~~markdown
# Continue Task

AEWS: v0.2.0
Artifact: CONTINUE_PROMPT.md
Target Role: Downstream Execution Agent
Execution Task State: [BLOCKED / PAUSED / UNVERIFIED / AWAITING_USER / FAILED]

## Goal

[原始目标]

## Scope

### In Scope
- [范围]

### Out of Scope
- [排除项]

## User Decisions

- [已确认决定]
- [待用户决定的问题]

## Verified Facts

- [事实与来源]

## Completed Work

- [已经完成的修改、产物和验证]

## Current Checkpoint

[下游 Agent 当前停在哪个阶段：Inspect / Understand / Plan / Research / Execute / Verify / Evaluate]

## Attempts

- [Attempt：命令、输入、结果、失败原因]

## Blocker or Missing Evidence

[阻塞、验证缺口或用户验收事项]

## Next Actions

1. [下一步]
2. [下一步]

## Recovery Conditions

[需要什么环境恢复、用户决定或输入资料]

## Verification and Delivery Requirements

[恢复后必须完成的验证、Completion Gate 和交付材料]

## First Files / Commands to Inspect

- [路径或命令]
~~~

禁止用模糊的“继续之前的工作”代替上述信息。若任务已经满足下游 Execution Completion Gate，不应生成 Continue Prompt，而应生成 Completion Report 和 Reproduction Information。Generator 生成本 Artifact 不表示任务已恢复或执行。
