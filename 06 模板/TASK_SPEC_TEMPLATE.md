# Canonical Task Specification 模板

> AEWS v0.2.0 · Generator Working Template  
> 用途：在 `REQUIREMENT_DRAFT` 到 `REQUIREMENT_READY` 期间组织任务语义；它是生成 Instruction Artifact 的输入，不是下游任务的执行授权。

## Metadata

- Title：
- AEWS Version：v0.2.0
- Source Request：
- Target Project / Workspace：
- Request Type：knowledge / research / analysis / engineering / documentation / other
- Generator State：REQUIREMENT_DRAFT / CONTEXT_ACQUISITION / AWAITING_USER / REQUIREMENT_READY / ARTIFACT_READY
- Planned Artifact：TASK_PROMPT.md / Target Project AGENTS.md / CONTINUE_PROMPT.md

## Task Interpretation

- User Goal：
- Expected Outcome：
- Why an Artifact is needed：
- Direct-answer / direct-execution override：none / explicit wording

## Scope

### In Scope

- [范围]

### Out of Scope

- [排除项]

## User Decisions and Constraints

- Confirmed decisions：
- Hard constraints：
- Material unknowns requiring a user decision：

## Verified Facts and Minimum Sufficient Prompt Context

| Fact / Context | Source | Confidence / Limitation |
| --- | --- | --- |
| [事实或上下文] | [路径、链接或用户输入] | [边界] |

### Required Target-Context Investigation

- [由下游 Execution Agent 在目标项目中自行检查的资料、代码、配置、官方文档或实验环境]

## Assumptions / Allowed Unknowns

- [允许保留的非材料性未知]
- [不得由 Generator 静默采用的材料性推断]

## Downstream Task Requirements

- Required workflow：Inspect → Understand → Plan → Research / Execute → Verify → Evaluate → Deliver
- Required deliverables：
- Mandatory Acceptance Criteria：
- Verification requirements / evidence：
- Delivery, reproduction and continuation requirements：

## Readiness Check

- [ ] Goal、范围、材料性约束和用户决策足以生成可靠 Artifact。
- [ ] 已取得 Minimum Sufficient Prompt Context，或把目标深度调查明确委派给下游 Agent。
- [ ] 未把猜测或未验证目标上下文写成事实。
- [ ] Artifact 类型与一次性任务、长期治理或任务续接相匹配。
- [ ] 若仍有 Material Unknown，状态不是 `REQUIREMENT_READY`。

用户不需要填写此模板；这是 AEWS Generator 的内部结构化工作材料。
