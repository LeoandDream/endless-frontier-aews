# 评估与迭代

> AEWS v0.2.0 · Informative / System Maintenance Entry

## 评估目的

AEWS 的成功不以文件数量判断，而以两条职责清晰的链路判断：

1. Generator Quality：能否从自然语言形成 Requirement Draft、获得 Minimum Sufficient Prompt Context、正确处理 Material Unknown，并交付可靠 Instruction Artifact；
2. Downstream Execution Quality：Execution Agent 能否据 Artifact 先检查、控制范围、根据证据执行、验证、交付、复现和续接。

## 评估方法

每次评估至少选择一个真实或受控任务，检查：

- 是否默认生成与任务匹配的 Artifact，且仅在用户明确覆盖时直接回答或直接执行；
- Generator 是否止于 `ARTIFACT_READY`，没有越权完成目标项目研究或修改；
- Requirement 是否达到 `REQUIREMENT_READY`，并且 Prompt 包含必要语义；
- 下游任务是否遵循 Inspect → Understand → Plan → Research / Execute → Verify → Evaluate → Deliver；
- Completion Gate 是否有证据，非完成状态是否有可独立续接材料；
- 文档、模板、决策记录、版本记录和链接是否仍然一致。

## 版本迭代

失败、错误路由、无依据的直接执行、错误完成、无法复现和无法续接应先记录为 Failure Case，再通过 System Maintenance Workflow 评估。不要为单一案例整体重写 AEWS。
