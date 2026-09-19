# 变更日志

## v0.2.0 — 2026-09-18

状态：ACTIVE（架构修订）

变更分类：ARCHITECTURE + BEHAVIOR

### 已变更

- 正式分离 AEWS Instruction Generator 与下游 Execution Agent 的职责。
- 将指令制品生成确立为默认产品行为：普通单次任务使用 `TASK_PROMPT.md`，长期治理使用目标项目 `AGENTS.md`，恢复任务使用 `CONTINUE_PROMPT.md`。
- 以 `Requirement Draft → Context Acquisition → Awaiting Decision → Requirement READY → ARTIFACT_READY` 取代 v0.1.x 的 Generator 状态概念 `DESIGN / BUILD / EXECUTE / PROMPT_READY`。
- 将 Requirement READY 重新定义为“已有足够信息生成可靠 Artifact”，而非获得执行目标任务的许可。
- 将 Inspect、Plan、Research、Execute、Verify、Completion、Reproduction 和 Delivery 重新归属为下游 Execution Agent 的指令要求。
- 除非用户明确要求直接回答或直接执行，否则知识、研究、分析和简单问题也默认生成 Prompt。
- 新增 Target Project AGENTS 生成规范、Target Project AGENTS 模板、专用 Reference Index，以及 Generator / Execution 状态分离规则。

### 已修复

- 将 FC-001 重新定性为 Generator / Executor Role Confusion，而非仅是 Requirement-to-Prompt 路由缺陷。
- 防止 Generator 的深度调查默认演变为目标任务执行，并引入 Minimum Sufficient Prompt Context。
- 明确 Reference Context 与 Target Project Context、Artifact 状态与 Execution Task 状态，以及 Generator 与 Execution Decision Boundary 的区别。

### 兼容性

- v0.1.x 的历史决策、Prompt 状态和 COMPLETED 记录仍保留历史语义，不会被静默迁移。
- D-006、D-010、D-016 及 D-020 至 D-028 保留历史，并在语义被替代处标记为 Superseded。
- 未引入 Runtime、CLI、Python Package、数据库、YAML 配置系统、Workflow Engine、Prompt Compiler 程序、Plugin Architecture 或 Web UI。

## v0.1.1 — 2026-09-18

状态：SUPERSEDED（历史的失败驱动架构修订）

变更分类：ARCHITECTURE + BEHAVIOR

### 已修复

- 记录并修复 FC-001：actionable task 绕过 Requirement-to-Prompt Pipeline，直接进入全面研究和 Integration Design。
- 新增 R-000：actionable engineering / research task 默认经过 Requirement Draft → Minimum Sufficient Context → Requirement READY → BUILD → Final Engineering Prompt → PROMPT_READY。
- 明确 DESIGN 是 Requirement Convergence 阶段，不是 actionable task 的默认终态；Knowledge / Informational 和明确 discussion-only 请求可以 DESIGN_ONLY 结束。
- Requirement READY 后自动 BUILD，不再要求用户主动说“生成 Prompt”。
- 新增 `PROMPT_READY` 状态，分离 Prompt 生成与执行授权。
- 新增 Minimum Sufficient Context、Progressive Context Acquisition 和 Workspace Context Boundary。
- 建立 Reference Materials 索引机制，AEWS 不默认吸收真实科研项目内容。

### 已同步

- 同步 AGENTS、README、ARCHITECTURE、AI_USAGE_RULES、需求收敛、Decision Boundary、CTS、Prompt Construction、Workflow、Task State、使用手册、维护手册、模板和案例。
- 增加 FC-001、D-020 至 D-028 和 Requirement Pipeline Regression Test。

### 兼容性

- v0.1.0 历史任务和历史 COMPLETED 状态不静默降级。
- v0.1.1 改变未来 actionable task 的默认路由和 Prompt 生成行为；Knowledge / Informational 仍不被强制生成 Prompt。
- 不引入 Runtime、CLI、Python Package、数据库或 Web UI。

## v0.1.0 — 2026-09-18

状态：HISTORICAL（定向补全）

### 已新增

- AEWS README 和 Codex 运行入口 AGENTS.md。
- 系统设计、核心规则、术语、版本与兼容性规范。
- Decision Log，记录 D-004 至 D-019R。
- 通用 Workflow、通用工程任务 Workflow 和 System Maintenance Workflow。
- 执行、验证、Task State、Completion Gate、完成、复现和续接规范。
- 使用手册和开发、维护与扩展手册。
- Prompt、完成报告、快速复现、续接和 Continue Prompt 模板。
- 简单任务、复杂工程任务和未完成任务案例。
- 失败案例和改进日志入口。

### 设计约束

- AEWS 保持 Codex-native、Markdown-first、个人自用和自然语言驱动。
- 没有创建 Python package、CLI、数据库、Web UI 或独立 Runtime。
- 空的未来扩展不被伪装成已完成规范。

### 兼容性

- 本版本不自动迁移历史 Prompt 或任务状态。
- 旧任务的历史 COMPLETED 状态不得因本版本静默降级。
- 材料性语义变化必须追加 Decision Log 和 CHANGELOG。
