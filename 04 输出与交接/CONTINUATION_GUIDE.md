# 续接规范

> AEWS v0.2.0 · Normative Specification

## 1. 适用状态与角色

本规范描述 downstream Execution Agent 的续接信息。BLOCKED、PAUSED、UNVERIFIED、AWAITING_USER 和复杂 FAILED 任务必须留下 Continuation Guide；AEWS Generator 根据它生成 `CONTINUE_PROMPT.md` 供后续 Execution Agent 使用。简单任务也应在无法完成时提供最小续接信息。

## 2. 续接结构

### 当前状态

写明 Task State、AEWS 版本和状态依据。

### Goal / Scope

写明原始目标、In Scope、Out of Scope 和用户已确认决定。

### 已完成工作

列出已经修改、验证、生成或排除的内容，并给出路径和证据。

### 当前阻塞

说明阻塞发生在哪个阶段、错误或未知是什么、为什么不能继续、阻塞属于环境、需求、验证还是用户决定。

### 已尝试方法

记录 Attempt、命令、输入、输出、失败原因以及不要重复的无效路径。

### 待完成工作

按优先级列出下一步，不把猜测写成确定任务。

### 恢复条件

说明需要用户回答、服务恢复、设备可用、数据准备或其他外部条件。

### 继续入口

提供未来 Agent 首先应读取的文件、命令、日志和当前检查点。

## 3. 续接质量

未来 Execution Agent 不应依赖原始对话才能继续。若缺失关键信息，应状态化为 AWAITING_USER 或 BLOCKED，而不是自行猜测并扩大 Scope。Generator 的 `ARTIFACT_READY` 不代表这些下游工作已经完成。
