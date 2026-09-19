# 失败处理

> AEWS v0.2.0 · Normative Specification

## 1. 适用范围与失败分类

本规范主要约束 downstream Execution Agent 的目标任务失败处理。Generator 在 Artifact 构建中遇到资料或决策不足时使用 `CONTEXT_ACQUISITION`、`AWAITING_USER` 或不进入 `ARTIFACT_READY`；不得把它误标为下游任务 FAILED。

先区分：

- Attempt Failure：一次命令、方案或假设失败；
- Technical Failure：代码、测试或构建失败；
- Environment Blocker：权限、服务、依赖、设备或资源不可用；
- Requirement Blocker：目标、范围、决策或验收仍不明确；
- Validation Gap：产物存在但缺少客观或用户验证；
- Task Failure：确认无法达到目标，或用户明确终止任务。

## 2. 处理规则

1. 记录失败发生在哪个阶段和哪次 Attempt。
2. 保留命令、输入、环境、输出和错误。
3. 判断是否存在安全、可逆、最小的替代路径。
4. 如果证据推翻计划，停止错误分支并 Replan。
5. 如果阻塞依赖外部变化，使用 BLOCKED。
6. 如果用户主动暂停，使用 PAUSED。
7. 如果等待用户决定或验收，使用 AWAITING_USER。
8. 如果关键验证缺失，使用 UNVERIFIED。
9. 只有任务本身确认不能完成或明确终止时才使用 FAILED。

## 3. 续接材料

所有非 COMPLETED 结果至少留下：

- 当前 State；
- Goal、Scope 和已确认决定；
- 已完成工作；
- 已尝试方法及结果；
- 当前失败点或阻塞；
- 尚未完成任务；
- 下一步建议；
- 需要用户决定或环境变化的事项；
- 相关文件、命令、版本和输出位置。

## 4. 禁止事项

- 不把一次 Attempt Failure 写成整个任务 FAILED；
- 不把环境阻塞伪装成代码错误；
- 不把缺验证写成成功；
- 不删除失败证据；
- 不通过降低 Acceptance Criteria 逃避失败；
- 不在未解决 L2 决策时擅自选择材料性方案。
