# CONTINUE_PROMPT 模板

> AEWS v0.2.0 · Instruction Artifact Template  
> 用途：为已暂停、阻塞、未验证或等待用户的下游 Execution Task 提供可独立续接的指令。

~~~markdown
# Continue Task

Artifact Type: CONTINUE_PROMPT.md
AEWS Version: v0.2.0
Execution Task State: [PAUSED / BLOCKED / UNVERIFIED / AWAITING_USER / FAILED]
Originating Artifact: [TASK_PROMPT.md / Target Project AGENTS.md / other]
Target Project / Workspace: [path or identifier]

## Goal

[原始目标]

## Confirmed Scope and Decisions

- In Scope:
- Out of Scope:
- User Decisions:

## Verified Facts

- [事实、来源和限制]

## Completed Work and Evidence

- [已完成修改、产物、命令、验证和证据位置]

## Current Checkpoint

[已完成的 Execution 阶段、当前文件/环境状态及可恢复位置]

## Attempts

- [Attempt、命令或方法、结果、失败原因及是否可重复]

## Blocker / Missing Evidence / User Validation

[阻塞条件、尚缺证据，或需要用户客观确认的事项]

## Next Actions

1. [下一步]
2. [下一步]

## Recovery Conditions

[恢复所需的用户决定、环境、数据、服务、硬件或访问条件]

## Verification and Delivery Requirements

[恢复后仍须满足的 mandatory Acceptance Criteria、验证证据和交付内容]

## First Files / Commands

- [优先读取的路径、日志或安全命令]
~~~

不要写“继续之前的工作”这类无法独立使用的描述。若下游任务已通过 Completion Gate，应使用完成报告和复现材料，而不是 Continue Prompt。
