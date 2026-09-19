# System Maintenance Workflow

> AEWS v0.2.0 · ACTIVE · REQUIRED for AEWS changes

## 目的

修改 AEWS 自身时，不能像修改普通项目文件一样随意编辑一个规范。必须先理解当前系统、定位 Source of Truth、评估影响，再同步派生文档、版本和决策记录。

## 维护链路

~~~text
Understand Current AEWS
→ Identify Change
→ Classify Change
→ Locate Source of Truth
→ Impact Analysis
→ Check Architecture Invariants
→ Modify Normative Specification
→ Update Derived Documentation
→ Consistency Check
→ CHANGELOG / Decision Log
→ Version
~~~

## 1. Understand Current AEWS

阅读根级 AGENTS、README、系统设计、核心规则、相关规范、CHANGELOG 和 Decision Log。检查当前目录、文档实际内容、链接、版本、未提交变更和历史状态。不能只看文件名判断系统是否存在某项能力。

## 2. Identify Change

明确用户真正要求改变的目标、预期行为、交付物、范围、排除项和验收条件。区分 Documentation、Behavior、Extension 和 Architecture 变化。

## 3. Classify Change

- DOCUMENTATION：不改变行为语义的说明、导航、措辞、格式和示例。
- BEHAVIOR：改变 Intent、需求、Prompt、执行、验证、状态或交付行为。
- EXTENSION：新增 Workflow、Profile、模板或平台适配，不改变默认核心语义。
- ARCHITECTURE：改变 Invariant、Source of Truth、核心职责边界或系统结构。

无法确定时按可能影响更大的类别分析，不得把材料性变化伪装成 Documentation。

## 4. Locate Source of Truth

优先顺序：

1. 当前用户显式要求；
2. 当前任务中用户确认的决定；
3. 正式 Normative Specification；
4. 当前实际项目状态；
5. 派生手册、模板和案例；
6. 历史材料和 AI 推断。

AGENTS 是运行入口，不是独立 Source of Truth。案例不能覆盖正式规范；模板不得偷偷改写验收语义。

## 5. Impact Analysis

至少检查：

- Architecture Invariants；
- Generator / Execution Separation、Artifact Routing、Requirement READY 和 ARTIFACT_READY；
- Generator / Execution Decision Boundary、Reference Context 和 Target Project Context；
- CTS 与 Prompt 模板；
- Workflow 和执行协议；
- Verification、Completion Gate 和 Task State；
- Delivery、Reproduction、Continuation；
- AGENTS、README、手册、模板、案例；
- CHANGELOG、Decision Log 和版本兼容性。

## 6. 修改与同步

先修改 Normative Source，再更新依赖它的派生文档。每个受影响文档都必须检查术语、状态、规则编号、链接和验收语义。不得整体重写无关文档。

## 7. 一致性检查

必须验证：

- 自然语言到交付的链路没有断点；
- Generator 状态没有与 downstream Execution lifecycle 混同；
- TASK_PROMPT、目标项目 AGENTS 和 CONTINUE_PROMPT 的默认路由一致；
- User Decision 与 Autonomous Implementation 边界一致；
- Completion Gate 与状态交付一致；
- 成功可复现，未完成可续接；
- README 和 AGENTS 的导航指向真实文件；
- 没有把未验证结果写成 COMPLETED；
- 没有通过降低验收标准制造完成。

## 8. 记录与版本

BEHAVIOR、EXTENSION 或 ARCHITECTURE 变化必须更新 CHANGELOG；材料性设计变化还必须更新 Decision Log。记录变化类别、影响、兼容性和验证结果。按 VERSIONING 决定版本变化，不得无理由整体重写或跳过记录。

## 9. Maintenance Checklist

- [ ] 当前 AEWS 已理解
- [ ] Change Classification 已完成
- [ ] Source of Truth 已定位
- [ ] Impact Analysis 已完成
- [ ] Architecture Invariants 已检查
- [ ] Normative Source 已修改
- [ ] 派生文档已同步
- [ ] 链接和术语已检查
- [ ] CHANGELOG / Decision Log 已更新
- [ ] Repository Completion Gate 已重新执行

## 10. Repository Completion Gate

每次 AEWS 的 BEHAVIOR、EXTENSION 或 ARCHITECTURE 维护完成前，维护者必须以当前修改范围重新检查：

- [ ] Source of Truth、AGENTS、README 和所有受影响的 Normative Specification 一致；
- [ ] Generator / Execution Agent 的职责、状态和 Artifact Routing 没有混同；
- [ ] Requirement READY、`ARTIFACT_READY`、Execution Completion Gate 和非完成状态的语义一致；
- [ ] CTS、`TASK_PROMPT.md`、目标项目 `AGENTS.md`、`CONTINUE_PROMPT.md` 及模板具有所需语义；
- [ ] Workflow、Execution、Verification、Failure Handling、Delivery、Reproduction 和 Continuation 的角色归属一致；
- [ ] Reference Context、Target Project Context 与无关 Workspace 内容的边界清晰；
- [ ] 决策、CHANGELOG、版本和兼容性记录完整，历史记录未被静默改写；
- [ ] 受影响的案例和回归测试已记录真实结果；
- [ ] Markdown 文件、内部链接和目录入口存在且可访问；
- [ ] 未引入与本次范围无关的 Runtime、CLI、Package、数据库、YAML 配置系统、Workflow Engine、Prompt Compiler、Plugin Architecture 或 Web UI；
- [ ] 没有以降低 Goal、Scope、Acceptance 或 Evidence 要求的方式制造通过。

此 Gate 是 AEWS 维护任务的完成条件；它不能取代下游 Execution Task 的 Completion Gate。
