# Handover Document: Meta-Rule & Prefs Refinement (Abstraction)

## 1. Status (当前状态)
*   **规则体系结构优化**: 明确了“维护者约束”与“用户规则”的边界。强化了规范的抽象化要求，禁止在公共规范中引用具体项目。

## 2. History (本次变更)
*   **Updated `main.md` (Root)**:
    *   将“增量更新/禁止删除”策略以及“抽象化与通用性（严禁项目名称）”原则均移动至此。明确这些是作为维护者的核心约束。
*   **Updated `docs/rules/00_META_RULES.md`**:
    *   彻底清理了所有维护者层面的更新策略和约束，使其纯粹作为被维护项目的元规则。
*   **Cleaned `docs/prefs/`**:
    *   重构了 Python 和 Vue 的 `.gitignore` 规范文档，移除了所有具体的项目名称引用，仅保留基于模式的描述。

## 3. Next Steps (下一步计划)
*   **审查**: 持续审查其他偏好文件，确保无残留的项目特定引用。