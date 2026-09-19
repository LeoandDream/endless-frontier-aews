# Decision Log

> AEWS v0.2.0 · Normative Design Record

每项决策记录 Context、Decision、Rationale、Consequences、Introduced Version 和 Status。Decision Log 记录“为什么这样设计”，不是任务执行日志。

## D-004 — L2 允许推荐但由用户决定

- Context：材料性项目选择可能有多个合理方案。
- Decision：Codex 可以分析和推荐，但最终决定权属于用户。
- Rationale：避免 AI 偷替用户决定架构、接口、模型或实验方向。
- Consequences：L2 问题必须说明选项、差异和推荐理由。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-005 — 已授权的具体 L3 操作不重复确认

- Context：高风险操作需要明确授权，但形式化重复确认会增加无效摩擦。
- Decision：用户已经明确授权具体 L3 操作时，不再重复确认同一操作。
- Rationale：保留风险边界，同时尊重已明确授权。
- Consequences：授权必须具体，普通“直接执行”不自动覆盖所有 L3 操作。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-006 — Rigorous requirement convergence

- Context：模糊需求容易导致语义降级和无效执行。
- Decision：Actionable engineering / research task 在进入 BUILD 或 EXECUTE 前必须经过 Requirement Readiness Gate；简单任务可隐式遵循结构，READY 后自动 BUILD。
- Rationale：在不要求用户填写复杂表单的情况下提高任务质量。
- Consequences：Material Unknown、关键决策或验收缺失时必须澄清或停留在非 READY 状态；Prompt 生成与执行授权分离。
- Introduced Version：v0.1.0
- Status：SUPERSEDED by D-030 / D-031

## D-007 — 项目问题重点询问，普通实现自主解决

- Context：频繁询问命名、局部拆分和工具选择会降低协作效率。
- Decision：只把影响项目目标、架构、公共接口、数据、实验和重要取舍的问题交给用户。
- Rationale：让用户拥有材料性决策，同时让 Codex 自主处理实现细节。
- Consequences：使用 Convention over Clarification。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-008 — Hybrid Context

- Context：完整复制项目会产生冗长和陈旧上下文，完全引用又可能遗漏关键语义。
- Decision：Goal、Scope、验收、约束和用户决定直接嵌入 Prompt，大型上下文引用路径并要求检查。
- Rationale：兼顾自包含性和当前状态准确性。
- Consequences：Prompt 必须同时有直接语义和 Context to Inspect。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-009 — Parent Task + Subtasks

- Context：复杂任务需要独立验收和交接，但步骤数量不等于子任务数量。
- Decision：只有有独立目标、验收、验证、依赖、失败或交接价值时拆分。
- Rationale：避免机械分解和百分比完成度。
- Consequences：Parent 状态由子任务证据和整体验收共同判断。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-010 — Intent / execution confirmation principle

- Context：BUILD、DESIGN 和 EXECUTE 的授权边界不同。
- Decision：显式 Intent 优先；actionable task READY 后自动 BUILD 并进入 PROMPT_READY；明确执行授权的 EXECUTE 不机械二次确认；没有执行授权时停在 PROMPT_READY；用户要求先确认时必须停止。
- Rationale：减少误修改和无效确认。
- Consequences：每次任务开始必须识别 Request Class / Intent，并区分 Prompt 生成与项目修改授权。
- Introduced Version：v0.1.0
- Status：SUPERSEDED by D-029 / D-031

## D-011 — Evidence-driven stop / replan

- Context：新证据可能推翻原计划。
- Decision：发现关键假设失效时停止当前分支并重新规划。
- Rationale：避免为了完成原计划而忽略事实。
- Consequences：交付中记录证据、变化和新计划。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-012 — Documentation / onboarding requirement

- Context：AEWS 需要被没有历史聊天上下文的用户和 Agent 使用。
- Decision：README、AGENTS、使用手册和维护手册是正式交付的一部分。
- Rationale：规范若不能被进入系统的人理解，就无法长期运行。
- Consequences：文档完整性是 Completion Gate 的组成部分。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-013 — Agent / User validation authority

