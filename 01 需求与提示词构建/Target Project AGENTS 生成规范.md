# Target Project AGENTS 生成规范

> AEWS v0.2.0 · Normative Specification

## 1. 目的

本规范定义 AEWS Generator 如何生成可直接放入 **目标项目根目录** 的 `AGENTS.md`。该文件是长期 Project Governance Artifact，约束未来进入目标项目的 Execution Agent；它不是 AEWS Repository 的 `AGENTS.md`，不约束 AEWS Generator。

## 2. 适用条件

当用户需要长期项目、实验环境、代码库或研究项目的统一开发、调研、验证、交付和续接规则时，Generator 必须输出 Target Project `AGENTS.md`。

如果用户同时需要治理规则和首个任务，应输出：

```text
Target Project / AGENTS.md
+
TASK_PROMPT.md
```

除非有长期治理需要，不要用 Target Project AGENTS 代替单次 TASK_PROMPT。

## 3. 必备内容

Target Project `AGENTS.md` 至少包含：

1. Project Goal 与明确边界；
2. Project Context、目录、关键组件、环境和 Source of Truth；
3. Context Sources 与资料权威性；
4. Coding / Research / Experiment Rules（按适用性）；
5. Inspect、Understand、Plan、Research / Execute 的期望；
6. L0–L3 Decision Boundary 与授权规则；
7. Verification、Evidence、Acceptance 与 Completion Gate；
8. Failure Handling、BLOCKED / PAUSED / UNVERIFIED 语义；
9. Delivery、Reproduction、Continuation；
10. 与 AEWS Generator 和 Reference Materials 的边界说明。

不适用部分可以省略或写 `N/A`，但不能用空标题替代规则。

## 4. 生成约束

- Generator 只能写入已确认的项目事实或明确的现场检查要求；
- 不得把 AEWS Reference Index 中的内容直接当作目标项目当前事实；
- 不得静默规定项目级 L2 选择；
- 必须明确哪些路径、配置、测试、日志、硬件或外部资料由 Execution Agent 在现场检查；
- 不得复制 AEWS Generator 自身 AGENTS 的全部内容，也不得让目标项目 AGENTS 重新定义 AEWS 核心架构。

## 5. 交付与状态

Generator 输出 Target Project `AGENTS.md` 后标记 `ARTIFACT_READY`。这仅表示长期项目规范已生成，不表示项目已经配置、代码已经实现或验证已完成。

使用 [TARGET_PROJECT_AGENTS_TEMPLATE.md](../06%20模板/TARGET_PROJECT_AGENTS_TEMPLATE.md) 作为结构起点，并根据目标项目裁剪。
