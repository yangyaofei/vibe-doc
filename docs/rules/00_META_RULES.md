# 项目核心元规则 (Project Meta-Rules)

## 1. 项目生命周期 (Lifecycle Phases)
所有项目必须经历明确的阶段流转：

*   **Phase 0: 构想与定义 (Inception)**
    *   **输入**: 模糊的用户意图。
    *   **活动**: 需求分析、澄清问题、边界定义。
    *   **产出**: `docs/requirement.md` (初稿) -> `docs/requirement_detail.md` (定稿)。
*   **Phase 1: 架构与选型 (Architecture)**
    *   **输入**: `requirement_detail.md`。
    *   **活动**: 技术选型、系统设计、关键决策。
    *   **产出**: `docs/tech.md` (唯一事实来源)。
*   **Phase 2: 构建与迭代 (Construction)**
    *   **输入**: `tech.md`。
    *   **活动**: Sprint 迭代开发 (Sprint Planning -> Execution -> Closing)。
    *   **产出**: 代码变更、测试报告、`docs/archive/step_*.md`。

## 2. 规则体系 (Rule System)

### A. 强制规则 (Rules) - `docs/rules/`
*   **性质**: 宪法。必须严格遵守，不可违背。
*   **适用**: 工作流程、文档格式、交接协议。

### B. 风格偏好 (Preferences) - `docs/prefs/`
*   **性质**: 习惯法。默认遵守，但允许根据具体情况调整。
*   **来源**: 
    1.  用户明确指定。
    2.  Agent 通过 `04_CODE_ANALYSIS.md` 从现有代码中提取。
*   **适用**: 代码风格 (Naming, Formatting)、框架惯用写法、目录结构。

## 3. 核心原则
1.  **文档驱动 (Doc-Driven)**: 
    *   Phase 0/1 必须产出文档才能进入下一阶段。
    *   Phase 2 必须先有 Plan 文档才能写代码。
2.  **上下文连续性**: 
    *   必须通过 `03_HANDOVER_PROTOCOL.md` 保证记忆传递。
3.  **风格一致性**: 
    *   在写代码前，必须先查阅 `docs/prefs/`。如果为空，必须先执行分析。

