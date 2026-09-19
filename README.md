# AEWS v0.2.0

AEWS（AI Engineering Workflow Specification）是一套 Codex-native、Markdown-first、自然语言驱动的 **Instruction Artifact Generator** 规范。

用户表达想做什么；AEWS 把它整理成另一个 Agent 能可靠执行的工程级指令。AEWS 默认不替用户完成目标项目任务，也不是 Python 包、CLI、数据库、Web 服务或独立 Runtime。

## 如何开始

直接说出你希望未来 Agent 做什么，不需要先填写 Prompt、Schema 或任务表单。

例如：

- “robosuite 支持哪些机器人？”
- “调研目前 CCF-A 会有哪些发表的 VLA 综述。”
- “我如何将松灵 NERO 接入 robosuite？”
- “为我的 robosuite + NERO 实验项目建立 Agent 开发规范。”
- “根据这份中断记录，给下一个 Agent 写续接 Prompt。”

默认情况下，AEWS 会建立 Requirement Draft、调查生成可靠指令所需的最小上下文、处理必要决策，并生成 Artifact。只有你明确说“直接回答，不要生成 Prompt”“这次不用给另一个 Agent”或“当前 Agent 直接执行”时，才覆盖该默认行为。

## 核心产品与角色

| 用户需要 | 默认产物 | 给谁使用 |
| --- | --- | --- |
| 单次任务 | `TASK_PROMPT.md` | Downstream Execution Agent |
| 长期项目或实验环境规则 | 目标项目 `AGENTS.md` | 未来进入目标项目的 Agent |
| 恢复暂停、失败、阻塞或切换的工作 | `CONTINUE_PROMPT.md` | 后续 Execution Agent |

~~~text
User
→ AEWS Generator
→ Instruction Artifact
→ Execution Agent
→ Target Project / Research Environment
→ Evidence / Delivery
~~~

Generator 的状态只有 `Requirement Draft`、`Context Acquisition`、`Awaiting Decision`、`Requirement READY` 和 `ARTIFACT_READY`。下游 Agent 才执行 Inspect、Plan、Research、Execute、Verify、Evaluate 和 Deliver。

## 默认工作链路

~~~text
Natural Language Request
→ Task Interpretation
→ Requirement Draft
→ Necessary Prompt Context
→ Requirement Analysis
→ Material Unknown Detection
→ Investigate / Ask User when necessary
→ Update Requirement Draft
→ Requirement Readiness Gate
→ Instruction Artifact Generation
→ ARTIFACT_READY
→（由下游 Execution Agent）Inspect → Understand → Plan → Research / Execute → Verify → Deliver
~~~

Requirement READY 的意思是“可以生成可靠 Artifact”，不是“AEWS 可以开始执行目标任务”。

## 文档导航

- [AGENTS.md](AGENTS.md)：AEWS Generator 运行入口。
- [系统设计说明](00%20架构与规范/ARCHITECTURE.md)：角色分离、核心链路和 Architecture Invariants。
- [核心规则](00%20架构与规范/AI_USAGE_RULES.md)：Instruction Artifact First、Prompt by Default、Context Boundary 等规则。
- [需求收敛规范](01%20需求与提示词构建/需求收敛规范.md)：Generator 的 Task Interpretation、Draft、Readiness 与 Artifact 路由。
- [Canonical Task Specification](01%20需求与提示词构建/Canonical%20Task%20Specification.md)：Artifact 的逻辑信息源。
- [Instruction Artifact 构建规范](01%20需求与提示词构建/Prompt%20构建规范.md)：TASK_PROMPT、目标项目 AGENTS、CONTINUE_PROMPT 的构建规则。
- [Target Project AGENTS 生成规范](01%20需求与提示词构建/Target%20Project%20AGENTS%20生成规范.md)：目标项目长期 Agent 契约。
- [Workflow 通用规范](02%20任务工作流/Workflow%20通用规范.md)：下游 Agent Workflow 约束。
- [执行与验证](03%20执行与验证/)：下游 Execution Agent 的执行、验证、状态和失败处理要求。
- [输出与交接](04%20输出与交接/)：下游 Delivery、复现和续接结构。
- [使用手册](05%20使用手册/使用手册.md)：面向用户的 Artifact 使用说明。
- [开发、维护与扩展手册](06%20开发维护与扩展/开发、维护与扩展手册.md)：AEWS 的架构维护入口。
- [模板](06%20模板/)：TASK_PROMPT、目标项目 AGENTS、续接和交付模板。
- [资料与参考](07%20资料与参考/)：Reference Index 与 Context Boundary。
- [案例](07%20案例/)：Generator 输出与下游执行案例。
- [评估与迭代](08%20评估与迭代/)：Failure Case、回归测试和改进记录。
- [CHANGELOG.md](CHANGELOG.md)：版本变化。

## 重要边界

- AEWS Reference Context 不等于 Target Project Context。
- 相关资料存在于 Workspace，不等于当前 Artifact Scope。
- Prompt / Artifact 生成不等于目标项目执行授权。
- `ARTIFACT_READY` 不等于 `COMPLETED`。
- 目标项目 `AGENTS.md` 与 AEWS Generator 的 `AGENTS.md` 必须分开。
- 修改 AEWS 自身必须使用 System Maintenance Workflow。
