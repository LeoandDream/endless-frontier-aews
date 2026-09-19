# 系统设计说明

> AEWS v0.2.0 · Normative Specification

## 1. 定位

AEWS（AI Engineering Workflow Specification）是 Codex-native、Markdown-first、natural-language-driven 的 **Instruction Artifact Generator**。用户描述想完成的事情；AEWS Generator 负责理解任务、收敛需求、获得生成可靠指令所需的最小上下文，并生成供另一个 Agent 使用的工程级指令制品。

AEWS 的默认产品不是目标任务的执行结果，而是可交给下游 Execution Agent 的 `TASK_PROMPT.md`。对于长期项目治理，默认产品可以是目标项目的 `AGENTS.md`；对于恢复中断工作，默认产品可以是 `CONTINUE_PROMPT.md`。

AEWS 不实现独立 Runtime、Prompt Compiler、State Manager、Workflow Registry、数据库、CLI 或 Web UI。Requirement Builder、Context Resolver、Decision Resolver、Readiness Gate 和 Instruction Builder 都是规范职责，不是软件模块。

## 2. Agent 角色与核心链路

~~~text
User
  ↓
AEWS Generator
  ↓
Task Interpretation
→ Requirement Draft
→ Necessary Prompt Context
→ Requirement Analysis
→ Material Unknown Detection
→ Investigate / Ask User when necessary
→ Update Requirement Draft
→ Requirement Readiness Gate
→ Instruction Artifact Generation
→ ARTIFACT_READY
  ↓
Downstream Execution Agent
  ↓
Target Project / Research Environment
  ↓
Inspect → Understand → Plan → Research / Execute → Verify → Evaluate → Deliver
~~~

Generator 与 Execution Agent 可以由不同会话、不同 Agent 或不同工作环境承担。用户明确要求“当前 AEWS Agent 直接执行”时，Generator 必须先完成或明确跳过 Artifact 生成，并显式切换到 Execution Agent 角色；这不是默认路径。

## 3. Architecture Invariants

普通局部修改不得隐式破坏以下不变量：

- A-001：Natural language is the primary user interface。
- A-002：用户不应需要 Prompt Engineering 专业知识。
- A-003：Generator 先调查能可靠获得、且生成 Artifact 所必需的上下文，再询问用户。
- A-004：改变用户目标、范围、验收或重要取舍的材料性决定属于用户。
- A-005：非材料性实现细节可以按项目约定或工程惯例写入 Execution Agent 指令。
- A-006：任务语义不得被静默削弱。
- A-007：未经验证的 Execution 结果不得表示为已验证。
- A-008：下游任务只有满足全部强制验收条件才能标为 COMPLETED。
- A-009：成功的下游任务必须保留足够复现信息。
- A-010：未完成的下游任务必须保留足够续接信息。
- A-011：Instruction Artifact 是执行表示，不是目标项目事实的唯一来源。
- A-012：平台行为不应污染通用 AEWS 规则。
- A-013：v0.x 优先采用简单的 Markdown 规范，避免不必要的软件基础设施。
- A-014：AEWS 修改必须可追溯，并解释材料性设计变化。
- A-015：**Instruction Generation First**。AEWS 默认生成给另一个 Agent 使用的工程指令，而不是直接执行用户目标。
- A-016：**Prompt by Default**。任何普通单次请求在 Requirement READY 后必须生成 `TASK_PROMPT.md`；简单问题只可缩短 Artifact，不能仅因简单绕过它。
- A-017：**Execution Separation**。Inspect、Plan、Research、Execute、Verify、Evaluate 和 Delivery 是下游 Execution Agent 的生命周期，不得作为 Generator 的默认状态机。
- A-018：Generator 只获取 Minimum Sufficient Prompt Context；若深度研究本身是目标任务，应把研究目标、来源和验证要求写入 Artifact，而非先完成研究。
- A-019：AEWS Reference Context 与 Target Project Context 必须分离；资料可被索引不等于属于当前 Artifact Scope。

## 4. 规范层级与 Source of Truth

- Normative Specification 决定系统行为，使用 MUST、MUST NOT、SHOULD、SHOULD NOT、MAY。
- Informative Documentation 负责解释、教程、模板和案例。
- 当前用户显式要求优先于正式规范；正式规范优先于项目约束、手册、案例和历史归档。
- 目标项目当前状态是下游 Execution Agent 的事实来源；Reference Index 只能帮助 Generator 定位资料，不能替代项目检查。

## 5. 组件职责

| 逻辑职责 | 规范承载 | 主要角色 |
| --- | --- | --- |
| Task Interpretation / Requirement Builder | 需求收敛规范 | Generator |
| Generator / Execution Decision Resolution | 决策边界 | 两层边界 |
| Canonical Instruction Specification | CTS 文档 | Generator |
| Instruction Artifact Construction | Prompt 构建规范和模板 | Generator |
| Target Project AGENTS Generation | Target Project AGENTS 生成规范 | Generator |
| Workflow Resolution | Workflow 规范 | Execution Agent 指令内容 |
| Execution / Verification | 执行、验证和失败处理规范 | Downstream Execution Agent |
| State / Delivery | Task State 与输出交接规范 | Generator 与 Execution Agent 分层 |
| System Maintenance | System Maintenance Workflow | AEWS 自身维护例外 |

## 6. Artifact 与 Context Boundary

核心 Artifact 的选择规则：

| 用户目标 | 默认 Artifact | 目标受众 |
| --- | --- | --- |
| 单次调研、分析、编码、Debug、集成、实验、文档、环境、Review 或复现任务 | `TASK_PROMPT.md` | Downstream Execution Agent |
| 长期项目或实验环境治理 | 目标项目 `AGENTS.md` | 进入该项目的未来 Agent |
| 恢复暂停、失败、阻塞或切换的工作 | `CONTINUE_PROMPT.md` | 后续 Execution Agent |

只有当前用户明确需要长期治理与首个任务时，才同时生成目标项目 `AGENTS.md` 和 `TASK_PROMPT.md`。不得为目录完整性制造多余 Artifact。

Context 必须分类为：

- `AEWS REFERENCE CONTEXT`：帮助 Generator 构建可靠 Artifact 的索引、路径、URL 或历史资料；
- `TARGET PROJECT CONTEXT`：Execution Agent 必须在真实环境中检查的源码、配置、测试、日志、数据和设备；
- `UNRELATED WORKSPACE CONTENT`：不因可访问而自动纳入 Scope 的并列资料。

AEWS 推荐作为独立 Git Repository，保存规范、模板、案例、决策记录、变更记录和 Reference Index。真实科研或工程项目通过路径、仓库地址或 URL 引用，不默认混入 AEWS Repository。

## 7. Execution 规范的重新归属

Decision Boundary、Inspect Before Modification、Minimal Effective Change、Incremental Execution、Verification Levels、Completion Gate、Failure Handling、Completion Report、Reproduction Guide 和 Continuation Guide 继续有效。

它们的主要作用是约束 **AEWS 生成给下游 Execution Agent 的行为要求**。Generator 需要把适用规则嵌入 Artifact，而不是默认亲自执行目标项目。

## 8. 修改本系统

修改 Core Rule、Architecture Invariant、Artifact 语义、Task State、Completion Gate 或交付契约，必须使用 System Maintenance Workflow，完成 Change Classification、Impact Analysis、Consistency Check、Decision Log、CHANGELOG 和 Version 更新。System Maintenance 是 AEWS 自身的显式维护工作，不改变 Generator / Execution Agent 的默认分离。
