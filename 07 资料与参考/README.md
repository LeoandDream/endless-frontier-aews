# Reference Materials

> AEWS v0.2.0 · Reference Index Entry

本目录只保存供 **AEWS Generator** 定位资料的索引、路径、URL、来源类型、用途和核验信息，不默认复制大型源码仓库、数据集、论文 PDF 或真实项目全部内容到 AEWS Repository。

## Context Boundary

- `AEWS REFERENCE CONTEXT`：Generator 构建 Artifact 时可按需读取的资料，不自动扩大 Scope。
- `TARGET PROJECT CONTEXT`：由 downstream Execution Agent 在真实项目 / 研究环境中检查的代码、配置、数据、测试、日志或设备。
- `UNRELATED WORKSPACE CONTENT`：当前 Artifact 无关的并列资料，不应因可访问而读取或纳入任务。

Reference Index 只提供 Generator 的定位入口，不替代 Target Project 当前状态、用户决定或正式规范。使用资料时应在 CTS 和 Artifact 中记录来源、用途、Authority 和由谁检查。

## 资料记录字段

每条资料尽量记录：

```text
ID:
Name:
Type:
Location:
Purpose:
Use When:
Authority:
Last Verified:
Notes:
```

`Location` 可以是 Local Path、Repository Path、URL、Git Repository、Documentation URL、Paper URL 或 Dataset URL。

## 使用规则

Generator 应优先通过索引定位 Reference Context，再按 Minimum Sufficient Prompt Context 读取。发现并列机器人项目不等于它属于当前 Artifact Scope；目标项目现场事实由 Execution Agent 检查。
