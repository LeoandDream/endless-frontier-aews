# CHANGELOG

## v0.2.0 — 2026-09-18

Status: ACTIVE / Architecture Revision

Change Classification: ARCHITECTURE + BEHAVIOR

### Changed

- Formally separated the AEWS Instruction Generator from the downstream Execution Agent.
- Made instruction artifact generation the default product behavior: `TASK_PROMPT.md` for ordinary single tasks, target-project `AGENTS.md` for long-lived governance, and `CONTINUE_PROMPT.md` for recovery.
- Replaced v0.1.x Generator state concepts `DESIGN / BUILD / EXECUTE / PROMPT_READY` with `Requirement Draft → Context Acquisition → Awaiting Decision → Requirement READY → ARTIFACT_READY`.
- Redefined Requirement READY as “enough information to generate a reliable Artifact,” not permission to execute the target task.
- Reassigned Inspect, Plan, Research, Execute, Verify, Completion, Reproduction and Delivery to downstream Execution Agent instructions.
- Made Prompt generation default for knowledge, research, analysis and simple questions unless the user explicitly requests a direct answer or direct execution.
- Added Target Project AGENTS Generation Specification, Target Project AGENTS template, specialised Reference Indexes and Generator / Execution state separation.

### Fixed

- Reclassified FC-001 as Generator / Executor Role Confusion rather than only a Requirement-to-Prompt routing defect.
- Prevented Generator deep investigation from becoming default target-task execution; introduced Minimum Sufficient Prompt Context.
- Clarified Reference Context versus Target Project Context, Artifact states versus Execution Task states, and Generator versus Execution Decision Boundaries.

### Compatibility

- v0.1.x historical decisions, Prompt states and COMPLETED records remain historical and are not silently migrated.
- D-006, D-010, D-016 and D-020 through D-028 retain their history and are marked Superseded where their semantics were replaced.
- No Runtime, CLI, Python Package, database, YAML configuration system, Workflow Engine, Prompt Compiler program, plugin architecture or Web UI was introduced.

## v0.1.1 — 2026-09-18

Status: SUPERSEDED / Historical failure-driven architecture revision

Change Classification: ARCHITECTURE + BEHAVIOR

### Fixed

- 记录并修复 FC-001：actionable task 绕过 Requirement-to-Prompt Pipeline，直接进入全面研究和 Integration Design。
- 新增 R-000：actionable engineering / research task 默认经过 Requirement Draft → Minimum Sufficient Context → Requirement READY → BUILD → Final Engineering Prompt → PROMPT_READY。
- 明确 DESIGN 是 Requirement Convergence 阶段，不是 actionable task 的默认终态；Knowledge / Informational 和明确 discussion-only 请求可以 DESIGN_ONLY 结束。
- Requirement READY 后自动 BUILD，不再要求用户主动说“生成 Prompt”。
- 新增 `PROMPT_READY` 状态，分离 Prompt 生成与执行授权。
- 新增 Minimum Sufficient Context、Progressive Context Acquisition 和 Workspace Context Boundary。
- 建立 Reference Materials 索引机制，AEWS 不默认吸收真实科研项目内容。

### Synchronized

- 同步 AGENTS、README、ARCHITECTURE、AI_USAGE_RULES、需求收敛、Decision Boundary、CTS、Prompt Construction、Workflow、Task State、使用手册、维护手册、模板和案例。
- 增加 FC-001、D-020 至 D-028 和 Requirement Pipeline Regression Test。

### Compatibility

- v0.1.0 历史任务和历史 COMPLETED 状态不静默降级。
- v0.1.1 改变未来 actionable task 的默认路由和 Prompt 生成行为；Knowledge / Informational 仍不被强制生成 Prompt。
- 不引入 Runtime、CLI、Python Package、数据库或 Web UI。

## v0.1.0 — 2026-09-18

Status: HISTORICAL / targeted completion

### Added

- AEWS README 和 Codex 运行入口 AGENTS.md。
- 系统设计、核心规则、术语、版本与兼容性规范。
- Decision Log，记录 D-004 至 D-019R。
- 通用 Workflow、通用工程任务 Workflow 和 System Maintenance Workflow。
- 执行、验证、Task State、Completion Gate、完成、复现和续接规范。
- 使用手册和开发、维护与扩展手册。
- Prompt、完成报告、快速复现、续接和 Continue Prompt 模板。
- 简单任务、复杂工程任务和未完成任务案例。
- 失败案例和改进日志入口。

### Design Constraints

- AEWS 保持 Codex-native、Markdown-first、个人自用和自然语言驱动。
- 没有创建 Python package、CLI、数据库、Web UI 或独立 Runtime。
- 空的未来扩展不被伪装成已完成规范。

### Compatibility

- 本版本不自动迁移历史 Prompt 或任务状态。
- 旧任务的历史 COMPLETED 状态不得因本版本静默降级。
- 材料性语义变化必须追加 Decision Log 和 CHANGELOG。
