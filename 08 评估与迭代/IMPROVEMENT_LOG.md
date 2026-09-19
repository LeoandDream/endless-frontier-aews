# 改进日志

> AEWS v0.2.0 · Maintenance Record

## 2026-09-18：第二阶段内容补全

- 观察：第一次实施生成了大量空 Markdown，只有 01 需求与提示词构建有实质内容。
- 影响：README、AGENTS、执行、交付、手册和案例无法独立使用。
- 改进：补齐 Core Documentation、Workflow、执行验证、Delivery、手册、模板和案例。
- 维护原则：优先内容完整性，不以文件数量或空目录制造完成感。
- 版本：AEWS v0.1.0
- 状态：已补全，待 Repository Completion Gate 验证。

## 2026-09-18：FC-001 Requirement-to-Prompt Pipeline 修复

- 触发任务：第一次真实 Blind Test，输入“我如何将松灵 NERO 接入 robosuite 呢？”。
- 观察：Agent 直接调查和形成 Integration Design，没有建立可见 Requirement Draft，也没有自动进入 BUILD 和 Final Prompt。
- 根因：DESIGN 可独立终止、actionable task 默认路由缺失、Requirement Draft 不强制先于深度调查、没有明确 PROMPT_READY 状态和 Context Boundary。
- 改动范围：核心架构、AI_USAGE_RULES、需求收敛、Decision Boundary、CTS、Prompt Construction、Workflow、Task State、入口、手册、Reference Materials、Failure Case、Decision Log、CHANGELOG 和回归测试。
- 验证：原始 Blind Test 回归路径必须达到 Requirement Draft、Minimum Sufficient Context、Requirement READY、BUILD、PROMPT_READY，并保持无执行授权时不修改真实项目。
- 版本：AEWS v0.1.1。
- 状态：已实施，待最终 Completion Gate。

## 2026-09-18：v0.2.0 Generator / Execution Architecture Revision

- 触发任务：FC-001 的进一步 Blind Test 根因分析。
- 观察：即使 v0.1.1 恢复了 Requirement-to-Prompt 链，当前 Agent 仍被规范描述为可默认进入下游执行生命周期，导致 Generator 与 Execution Agent 混淆。
- 根因：Instruction Generation 没有被定义为唯一默认产品；DESIGN / BUILD / EXECUTE 与 Inspect / Verify 同时出现在 Generator 主链和下游任务语义中。
- 改动范围：Architecture、Core Rules、AGENTS、Requirement、Decision Boundary、CTS、Artifact Construction、Target Project AGENTS、Workflow、Execution / Verification / State / Delivery、Reference Index、手册、模板、案例、Decision Log、CHANGELOG、Versioning 和 Test A–E。
- 验证：Test A–E 必须证明研究、工程、简单问题、显式覆盖和长期项目治理均符合 Artifact First；不修改真实目标项目。
- 版本：AEWS v0.2.0。
- 状态：已实施；Test A–E、文档完整性和内部链接检查通过。

## 后续记录格式

每条改进记录包含日期、触发任务、观察到的摩擦或失败、影响、根因、改动范围、验证、版本和状态。材料性规则变化必须同步 Decision Log 和 CHANGELOG。