- Context：客观测试和主观效果可能需要不同验证者。
- Decision：Agent 验证客观行为；用户或指定权威负责视觉、体验、研究结论和明确要求的人工验收。
- Rationale：避免 Agent 对不可客观判断的结果虚假宣布完成。
- Consequences：必要时使用 AWAITING_USER 或 UNVERIFIED。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-014 — No Semantic Downgrade

- Context：最低级可验证条件不一定满足用户原始目标。
- Decision：不得通过降低目标、范围或验收语义来制造完成。
- Rationale：保持用户意图和交付承诺。
- Consequences：Formal integration、usable、research conclusion 等词必须按真实边界验证。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-015 — State-Driven Delivery

- Context：成功、阻塞、暂停和待验收需要不同交付材料。
- Decision：Delivery 由 Task State 和 Completion Gate 驱动。
- Rationale：让后续 Agent 知道当前能否复现或继续。
- Consequences：每次交付必须报告状态、证据和下一步。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-016 — Canonical Task Specification → Agent Prompt

- Context：用户自然语言和执行 Prompt 之间需要稳定的逻辑结构。
- Decision：使用 CTS 组织语义，再生成 Agent-ready Prompt；不实现独立编译器。
- Rationale：保留结构化质量而不引入软件基础设施。
- Consequences：Goal、Scope、User Decisions 和 Acceptance Criteria 在构建中不得被静默修改。
- Introduced Version：v0.1.0
- Status：SUPERSEDED by D-030 / D-034

## D-017 — AGENTS.md is not independent source of truth

- Context：Agent 入口需要简洁，但完整规则分布在正式规范中。
- Decision：AGENTS.md 负责运行入口和导航，正式规范才是行为 Source of Truth。
- Rationale：避免入口文件与规范长期漂移。
- Consequences：修改核心规则时必须检查 AGENTS.md，但不把所有规则复制进去。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-018 — Documentation Completeness over File Count

- Context：大量空文件制造“完成”的假象。
- Decision：优先完成少量有实质内容的文档，逻辑上可合并，不为数量创建空文件。
- Rationale：内容和可用性优先于目录视觉完整。
- Consequences：未来扩展可以保留为明确的 Future Extension，而不是空规范。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-019R — Codex-native orchestration; no independent runtime

- Context：AEWS 的目标是可用的个人规范工作空间，不是软件产品。
- Decision：v0.1 不实现 Runtime、CLI、数据库、Registry 或 Compiler 程序。
- Rationale：先通过真实使用验证规范，再由失败驱动未来扩展。
- Consequences：Resolver、Compiler、State Machine 等只作为逻辑职责。
- Introduced Version：v0.1.0
- Status：ACTIVE

## D-020 — Actionable task 默认进入 Requirement-to-Prompt Pipeline

- Context：Blind Test 中“我如何将 NERO 接入 robosuite”被当作可独立结束的技术研究，绕过了 Requirement Draft、Readiness Gate 和 Final Prompt。
- Decision：Actionable engineering / research task 默认经过 Requirement Draft → Minimum Sufficient Context → Requirement READY → BUILD → Final Engineering Prompt → PROMPT_READY。用户不需要主动要求生成 Prompt。
- Rationale：AEWS 的核心产物是需求收敛后的可执行 Prompt；保留用户表达自然语言的入口。
- Consequences：Knowledge / Informational 和明确 discussion-only 请求仍可 DESIGN_ONLY；PROMPT_READY 不等于执行授权。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-030

## D-021 — DESIGN 是 Requirement Convergence 阶段，不是 actionable task 默认终态

- Context：v0.1.0 对 DESIGN 的研究和方案分析没有退出条件。
- Decision：DESIGN 用于探索目标、调查上下文、比较方案和解决 Material Unknown；actionable task 必须继续向 READY 推进。只有知识问答、明确 discussion-only 或用户主动终止才可 DESIGN_ONLY 结束。
- Rationale：避免技术研究被误当作需求完成。
- Consequences：DESIGN 活动必须受 Requirement Draft 和 Minimum Sufficient Context 约束。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-029 / D-032

## D-022 — Requirement READY 自动进入 BUILD

