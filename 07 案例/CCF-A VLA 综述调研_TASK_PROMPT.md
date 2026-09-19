# TASK_PROMPT — CCF-A 会议发表的 VLA 综述调研

> 供 downstream Execution Agent 使用。此文件是研究任务指令，不是研究结果或完成声明。

## 0. Artifact Metadata

| 字段                         | 内容                                |
| -------------------------- | --------------------------------- |
| Artifact Type              | `TASK_PROMPT.md`                  |
| AEWS Version               | `v0.2.0`                          |
| Generator State            | `ARTIFACT_READY`                  |
| Target Project / Workspace | 公共学术文献与官方网页；无目标代码项目               |
| Task Type                  | Research / Literature Review      |
| Generated At               | 2026-09-19 (Asia/Shanghai)        |
| Source Requirement         | 用户请求：“调研目前 CCF-A 会有哪些发表的 VLA 综述？” |

## 1. Task and Goal

在本任务实际执行的检索截止日，系统性识别**正式发表在当日 CCF 推荐目录中 A 类国际学术会议**的、以 **Vision-Language-Action（VLA）系统/模型/智能体**为中心主题的综述（survey / review / literature review / taxonomy / overview）论文。

给出可审计的中文结论：哪些论文被严格确认符合条件；哪些看似相关但不符合“CCF-A 会议正式长文”或“VLA 专题综述”条件；以及在证据不足或严格条件下未发现论文时，应如何准确表述。不要用“没有”替代未完成的检索。

## 2. Deliverables

在最终回复中交付一份可独立阅读的 Markdown 调研报告，至少包括：

1. **结论与口径**：检索截止日、采用的 CCF 目录版本/页面、`CCF-A 会议`与`VLA 综述`的纳入规则，以及“完整性”的证据边界。
2. **已确认纳入表**：每篇论文的标题、作者、会议全称/简称、发表年份、论文类型、DOI 或 proceedings/publisher 页面、CCF-A 证明链接、该文是 VLA 综述的内容证据链接与简短依据。
3. **相关但排除/未确认表**：列出具有代表性的候选及排除原因（例如仅为 arXiv 预印本、期刊而非会议、workshop/short/demo/Findings、会议非当前 CCF-A、或只是 VLM/具身智能综述而非 VLA 专题综述）。
4. **检索覆盖与复现记录**：CCF-A 会议/领域覆盖方式、每类检索式、检索平台、访问日期、筛选计数和关键空结果。记录足以支持“在所述范围内未检出”的结论。
5. **局限与后续建议**：目录版本可能变化、索引滞后、访问受限或范围歧义等限制；若未通过所有强制验收，使用准确状态并给出可续接的下一步。

除非目标工作区的既有规则要求持久化文件，否则以最终 Markdown 报告交付即可；不要为了本任务修改无关项目文件。

## 3. Scope

### In Scope

- 截至实际检索截止日，出现在 CCF 官方**当前**推荐国际学术会议和期刊目录中的 A 类**会议**；只纳入其正式 proceedings 中的 `Full paper` 或 `Regular paper`。
- 论文的核心贡献明确是对 VLA 的文献综述、系统性回顾、分类/图谱式综述或实质性 overview。这里的 VLA 指以视觉观测和语言指令为输入、输出动作/控制/具身任务行为的 Vision-Language-Action 模型、系统或智能体；采用同义名称时必须以论文原文语境证明其等同。
- 对当前所有 CCF-A 会议目录进行可追溯覆盖，而非只搜索少数 AI/视觉会议。可优先从 AI、图形学与多媒体、交叉/综合/新兴等最可能相关领域开始，但必须记录其他领域的覆盖或合理的排除理由。
- 已有 arXiv 版本、但后来以符合条件的正式长文发表在 CCF-A 会议中的论文；证据必须来自正式论文页/论文集，而不能只凭 arXiv。

### Out of Scope

- CCF-A 期刊、非 A 类会议、仅作为 workshop、short paper、demo、technical brief、summary 或 Findings 发表的条目。
- 只有 VLA 章节或顺带提及 VLA 的 VLM、LLM、具身 AI、机器人学习或基础模型综述；这类可列入“相关但排除”表，不得混入确认结果。
- 预印本、博客、课程讲义、新闻稿或二手列表作为发表或分级的最终证据。
- 对论文方法优劣、引用量、性能、产业价值或研究方向的主观评价。

## 4. Verified Facts and Context

