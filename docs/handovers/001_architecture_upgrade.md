# Handover Document: Architecture Upgrade

## 1. Status (当前状态)
*   **架构重构完成**: 已成功分离 "维护者模式" (Root) 和 "消费者模式" (Templates)。
*   **规则体系升级**: 
    *   引入了 `Phase 0` (需求分析)。
    *   引入了 `docs/prefs/` (偏好) 和 `04_CODE_ANALYSIS.md`。
*   **目录结构**:
    *   `vibe-doc` 现在具备了自维护的能力。
    *   `templates/main.md` 准备好供用户复制使用。

## 2. History (本次会话产出)
*   Created `README.md`: 项目总入口。
*   Created `templates/main.md`: 针对软件开发的 Prompt 模板。
*   Updated `main.md`: 针对 vibe-doc 维护的 Prompt。
*   Updated `docs/rules/00_META_RULES.md`: 增加 Lifecycle 和 Rule/Pref 定义。
*   Updated `docs/rules/01_WORKFLOW.md`: 增加 Requirement Analysis 流程。
*   Created `docs/rules/04_CODE_ANALYSIS.md`: 新增代码风格提取协议。

## 3. Next Steps (下一步计划)
*   **分析数据**: 下一步可以尝试运行 `main.md` (维护者模式)，读取 `data/` 下的参考项目，提取出第一批 `docs/prefs/` (如 `java_style.md`)，验证自维护流程。
*   **推广**: 用户可以将 `docs/rules` 和 `templates/main.md` 复制到新项目中使用。

## 4. Execution Guide (维护者指南)
*   当你作为 vibe-doc 的维护者时，切记不要执行 `rules` 里的软件开发指令（如写代码、测试）。你的工作是**编辑 Markdown**。
*   使用 `04_CODE_ANALYSIS.md` 作为工具来丰富 `docs/prefs/`。