- Context：用户不应需要知道何时输入“生成 Prompt”。
- Decision：Requirement READY 后 MUST 自动 BUILD，并生成 Final Engineering Prompt。
- Rationale：恢复 Requirement-to-Prompt 主链，降低用户的 Prompt Engineering 负担。
- Consequences：BUILD 后进入 PROMPT_READY；没有执行授权时不修改项目。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-031

## D-023 — PROMPT_READY 是需求阶段默认终点

- Context：Prompt 生成、执行授权和项目修改在 v0.1.0 的边界不够显式。
- Decision：新增轻量逻辑状态 PROMPT_READY，表示 Requirement 已 READY 且 Final Engineering Prompt 已生成。
- Rationale：让用户能复制、修改、交给其他 Agent 或明确授权当前 Agent 执行。
- Consequences：PROMPT_READY 不是 COMPLETED，也不是执行授权；显式授权后才进入 EXECUTE。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-031

## D-024 — Minimum Sufficient Context

- Context：Blind Test 出现先全面扫描和研究、后建立需求的问题。
- Decision：调查只获取足以可靠完成当前 Requirement Convergence 的最小上下文；额外调查只有在可能改变 Goal、Scope、Architecture、Interface、Material Decision、Acceptance、Verification 或 Feasibility 时才继续。
- Rationale：控制调查成本，避免 Over-Investigation。
- Consequences：Token、时间、Tool Call 和外部搜索都属于调查成本。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-031

## D-025 — Progressive Context Acquisition

- Context：不同任务需要不同深度的本地和外部资料。
- Decision：按 Level 1 直接上下文、Level 2 项目资料、Level 3 关联资料、Level 4 官方资料、Level 5 广泛研究渐进获取。
- Rationale：只有前一级不足以解决 Material Unknown 时才扩大调查。
- Consequences：不得默认 Full Repo Scan + Official Research。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-031

## D-026 — Workspace Context Boundary

- Context：AEWS Workspace 中并列存在科研项目，容易发生 Context Contamination。
- Decision：将资料区分为 ACTIVE TASK CONTEXT、REFERENCE CONTEXT 和 UNRELATED WORKSPACE CONTENT；相关资料可被发现，但不会自动进入 Scope。
- Rationale：保持任务边界和事实来源清晰。
- Consequences：Reference Context 通过索引、路径或 URL 按需读取，并记录用途。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-037

## D-027 — AEWS 与真实科研项目保持 Repository Boundary

- Context：AEWS 规范与 robosuite、StarVLA、LIBERO、NERO 等真实项目的生命周期和权限不同。
- Decision：AEWS Repository 保存规范、模板、Workflow、案例、记录和 Reference Index；真实项目不默认作为 AEWS Repository 子目录。
- Rationale：避免把项目内容和规范 Source of Truth 混在一起。
- Consequences：通过 Local Path、Repository URL、Documentation URL 等地址引用项目。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-036

## D-028 — Reference Materials 使用索引而非内容复制

- Context：复制大型源码、数据集或论文会制造陈旧和边界问题。
- Decision：建立 Reference Materials 索引，记录 ID、名称、类型、位置、用途、领域、权威性、核验时间和备注。
- Rationale：优先定位可靠资料，同时保持 AEWS 仓库轻量。
- Consequences：索引是定位入口，不把被引用资料伪装成 AEWS 本地事实。
- Introduced Version：v0.1.1
- Status：SUPERSEDED by D-037

## D-029 — Generator / Execution Agent Separation

- Context：v0.1.x 将 Prompt Generator 与执行目标项目的 Agent 混为同一默认角色，导致 Generator 直接研究、设计或执行目标任务。
- Decision：AEWS 当前会话默认是 Instruction Generator；下游 Execution Agent 接收 Artifact 后在真实目标环境中执行。
- Rationale：将需求收敛与现场执行分离，避免 Generator 提前完成目标任务并混淆证据归属。
- Consequences：Generator 使用 Requirement Draft → Artifact Ready；Execution Agent 使用 Inspect → Deliver。显式用户要求才可触发当前 Agent 的角色切换。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-030 — Instruction Artifact First

