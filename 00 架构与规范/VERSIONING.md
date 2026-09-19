# 版本与兼容性

> AEWS v0.2.0 · Normative Specification

## 1. 版本规则

当前版本为 AEWS v0.2.0，状态为由 Generator / Executor Role Confusion 驱动的 Architecture Revision。Instruction Artifact、完成报告和续接材料至少标记 AEWS 版本；复杂交接材料还应记录相关规范文件和变更上下文。

v0.x 允许通过真实使用暴露问题并进行定向修订，但不允许借版本迭代悄悄降低已有任务的语义或验收标准。

## 2. 变化分类

- DOCUMENTATION：不改变行为语义的说明、导航、措辞或示例更新。
- BEHAVIOR：改变 Intent、需求、Prompt、执行、验证、状态或交付行为。
- EXTENSION：新增 Workflow、Profile、模板或适配能力，不改变既有核心语义。
- ARCHITECTURE：修改 Architecture Invariant、Source of Truth、核心结构或职责边界。Generator / Execution Separation、核心 Artifact 和状态归属的变化必须按 ARCHITECTURE 处理。

BEHAVIOR 和 ARCHITECTURE 变化必须进入 Decision Log，并在 CHANGELOG 中说明影响；EXTENSION 必须说明兼容性和是否改变默认行为。

## 3. 兼容性原则

- 历史任务应记录当时的 AEWS 版本。
- 旧任务已有的 COMPLETED 状态不得因新版本静默降级。
- 重大语义变化必须进入 CHANGELOG 和 Decision Log。
- Deprecated 行为应先说明替代方案，再在后续 Major 版本移除。
- 无法可靠迁移的历史语义不得自动猜测。
- Prompt、报告和模板可以增加字段，但不得删除仍被既有任务依赖的核心语义。

## 4. 修改流程

~~~text
Understand Current AEWS
→ Identify Change
→ Classify Change
→ Locate Source of Truth
→ Impact Analysis
→ Check Invariants
→ Modify Normative Source
→ Update Derived Docs
→ Consistency Check
→ CHANGELOG / Decision Log
→ Version
~~~

## 5. 版本状态

- DRAFT：正在设计，不能作为默认规范。
- DESIGN FREEZE：语义冻结，准备实施。
- ACTIVE：当前默认使用版本。
- DEPRECATED：仍可读取但有替代方案。
- ARCHIVED：历史记录，不再作为当前行为依据。

v0.2.0 当前标记为 ACTIVE，但只有 Repository Completion Gate 全部通过后才可对外宣称工作空间完整可用。v0.1.x 仍是历史版本；历史任务的 PROMPT_READY、ARTIFACT、COMPLETED 或交付记录不因本版本静默迁移或降级。
