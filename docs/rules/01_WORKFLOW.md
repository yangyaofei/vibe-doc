# 开发工作流指南 (Workflow Guidelines)

本指南定义了从需求捕捉到代码交付的全生命周期管理流程。

## 一、 核心协议 (Core Protocols)

这些协议是跨阶段通用的操作标准。

### 1.1 文档迭代协议 (Documentation Iteration Protocol)
**所有**正式文档的产出必须严格遵循以下 7 步流程：

1.  **初始化 (Setup)**:
    *   使用文档进行交流。输出主要是文档内容的总结。
    *   对于 `XXX.md` 的迭代，首先创建目录 `docs/XXX/`。
    *   将原始 `XXX.md` (如有) 复制过去，重命名为 `01_XXX.md`。
2.  **QA 启动 (Questioning)**:
    *   Agent 将问题 append 到当前文档末尾，以 `# Question` 开头。
    *   用户将以 `# Answer` 开头进行回答。
3.  **QA 循环 (Clarification)**:
    *   若沟通不够清晰，Agent 继续在 **当前文档** 中 append `# Question`。
    *   用户继续回答。
4.  **复述 (Restatement)**:
    *   若 Agent 认为清晰了，**必须对讨论内容进行复述**。
    *   形成新文档 `02_XXX.md` (编号自增)。
5.  **审计 (Audit)**:
    *   新文档形成后进入审计环节
    *   用户在当前最新文档末尾以 `# Audit` 开头追加评论。
    *   **分支 A (审计文本不充分)**: 若审计内容不清晰或不理解，Agent 回到上述 QA 环节，**在当前文档中 (不创建新文档)** append `# Question`。
    *   **分支 B (审计文本充分)**: 若审计内容清晰且 Agent 理解，形成新文档并自增编号保存。
6.  **终结 (Termination)**:
    *   流程结束标志: **有且只有** 用户明确说出“**文档合格，我们进行下一步XXX内容**”，则整个流程结束。
7.  **后处理 (Post-processing)**:
    *   **提取**: 将最终文档 (如 `05_XXX.md`) 复制到外层，替换原有正式文档。
    *   **归档**: 将中间过程文档 (含最终的 `05_XXX.md`) 归档到 `docs/archive/XXX/` 文件夹。
    *   **Handover**: 增加对应的 `docs/handovers/` 记录，用于上下文清理及下一步工作。

### 1.2 需求与状态管理 (Requirement Management)
- **Backlog**: 未进入当前 Sprint 的需求保留在 `requirement.md` 或专门的任务池中。
- **Priority**: 需求分为 P0 (阻塞级), P1 (核心功能), P2 (优化/后期)。
- **Status**: 追踪需求从 `Pending` -> `In Sprint` -> `Implemented` -> `Verified` 的全过程。
- **Reconciliation**: 每个 Sprint 结束后，必须核对计划与实际达成情况，未完成的需求重新回到池中或滚动至下个 Sprint。
- **Archive**: 文档进行更改后需要对原有文档进行 `archive`, 在 `docs/archive/requirement` 下自增的进行归档
---

## 二、 生命周期工作流 (Lifecycle Workflows)

### 阶段 1: 需求孵化 (Requirement Incubation)
- **目标**: 将模糊想法转化为明确的 `requirement.md`。
- **方法**: 使用 *文档迭代协议*。

### 阶段 2: 架构与技术设计 (Architecture & Tech Design)
- **目标**: 产出指导性的 `architecture.md` 或 `tech.md`。
- **重点**: 定义系统边界、核心技术栈、数据流向。

### 阶段 3: Sprint 迭代规划 (Sprint Planning)
- **目标**: 从 Backlog 中筛选需求，确定本次 Sprint 的范围。
- **产出**: `docs/sprints/sprint_{N}_plan.md`。
- **要求**: 遵循 `docs/rules/02_SPRINT_PROTOCOL.md`。

### 阶段 4: 任务详细设计 (Detailed Implementation Spec)
- **目标**: 在开发前，针对具体 Task 产出“拿来即用”的实现文档。
- **重点**: 消除所有技术细节的不确定性，达到“无需动脑直接编码”的程度。

### 阶段 5: 核心开发循环 (Core Dev Loop)
- **目标**: 编码实现与验证。
- **步骤**: Plan -> Analyze -> Act -> Verify -> Document (详见原 Workflow 1 描述)。

### 阶段 6: 验收与回顾 (Review & Retrospective)
- **目标**: 确认 Sprint 达成率，更新技术文档状态，进行上下文切换。

---

## 三、 核心开发循环 (Core Dev Loop - 详述)

在进入编码阶段后，必须严格遵循以下循环：

### 1. 核心流程
1.  **情境化 (Contextualize)**:
    *   阅读相关的技术文档（如 `tech.md`）和当前 Sprint 的任务计划。
2.  **风格分析 (Style Analysis)**:
    *   **检查**: 检查 `docs/prefs/` 中是否存在对应语言或框架的编码规范。
    *   **提取**: 若无规范，需分析现有代码并按照 `docs/rules/04_CODE_ANALYSIS.md` 提取风格规范。
3.  **计划 (Plan)**:
    *   在行动前，向用户输出简短的执行计划（Step 1, Step 2...）。
4.  **实施 (Implement)**:
    *   编写代码，必须严格模仿项目既有的编码风格和架构模式。
5.  **验证 (Verify)**:
    *   运行测试、执行构建脚本或通过 API 工具（如 `curl`）验证功能。**严禁在未经验证的情况下宣称任务完成。**
6.  **总结 (Summary)**:
    *   每个原子步骤完成后，创建 `docs/archive/step_{N}_abstract.md` 记录变更。
7.  **提交 (Commit)**:
    *   格式规范: `feat(scope): Description (Step N)` 或 `fix(scope): Description`。

### 2. Step Abstract 模板
```markdown
# Step {N} Summary
## 1. 变更摘要
* 简述修改了什么功能或修复了什么问题。

## 2. 关键决策
* 记录为什么选择特定的库或设计模式。

## 3. 验证结果
* [x] Build Pass
* [x] Test Pass / Verification Log
```