- Context：Prompt 在 v0.1.x 中仍容易被理解为可选中间物，而不是 AEWS 的主要产品。
- Decision：AEWS 默认生成给另一个 Agent 使用的 Instruction Artifact，不默认交付目标任务的研究、代码或实验结果。
- Rationale：用户负责表达任务，AEWS 负责把任务说明白并约束好。
- Consequences：普通单次请求进入 `TASK_PROMPT.md`；Generator 只调查 Minimum Sufficient Prompt Context。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-031 — Prompt by Default and Artifact Readiness

- Context：用户曾需要主动说“生成 Prompt”或理解 BUILD 才能获得默认产品。
- Decision：所有普通请求在 Requirement READY 后自动生成适用 Artifact，并以 `ARTIFACT_READY` 作为 Generator 默认终点；用户可以显式覆盖为直接回答或当前 Agent 直接执行。
- Rationale：保持自然语言入口，同时不混淆 Prompt 生成与目标任务执行。
- Consequences：Requirement READY 的含义改为“可生成可靠 Artifact”；`PROMPT_READY` 是历史状态，不再作为当前默认状态。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-032 — Execution Lifecycle Belongs to Downstream Agent

- Context：DESIGN / BUILD / EXECUTE、Inspect、Verify 和 Completion 曾被作为 Generator 的混合状态。
- Decision：Research、Inspect、Understand、Plan、Execute、Verify、Evaluate、Deliver 和 Execution Completion Gate 归属 downstream Execution Agent；Generator 将适用要求写入 Artifact。
- Rationale：让 Generator 状态与目标项目证据边界一致。
- Consequences：Generator UI 只显示 Requirement Draft、Context Acquisition、Awaiting Decision、Requirement READY、ARTIFACT_READY。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-033 — Applicability-based Prompt Sections

- Context：不同任务不一定具有同样的执行章节；强制填满模板会产生虚假规则。
- Decision：TASK_PROMPT 按任务适用性包含 Research、Inspect、Plan、Execute、Verify、Delivery 等章节；不适用内容可以省略或写 `N/A`。
- Rationale：所有请求都可生成 Artifact，同时保持 Artifact 简洁和真实。
- Consequences：研究 / 知识 Prompt 不因没有 Execute 章节而跳过 Artifact Generation。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-034 — Three Core Artifact Types

- Context：单次任务、长期项目治理和任务续接需要不同的稳定输出形态。
- Decision：正式核心 Artifact 为 `TASK_PROMPT.md`、目标项目 `AGENTS.md` 和 `CONTINUE_PROMPT.md`。
- Rationale：覆盖绝大多数用户协作场景，不引入 Runtime 或复杂文件体系。
- Consequences：只选择最小足够 Artifact；长期治理与首个任务确有必要时才组合输出。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-035 — Target Project AGENTS.md Is a Formal Output

- Context：长期项目需要持续的 Execution Agent 契约，不能依赖单次 Prompt 或 AEWS 自身 AGENTS。
- Decision：用户请求长期项目 / 实验环境治理时，Generator 生成可直接放入目标项目根目录的 `AGENTS.md`。
- Rationale：把项目 Source of Truth、Decision Boundary、Execution、Verification、Delivery 和 Continuation 固化到目标环境。
- Consequences：必须明确区分 AEWS Generator AGENTS 与 Target Project AGENTS。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-036 — AEWS as an Independent Repository

- Context：AEWS 规范与真实科研 / 工程项目具有不同的权限、事实和生命周期。
- Decision：AEWS 推荐作为独立 Git Repository，保存规范、模板、案例、记录和 Reference Index；真实项目通过地址引用。
- Rationale：避免规范与业务项目相互污染。
- Consequences：不为目录美观强制重命名或迁移现有资料，但不得默认把并列业务目录作为 Artifact Scope。
- Introduced Version：v0.2.0
- Status：ACTIVE

## D-037 — Reference Index and Target Context Separation

- Context：Reference Materials 容易被误当作当前目标项目现场事实。
- Decision：Reference Index 只服务 Generator 的资料定位；Target Project Context 由 Execution Agent 在真实环境中检查。
- Rationale：保证 Artifact 的来源透明，避免历史或并列资料污染现场执行。
- Consequences：索引记录位置、用途、Use When、Authority 和核验时间；Generator 必须在 Artifact 中区分 Reference 与 Target Context。
- Introduced Version：v0.2.0
- Status：ACTIVE
