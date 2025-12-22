# Vibe-Doc: AI-Native Development Framework

**Vibe-Doc** 是一个为 AI Agent (如 Gemini, Claude, ChatGPT) 设计的标准化上下文框架。它的目的是让 AI 在接手软件项目时，能够遵循一套严谨的、可预测的工程流，从而实现高质量的代码交付和自我维护。

## 📂 目录结构 (Directory Structure)

### 核心交付物 (The Product)
这些文件是**最终用户**会复制到自己项目中的内容：

*   **`docs/rules/` (宪法)**: 强制性执行规范。
    *   `00_META_RULES.md`: 项目的元规则，定义了生命周期和优先级。
    *   `01_WORKFLOW.md`: 包含了需求分析、架构设计、代码实现的具体工作流。
    *   `02_SPRING_PROTOCOL.md`: 定义了迭代（Sprint）管理的标准。
    *   `03_HANDOVER_PROTOCOL.md`: 定义了上下文交接的标准。
    *   `04_CODE_ANALYSIS.md`: 定义了如何分析现有代码并提取风格偏好的协议。
*   **`docs/prefs/` (习惯法)**: 可选的、经验性的偏好设置。
    *   存放针对特定语言（Java, Vue）、框架（Spring Boot, Nuxt）或架构模式的代码风格定义。
    *   这些文件通常由 Agent 分析现有代码后自动生成。
*   **`templates/main.md`**: 用户将其复制到自己项目根目录的 Prompt 入口。

### 本项目维护 (Internal Maintenance)
这些文件用于维护 `vibe-doc` 本身：

*   **`main.md` (Root)**: 本项目的维护者入口。它指导 Agent 如何更新规则文档，而不是写代码。
*   **`docs/handovers/`**: 记录 `vibe-doc` 自身的变更历史。
*   **`data/`**: 存放参考项目（原始素材），用于提取最佳实践并沉淀到 `docs/prefs/` 中。

## 🚀 如何使用 (How to Use)

### 场景 A: 在你的新项目中使用 Vibe-Doc
1.  将 `docs/rules/`, `docs/prefs/` (可选), `docs/handovers/` (空文件夹) 复制到你的项目根目录 `docs/` 下。
2.  将 `templates/main.md` 复制到你的项目根目录，重命名为 `main.md` (或其他你喜欢的 Prompt 文件名)。
3.  (可选) 将你现有的核心代码放入 `src/`。
4.  将 `main.md` 的内容发送给 AI Agent。

### 场景 B: 维护/更新 Vibe-Doc 本身
1.  确保你处于 `vibe-doc` 仓库根目录。
2.  将根目录下的 `main.md` 发送给 AI Agent。
3.  下达指令（例如：“分析 data/XXX 的代码风格并更新 prefs”，或“修改 01_WORKFLOW 增加测试环节”）。

## 🤝 贡献
本项目通过 AI 自我迭代进行维护。请遵循 `docs/handovers/` 中的最新记录进行上下文恢复。
