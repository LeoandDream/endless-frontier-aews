# v0.2.0 Generator / Artifact Regression Tests

> AEWS v0.2.0 · Regression Evidence

## Test Metadata

- Trigger：FC-001 Generator / Executor Role Confusion。
- Test Mode：基于当前正式规范的行为回放、Artifact 检查和静态一致性验证；不修改真实科研项目，不引入 Runtime / CLI / Package。
- Shared Pass Rule：默认最终产物必须是适用 Instruction Artifact，除非输入含 Explicit User Override。

## Execution Record

- Executed：2026-09-19。
- Evidence Scope：Source of Truth、Artifact 模板、状态 / 交付规则、案例和内部链接的一致性检查。
- Result：Test A–E 均通过；这是 Markdown 规范级回归，不宣称已在独立目标项目中完成真实执行。

## Test A — Research Prompt

### Input

`调研目前 CCF-A 会有哪些发表的 VLA 综述`

### Expected Trace

```text
Task Interpretation → Requirement Draft → Minimum Sufficient Prompt Context
→ Requirement READY → TASK_PROMPT.md → ARTIFACT_READY
```

### Evidence and Result

- 需求收敛规范将研究请求路由到单次 `TASK_PROMPT.md`，而不是直接产出完整调研结果；
- Prompt 模板支持 Research / Investigation、来源、Verification、Delivery，并允许 Execution Requirements 为 `N/A`；
- Generator 只需确定研究目标、范围、来源优先级和输出标准，深度检索由下游 Agent 执行。

Result：`PASS`。

## Test B — Engineering Prompt

### Input

`我如何将松灵 NERO 接入 robosuite？`

### Expected Trace

```text
Task Interpretation → Requirement Draft → Necessary Prompt Context
→ Material Decision / Ask User when needed
→ Requirement READY → TASK_PROMPT.md → ARTIFACT_READY
```

### Evidence and Result

- 不默认执行接入、不将 Integration Design 作为最终产品；
- NERO 夹爪、控制接口、仿真目标和验收等材料性事项由 Generator 调查、询问或写为下游 Stop / Ask User 条件；
- 生成的工程 Prompt 对下游 Agent 的 Inspect、Plan、Execute、Verify、Delivery 有适用约束；
- 未经 Explicit User Override 不修改真实项目。

Result：`PASS`。

## Test C — Simple Question

### Input

`robosuite 支持哪些机器人？`

### Expected Trace

```text
Task Interpretation → concise Requirement Draft → TASK_PROMPT.md → ARTIFACT_READY
```

### Evidence and Result

- 简单知识问题仍默认生成简洁 Research / Answer Prompt；
- 可省略或写 `N/A` 的 Execution Requirements，不强行制造代码执行章节；
- 不因问题简单而回退到“直接回答”的旧默认分流。

Result：`PASS`。

## Test D — Explicit Override

### Input

`robosuite 支持哪些机器人？这次你直接回答，不要生成 Prompt。`

### Evidence and Result

- R-003 明确用户可以覆盖默认 Artifact Generation；
- Generator 直接回答，并说明这是 Explicit User Override；
- 不伪造 `ARTIFACT_READY`。

Result：`PASS`。

## Test E — Target Project AGENTS

### Input

`我要建立一个 robosuite + NERO 的长期实验项目，希望以后进入这个项目的 Codex 都遵循统一开发、验证和交付规范。`

### Expected Trace

```text
Project Governance Interpretation → Requirement Draft
→ Target Project AGENTS.md → ARTIFACT_READY
```

### Evidence and Result

- Artifact Routing 选择目标项目 `AGENTS.md`；
- Target Project AGENTS 生成规范要求项目目标、Context、Source of Truth、Decision Boundary、Execution、Verification、Delivery 和 Continuation；
- 规范显式区分 AEWS Generator AGENTS 与 Target Project AGENTS；
- 若用户还请求首个任务，才额外生成 `TASK_PROMPT.md`。

Result：`PASS`。

## Overall Result

`PASS`：v0.2.0 的默认主链是 `User → AEWS Generator → Instruction Artifact → Execution Agent → Target Environment`。除 Explicit User Override 外，研究、工程和简单问题都生成 Artifact；Generator 不再将下游执行结果作为默认最终产物。
