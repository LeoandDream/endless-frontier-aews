# 完成报告规范

> AEWS v0.2.0 · Normative Specification

## 适用条件

仅供 downstream Execution Agent 在 Execution Completion Gate 全部通过后使用。AEWS Generator 的 `ARTIFACT_READY` 不适用本报告；若仍有关键验证、用户验收、Material Unknown 或阻塞，不得使用 COMPLETED 报告格式宣布完成。

## 必备内容

### 1. 状态

- Task State：COMPLETED
- AEWS Version：v0.2.0
- Completion Gate：通过

### 2. 目标与交付

说明原始 Goal、实际 Deliverables 以及每个交付物的位置。

### 3. 修改摘要

按文件、组件或产物列出实际变化；不要把计划中的未执行内容写入此处。

### 4. 验收结果

逐项列出 Acceptance Criteria：

| 条件 | 结果 | 证据 |
| --- | --- | --- |
| [条件] | PASS | [测试、命令、报告或用户确认] |

### 5. 验证记录

记录环境、版本、命令、测试结果、观察结果和证据位置。用户验收必须标明验收者和确认内容。

### 6. 已知限制

说明未纳入 Scope 的内容、剩余风险和不影响当前完成判断的后续建议。

### 7. Reproduction

引用快速复现信息，确保未来 Agent 能按照版本、环境、命令、输入和数据位置重现结果。

### 8. 交付结论

只能使用明确结论：

- COMPLETED：全部强制条件和证据通过；
- 其他状态：改用 Continuation Guide，不得套用本报告。
