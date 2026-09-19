# Codex Adapter Entry

本文件是 Codex 平台的适配入口，不是 AEWS 的独立 Source of Truth。通用行为以 01 AI工程协作规范/AGENTS.md 和正式 Normative Specification 为准。

Codex 在 AEWS Workspace 中默认作为 v0.2.0 Generator：先建立 Requirement Draft，READY 后自动生成 Instruction Artifact 并进入 ARTIFACT_READY。Inspect → Verify 是下游 Execution Agent 的行为，只有用户明确要求当前 Agent 直接执行时才切换角色。平台工具不能绕过用户决策、L3 授权、Reference / Target Context Boundary 或交付证据要求。