| Fact / Context | Source | Confidence / Limitation |
| --- | --- | --- |
| 用户要调研“目前 CCF-A 会”中发表的 VLA 综述。 | 当前用户请求 | EXPLICIT；“会”按通常语义限定为会议，不含期刊。 |
| CCF 当前官方目录按 A/B/C 分类；其对会议纳入的论文形式限定为 Full paper 或 Regular paper，并排除 short、demo、technical brief、summary、Findings 与伴随 workshop 等。 | [CCF 推荐国际学术刊物目录](https://www.ccf.org.cn/Academic_Evaluation/By_category/) | REFERENCE；下游仍须在研究日打开页面，记录当时版本与更新时间。 |
| CCF 目录会修订；“目前”必须以实际检索日的官方页面/正式版为准，而不能把历史分级当作当前事实。 | 同上 | REFERENCE；报告必须冻结检索截止日。 |
| VLA 的严格专题边界和每篇论文的发表/内容证据尚未调查。 | 未执行的下游研究 | UNKNOWN；不得预设存在、数量或“全部”结论。 |

### Context to Inspect and Source Priority

本任务无 Target Project。下游 Agent 应在公共研究环境中按以下优先级获取和保留链接：

1. **CCF 官方目录**：确认执行日的版本、A 类会议条目、会议名称/简称和论文形式规则。若目录按领域拆页，保留每个实际用来确认会议的 CCF 页面。
2. **会议主办方/出版社的 proceedings 或论文落地页**（ACM DL、IEEE Xplore、Springer、OpenReview/正式 proceedings 等）：确认会议、年份、论文类型、作者和正式发表状态。
3. **DOI/Crossref 与 DBLP**：交叉核验书目信息和会议归属；它们可用于发现，不代替前两类最终证据。
4. **论文 PDF 或官方 abstract 页面**：确认该文是否真正以 VLA 为中心并且是综述性质。搜索引擎、Google Scholar、Semantic Scholar、arXiv 仅作为发现渠道或版本线索。

## 5. User Decisions and Constraints

- 已确认：交付语言为中文；目标是调研结论而非实现代码或建立长期项目规则。
- 已按请求自然语义固定：`CCF-A 会` = **执行日当前 CCF A 类会议**，不包括 CCF-A 期刊。
- 已按严格、可复核口径固定：`VLA 综述` = VLA 为中心主题的综述论文；更宽泛的具身 AI/VLM/LLM/机器人综述只能作为相关排除项。
- 不得将本 Artifact 的 2026-09-19 生成日期误作研究完成日期；以实际检索截止日为准。

## 6. Research Requirements and Workflow

### 6.1 Inspect and Plan

1. 先打开 CCF 官方当前目录，记录版本、发布日期/更新时间、访问日，并建立当前 A 类会议清单或按领域覆盖矩阵。
2. 明确每个检索来源的可访问范围与局限；不要仅以单一搜索引擎或单一关键词给出全称结论。
3. 在报告中先写出纳入/排除判据，再开始筛选；记录每个候选的发现来源、复核来源与最终判定。

### 6.2 Search Strategy

至少组合执行下列检索，并根据观察到的新同义词扩展，但须记录扩展理由：

- 精确短语：`"vision-language-action" survey`、`"vision language action" review`、`VLA survey robotics`、`VLA review embodied AI`。
- 会议/出版社定向检索：将上述词组分别与当前 CCF-A 会议简称、论文集、DBLP 和主办方/出版社域名组合。
- 反向检索：检查高相关 VLA survey/review 的正式发表去向，再据 CCF 官方目录确认会议级别；不能从预印本标签反推发表状态。
- 近邻术语检索：`vision-language-action model/agent` 与 `survey`、`review`、`taxonomy`、`overview` 的组合，以及 VLA、视觉-语言-动作、具身/机器人控制等中英文变体。近邻结果必须通过正文/abstract 的严格 VLA 主题判定。
- 对每个可能相关的 CCF-A 领域/会议簇记录至少一个定向检索或一个可说明的系统性排除路径；对无结果的簇保留检索式和日期。

研究时将候选分为：`confirmed eligible`、`related but excluded`、`insufficient evidence`、`duplicate/version of same work`。不要把同一 work 的 preprint 与 proceedings 版本重复计数。

### 6.3 Evidence Rules

每个 `confirmed eligible` 条目必须同时满足并逐项留证：

1. **当前 CCF-A 会议证据**：官方 CCF 页面可将会议名称/简称对应为执行日 A 类会议。
2. **正式长文发表证据**：会议主办方或出版社的 proceedings/论文页确认会议、年份、作者和 Full/Regular 发表状态；必要时以 proceedings 类型或会议规则佐证。
3. **VLA 专题综述证据**：标题、abstract、关键词、引言/结构中至少有可定位的原始内容，证明它既以 VLA 为中心又具有综述/回顾/分类性质。
4. **书目信息交叉核验**：用 DOI、DBLP 或 Crossref 与官方论文页交叉检查标题、作者、年份和 venue；遇到冲突，以正式 proceedings 为准并说明。

单独命中关键词、arXiv `survey` 标签、二手榜单或“该会议通常是 CCF-A”的说法均不够。若论文实际只是在 CCF-A workshop 或 Findings 等形式发表，必须排除并提供证据。

## 7. Execution Decision Boundary

- **L0 — Autonomous**：检索公开资料、访问官方目录与数字图书馆、设计等价检索式、建立覆盖矩阵、消歧题名/版本、对事实附 URL 和访问日期。
- **L1 — Autonomous + Record**：在不改变严格纳入标准的前提下选择数据库、检索顺序、会议聚类方式和表格字段；记录选择、盲区与替代来源。
- **L2 — Ask User**：若必须改变以下任一语义才可能满足任务，应暂停并询问用户：将 CCF-A 期刊并入“会”；改按发表当年的历史 CCF 分级；将 VLM/具身 AI/机器人综述视同 VLA 专题综述；将 workshop/short/demo/Findings 或仅预印本视为正式发表；或改变报告的时间范围与“完整性”声明。
- **L3 — Explicit Authorization**：本任务不应进行破坏性操作、账号付费、绕过访问控制、批量下载受版权保护全文，或修改/删除任何项目数据。若确有必要，先获得针对该操作的用户明确授权。

## 8. Acceptance Criteria and Verification Plan

| Priority | Acceptance Criterion | Verification Method | Passing Evidence |
| --- | --- | --- | --- |
| Mandatory | 报告明确检索截止日、CCF 目录版本/页面和严格纳入规则。 | 打开 CCF 官方页并在报告逐项引用。 | 可访问的 CCF 链接、页面版本/更新时间与访问日。 |
| Mandatory | 每个确认纳入条目同时有 CCF-A、正式长文、VLA 专题综述和书目信息四类证据。 | 对每行按 6.3 的四项清单复核。 | 链接、定位依据、交叉核验结果；缺任何一项则不纳入。 |
| Mandatory | 会议全覆盖声明有审计基础，且不会只因少量关键词未命中而声称“全部”。 | 提供按 CCF 领域/会议簇的覆盖矩阵、检索式、日期和结果。 | 可复现的搜索日志与计数；若覆盖不完整则降低结论措辞。 |
| Mandatory | 相关但不符合条件的候选与已确认论文明确分开。 | 逐项应用纳入/排除规则。 | 排除原因和支持链接；不混入主表。 |
| Mandatory | 结论不夸大负面结果。 | 审查措辞是否将“未检出”限定在数据源、日期和检索策略内。 | 条件化结论与局限说明。 |
| Recommended | 关键元数据由两个独立来源核对。 | 对 publisher/proceedings 与 DOI/DBLP/Crossref 比对。 | 题名、作者、年份和 venue 一致，或冲突说明。 |

## 9. Stop / Replan Conditions

- CCF 当前目录与数据库/二手资料的分级不一致：以 CCF 官方执行日页面为准，记录差异；若“当前”与“历史发表时”分级的选择会改变结论，按 L2 询问用户。
- 找到的候选只有预印本、没有正式会议长文证据，或论文形式无法确认：转入 `insufficient evidence`，不得为了完整性计入主表。
- 访问受限、索引严重不全或无法完成足够覆盖：停止任何“全部/没有”的绝对表述，明确为 `UNVERIFIED` 或 `BLOCKED`，交付已完成覆盖和续接步骤。
- 新证据表明 VLA 定义或会议范围需要实质放宽：不得静默扩张；按 L2 询问用户。
- 出现重复版本、撤稿、标题变体或年份冲突：停止计数，先完成去重和正式版本核验。

## 10. Delivery Requirements

最终报告以以下结构为宜：

1. `检索结论（截至 YYYY-MM-DD）`：先说明是否检出严格符合项；若为零，使用“在已记录的来源和检索策略下未检出已确认条目”，不要写无条件“没有”。
2. `口径与来源`：CCF 当前目录、论文形式规则、VLA 的严格定义和检索截止日。
3. `已确认的 VLA 综述`：使用完整证据表，所有链接应直达官方 CCF 和正式论文/论文集页。
4. `相关但排除或未确认的候选`：用单独表格给出每项排除/不确定原因。
5. `检索覆盖、复现与限制`：会议/领域覆盖矩阵、检索式、数据库、查询日期、访问限制、去重规则和计数。
6. `状态`：只有所有 Mandatory 条件均有实际 Evidence 才可标为 downstream `COMPLETED`；否则准确标注 `UNVERIFIED`、`BLOCKED` 或 `AWAITING_USER`，并说明差距。

交付中保留：访问日期、所有关键 URL、数据库/检索式、筛选规则、候选计数、正式版本识别方式和已知盲区，以便另一位 Agent 复现或更新报告。

## 11. Continuation Requirements

若未完成，提供一段可直接交给后续 Agent 的续接记录：已覆盖的 CCF 领域/会议簇、已运行检索式和日期、已验证/排除/待核验候选、访问受限来源、未满足的 Acceptance Criterion、下一步优先检索路径。不得只写“继续查找”。

---

## Generator Quality Check

- [x] Artifact 为单次 Research 任务的 `TASK_PROMPT.md`，面向 downstream Execution Agent。
- [x] Goal、Deliverables、Scope、事实、未知、来源、验收、验证、决策边界、停止条件与交付已明确。
- [x] CCF 官方目录作为分级事实来源；论文与内容核验均下放给 downstream research。
- [x] 未把尚未进行的文献调研、存在性或完整性结论表示为事实。
- [x] 已区分严格符合项、相关排除项与证据不足项，避免语义降级。
- [x] Generator 状态为 `ARTIFACT_READY`；下游研究任务尚未开始，未标记为 `COMPLETED`。
