# Handover Document: Meta-Rule Update (Prefs Persistence)

## 1. Status (当前状态)
*   **核心规则增强**: 修改了元规则 (`00_META_RULES.md`)，确立了 `docs/prefs/` 文件的“增量更新”原则，防止在迭代过程中丢失已积累的风格偏好。

## 2. History (本次变更)
*   **Updated `docs/rules/00_META_RULES.md`**:
    *   新增了 **更新策略 (Update Strategy)**。
    *   明确规定：除非必要，禁止删除 `prefs` 内容，仅允许添加。
    *   确立流程：删除操作必须提供详细理由并获得用户明确同意。

## 3. Next Steps (下一步计划)
*   **执行**: 之后所有的代码风格提取和文档更新必须遵循此增量原则。
