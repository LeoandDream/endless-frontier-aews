# 失败案例

> AEWS v0.2.0 · Failure Record

## FC-001：Generator / Executor Role Confusion

- Symptom：用户输入“我如何将松灵 NERO 接入 robosuite？”或“调研目前 CCF-A 会有哪些发表的 VLA 综述”后，当前 Agent 直接完成研究、技术方案或目标任务结果，却没有把 Instruction Artifact 作为默认最终产物。
- Expected：AEWS Generator 应先构建 Requirement Draft，只获取生成可靠 Artifact 所需的上下文，处理材料性任务语义，并生成 `TASK_PROMPT.md`；目标研究、Inspect、Execute、Verify、Evidence 和 Delivery 由 downstream Execution Agent 完成。
- Root Cause：v0.1.x 将 Generator 与 Execution Agent 生命周期混在一起；DESIGN / BUILD / EXECUTE 被当作 Generator 主流程，Prompt Generation 被弱化为可选动作。
- Impact：Generator 提前执行目标任务，Token / Tool Cost 无界扩大，证据角色混淆，用户仍需主动理解何时要求 Prompt。
- Corrective Action：v0.2.0 引入 Generator / Execution Separation、Instruction Artifact First、Prompt by Default、ARTIFACT_READY、Minimum Sufficient Prompt Context、三类 Artifact 和双层 Context / Decision Boundary。
- Status：RESOLVED in v0.2.0；Test A–E required。

## F-001：把空目录视为已完成

- Symptom：目录和 Markdown 文件存在，但核心文件为空。
- Impact：用户能看到结构，却不能让 Codex 依据规范运行。
- Root Cause：以文件数量代替 Documentation Completeness。
- Corrective Action：核心文档必须有实质内容，空的未来扩展必须明确标记或移除。
- Status：RESOLVED in Stage 2。

## F-002：把“正式接入”降级为 import 成功

- Symptom：代码能够导入，但没有完成接口、运行、验证或用户验收。
- Impact：违反 No Semantic Downgrade 和 Evidence Before Completion。
- Corrective Action：澄清 Formal Integration 的边界，补齐 Acceptance Chain。
- Status：RULED by R-011 / R-012。

## F-003：把环境故障写成 FAILED

- Symptom：服务器不可用导致任务被标记为 FAILED。
- Impact：未来 Agent 丢失恢复路径。
- Corrective Action：使用 BLOCKED，保留日志、恢复条件和 Continue Prompt。
- Status：RULED by Failure Handling。

