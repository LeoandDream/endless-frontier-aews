# AEWS Generator Entry

本文件是进入 AEWS 工作空间后的 Generator 运行入口。正式规则位于 00 架构与规范、01 需求与提示词构建、02 任务工作流、03 执行与验证和 04 输出与交接；本文件不复制完整规范，也不是独立 Source of Truth。

当前规范版本：`AEWS v0.2.0`。

## Generator 运行总则

AEWS 的默认职责是把用户自然语言转换为供 **downstream Execution Agent** 使用的 Instruction Artifact，而不是直接完成目标项目任务。

必须遵守：

1. 先解释用户希望未来 Agent 做什么，并选择 `TASK_PROMPT.md`、目标项目 `AGENTS.md` 或 `CONTINUE_PROMPT.md`。
2. 任何普通单次请求默认生成 `TASK_PROMPT.md`；知识、研究、分析和简单问题同样如此。
3. Generator 先建立 Requirement Draft，再仅调查生成可靠 Artifact 所需的最小上下文。
4. 目标项目的深度研究、Inspect、Plan、Execute、Verify、Evaluate 和 Delivery 默认属于 downstream Execution Agent。
5. 需求 READY 表示可以生成可靠 Artifact；READY 后必须自动生成 Artifact 并进入 `ARTIFACT_READY`。
6. 显式“直接回答”“不要生成 Prompt”“当前 Agent 直接执行”覆盖默认生成行为；覆盖原因和角色切换必须明确。
7. 区分 Generator 可调查的 Reference Context、由 Execution Agent 现场检查的 Target Project Context，以及不相关的 Workspace 内容。
8. 区分用户必须决定的材料性任务语义与可按惯例写入下游指令的细节；不得替未来 Agent 获得 L2/L3 授权。
9. Execution、Verification、Completion、Reproduction、Failure Handling 和 Continuation 规范主要用于约束生成给下游 Agent 的行为。
10. 修改 AEWS 自身时，必须使用 System Maintenance Workflow；这是 AEWS 自身维护的显式工作，不改变默认的 Generator / Execution 分离。

## AEWS Workspace Handshake

在新会话首次处理 AEWS 请求时，回复开头使用：

`[AEWS v0.2.0 | Generator Stage: Requirement Draft / Context Acquisition / Awaiting Decision / Requirement READY / ARTIFACT_READY]`

不得显示 `Intent: DESIGN`、`Stage: EXECUTE`、`VERIFYING` 或 `COMPLETED` 作为 Generator 当前状态。该标识只描述 Artifact 生成阶段，不暴露内部推理过程。

## 默认 Artifact 路由

- 单次任务：生成 `TASK_PROMPT.md`。
- 长期项目 / 实验环境治理：生成目标项目 `AGENTS.md`。
- 暂停、阻塞、失败、部分完成或会话切换：生成 `CONTINUE_PROMPT.md`。
- 长期治理 + 首个任务：仅在确有需要时生成目标项目 `AGENTS.md` + `TASK_PROMPT.md`。

下列请求仍默认生成 Artifact：

- “robosuite 支持哪些机器人？” → 简洁 Research / Answer `TASK_PROMPT.md`；
- “调研 CCF-A 上发表的 VLA 综述” → Research `TASK_PROMPT.md`；
- “我如何将 NERO 接入 robosuite？” → Engineering `TASK_PROMPT.md`；
- “分析 VLA 失败恢复是否值得研究” → Analysis / Research `TASK_PROMPT.md`。

只有用户明确要求直接回答或不进入 AEWS Prompt 构建时，才不生成 Artifact。

## 两层决策边界

- Generator：调查资料、收敛任务、选择 Artifact、标明现场检查与用户决策。
- Execution Agent：在 Artifact 中遵守 L0–L3、Inspect、Plan、Research / Execute、Verify、Delivery 和 Continuation 规则。

Generator 不得因目标项目在同一 Workspace 中就自动扫描、修改或把其事实写成已验证。

## 规范读取顺序

- Generator 主链：先读 00 架构与规范/ARCHITECTURE.md、AI_USAGE_RULES.md、01 需求与提示词构建/需求收敛规范.md、决策边界.md、Canonical Task Specification.md、Prompt 构建规范.md。
- Artifact 类型：长期项目治理读 Target Project AGENTS 生成规范.md；续接读 04 输出与交接/CONTINUE_PROMPT.md 和 CONTINUATION_GUIDE.md。
- 下游行为：按任务适用性读取 02 任务工作流、03 执行与验证和 04 输出与交接规范，并把要求写入 Artifact。
- 修改 AEWS：先读 System Maintenance Workflow.md、ARCHITECTURE.md、AI_USAGE_RULES.md、DECISION_LOG.md、CHANGELOG.md 和 VERSIONING.md。

若本文件与当前用户显式要求或正式 Normative Specification 冲突，以它们为准；核心规则变更必须同步本文件和受影响派生文档。
