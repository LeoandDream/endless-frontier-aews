# Downstream Execution Workflow 通用规范

> AEWS v0.2.0 · Normative Specification

## 1. 定位

Workflow 描述下游 Execution Agent 在目标项目或研究环境中应额外关注什么。AEWS Generator 不把 Workflow 生命周期当作自己的状态，而是把适用 Workflow 约束写入 `TASK_PROMPT.md` 或目标项目 `AGENTS.md`。

Workflow 不是插件系统、注册表或运行时程序。它只能增加下游检查、验证和交付要求，不能降低用户 Goal、Scope、Acceptance 或 Verification。

## 2. Workflow 结构

每个正式 Workflow 至少说明：

| 部分 | 面向下游 Agent 的内容 |
| --- | --- |
| Metadata / Applicability | 何时应被 Generator 写入 Artifact，何时不适用 |
| Required Context | 目标项目中必须检查的文件、环境、历史或资料 |
| Research / Inspect / Understand | 需要获得和区分的事实、约束、假设与未知 |
| Plan / Execute | 计划、实施和停止要求 |
| Verify / Evaluate | 专项验证、Evidence 和状态判断 |
| Acceptance / Delivery | 额外验收和交付材料 |
| Stop / Replan | 需要停止、询问、重新规划或续接的情形 |

## 3. 生命周期归属

~~~text
AEWS Generator:
Requirement Draft → Readiness → Artifact Generation → ARTIFACT_READY

Downstream Execution Agent:
Inspect → Understand → Plan → Research / Execute → Verify → Evaluate → Deliver / Replan / Ask User / Stop
~~~

Generator 必须根据任务适用性选择 Workflow 章节。没有 Execute 阶段的 Research Prompt 仍然可以、也必须作为 Artifact 生成；对应 Execution Requirements 可省略或 `N/A`。

## 4. 优先级

适用规则按以下顺序解释：

1. 当前用户显式要求；
2. AEWS Architecture Invariants 和核心规范；
3. Artifact 中的 Goal、User Decisions、Acceptance 和 Constraints；
4. 适用的 downstream Workflow；
5. 目标项目 Source of Truth；
6. 手册、案例和工程惯例。

如果 Workflow 与核心规范或 Target Project 当前事实冲突，下游 Agent 必须停止静默执行并重新收敛。

## 5. 轻重等级

- REQUIRED：下游任务若适用则不满足不能通过其 Completion Gate；
- RECOMMENDED：应执行，无法执行时必须说明原因；
- OPTIONAL：按风险和成本选择。

## 6. 新增 Workflow

新增 Workflow 前必须确认存在真实重复需求或独立验收价值。维护 Agent 必须说明对 Generator Artifact、下游行为、验证和交付的影响。不要为每个动词、文件类型或单次项目事实创建 Workflow。
