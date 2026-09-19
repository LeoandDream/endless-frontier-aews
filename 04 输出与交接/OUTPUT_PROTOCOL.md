# Delivery Protocol

> AEWS v0.2.0 · Normative Specification

## 1. 两层交付

AEWS v0.2.0 区分 Generator Artifact Delivery 与 downstream Execution Delivery。

- Generator 的默认交付是可靠的 Instruction Artifact，状态为 `ARTIFACT_READY`；
- Execution Agent 的交付是目标任务的结果、Evidence、Completion / Reproduction / Continuation 材料。

Generator 不得将 Artifact 交付写成目标任务已完成。

## 2. Generator Artifact Delivery

### ARTIFACT_READY

必须提供：

1. Artifact 类型和文件名：`TASK_PROMPT.md`、目标项目 `AGENTS.md` 或 `CONTINUE_PROMPT.md`；
2. Artifact 正文或明确可复制内容；
3. Requirement READY / Artifact Gate 的简要依据；
4. 已使用的 Reference Context、下游需现场检查的 Target Project Context；
5. 未解决但已正确下放的 Stop / Ask User 条件；
6. 明确说明 Generator 未执行目标项目任务，除非用户显式覆盖。

## 3. Downstream Execution Delivery

### COMPLETED

必须提供：

- Completion Report；
- 强制 Acceptance Criteria 逐项结果；
- 验证 Evidence；
- 环境、版本、命令、输入输出和复现方式；
- 已知限制和后续可选工作。

### UNVERIFIED / AWAITING_USER

必须说明缺失的证据或用户确认、可观察结果、确认方式和当前不可宣称的内容。

### BLOCKED / PAUSED / FAILED

必须提供 Continuation Guide；复杂任务还应提供 `CONTINUE_PROMPT.md`。说明已完成工作、阻塞/失败点、下一步、恢复条件和禁止重复的尝试。

## 4. 状态约束

- Generator 只有通过 Artifact Gate 才可写 `ARTIFACT_READY`。
- 下游没有通过 Execution Completion Gate 不得使用 COMPLETED。
- 不得把计划、Prompt 或 Generator 推断写成下游已完成事实。
- Delivery 的范围必须与用户请求、CTS 和目标项目现场事实一致。
