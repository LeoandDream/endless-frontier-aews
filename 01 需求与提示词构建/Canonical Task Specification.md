# Canonical Task Specification

> AEWS v0.2.0 · Canonical Instruction Source

## 1. 定位

Canonical Task Specification（CTS）是 Generator 在 Requirement Draft 与 Instruction Artifact 之间使用的逻辑信息结构。它不是目标任务的执行状态机，也不要求生成 YAML、Schema Validator 或 Prompt Compiler 程序。

CTS 的主要作用是保证 `TASK_PROMPT.md`、目标项目 `AGENTS.md` 和 `CONTINUE_PROMPT.md` 不会在生成时静默改变用户任务语义。简单任务可以隐式使用 CTS；复杂 Artifact 应显式记录完整结构。

## 2. 结构

~~~text
Canonical Instruction Specification
├── Metadata
├── Artifact Type
├── Task Interpretation
├── Goal
├── Deliverables
├── Scope
├── Constraints
├── User Decisions
├── Generator Verified Facts
├── Context Sources
│   ├── AEWS Reference Context
│   └── Target Project Context to Inspect
├── Assumptions / Unknowns
├── Downstream Workflow Profile
├── Execution Decision Boundary
├── Acceptance Criteria
├── Verification Requirements
├── Delivery Contract
└── Generator State / Artifact Status
~~~

## 3. 字段定义

### Metadata

记录标题、AEWS 版本、来源、目标项目或研究环境（如已知）和创建时间（如有必要）。Artifact 至少标记 `AEWS: v0.2.0`。

### Artifact Type

取 `TASK_PROMPT`、`PROJECT_AGENTS` 或 `CONTINUE_PROMPT`。仅当用户需要长期治理和首个任务时才取组合输出，并说明理由。

### Task Interpretation

说明用户希望下游 Agent 完成什么，不写成 Generator 自己要执行什么。可标注任务形态：Research、Analysis、Engineering、Debug、Integration、Experiment、Documentation、Environment、Review、Reproduction、Project Governance 或 Continuation。

### Goal / Deliverables / Scope / Constraints

分别描述目标、下游 Agent 应交付的结果、In Scope / Out of Scope，以及平台、兼容性、依赖、安全、性能、时间和工作区约束。不得用删减 Out of Scope 来降低原始目标。

### User Decisions

只记录用户明确选择或可靠项目约束已经决定的材料性事项。下游需现场判断的 L2/L3 内容必须写入 Execution Decision Boundary，不得伪装为已确认决定。

### Generator Verified Facts

记录由用户、Reference Context 或当前可可靠访问目标项目支持的事实，并标记来源。推断和未知不能写成事实。

### Context Sources

明确区分：

- `AEWS Reference Context`：帮助 Generator 构建 Artifact 的索引、路径或 URL；
- `Target Project Context to Inspect`：下游 Agent 在真实环境中必须检查的代码、配置、测试、日志、数据、设备或外部资料；
- `Unrelated Workspace Content`：明确不应自动纳入 Scope 的内容。

### Assumptions / Unknowns

记录允许保留的非材料性未知、需要下游 Inspect 的未知和阻止 Artifact 生成的 Material Unknown。`INFERRED + MATERIAL` 不能绕过 User Decision 或 Stop Rule。

### Downstream Workflow Profile

选择下游 Agent 适用的行动章节：Research / Investigation、Inspect、Understand、Plan、Execute、Verify、Evaluate、Delivery。无关章节可以省略或写 `N/A`。

### Execution Decision Boundary

向下游 Agent 写明 L0–L3：可自主事项、需记录事项、必须询问的 L2，以及需具体授权的 L3。

### Acceptance / Verification / Delivery

每条必要验收都要有下游验证或用户/外部权威确认方式。Delivery Contract 必须说明 Completion Report、Reproduction Information 或 Continuation Artifact 的要求。

### Generator State / Artifact Status

使用 `REQUIREMENT_DRAFT`、`CONTEXT_ACQUISITION`、`AWAITING_USER`、`REQUIREMENT_READY`、`ARTIFACT_READY`。不得使用下游 `IN_PROGRESS`、`VERIFYING`、`COMPLETED` 描述 Generator 状态。

## 4. 最小 CTS

任何准备输出的 `TASK_PROMPT.md` 至少隐式具备：

```text
Artifact Type
Task Interpretation / Goal
Deliverables
In Scope / Out of Scope
Constraints
Generator Verified Facts / Context Sources
User Decisions / Unknowns
Applicable Downstream Requirements
Acceptance / Verification
Decision Boundary
Delivery Contract
Artifact Status
```

字段不适用时必须写 `N/A` 或省略；如果缺失会改变任务语义、无法判断 Artifact 是否可靠或无法约束下游 Agent，则不得进入 `ARTIFACT_READY`。

## 5. CTS 到 Artifact 的约束

Artifact Construction 不得重写 Goal、Scope、User Decisions、Acceptance 或 Verification 的真实语义。发生冲突时，必须回到 Requirement Draft、Reference Context 或用户决策处理。

Requirement READY 后 Generator 自动生成适用 Artifact，并标记 `ARTIFACT_READY`。这不表示下游任务已经开始、已经验证或已经完成。
