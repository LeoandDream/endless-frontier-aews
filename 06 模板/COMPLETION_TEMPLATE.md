# 完成报告模板

> AEWS v0.2.0 · Downstream Execution Delivery Template

使用前提：下游 Execution Task 的 Completion Gate 已通过，所有强制 Acceptance Criteria 均有 Evidence，必要用户验收已完成。

## 状态

- Execution Task State：COMPLETED
- AEWS Version：v0.2.0
- Originating Artifact：
- Completion Gate：PASS

## Goal

[原始目标]

## Deliverables

| 交付物 | 位置 | 结果 |
| --- | --- | --- |
| [名称] | [路径] | PASS |

## 修改摘要

- [实际修改]

## Acceptance Criteria

| 条件 | 结果 | Evidence |
| --- | --- | --- |
| [条件] | PASS | [证据] |

## Verification

- 环境：
- 版本：
- 命令 / 测试：
- 实际结果：
- 证据位置：

## 用户或外部验收

- 验收者：
- 确认内容：

## 已知限制

- [限制或不在 Scope 的内容]

## Reproduction

- 复现入口：
- 输入与配置：
- 命令：
- 预期结果：

只有下游任务的所有强制条件通过时才使用 `COMPLETED`；否则使用 Continuation Guide / `CONTINUE_PROMPT.md`，并保留真实状态。
