# Sprint 迭代协议 (Sprint Protocol)

## 1. 迭代定义
项目按 **Sprint 1, 2, 3...** 分阶段推进。每个 Sprint 代表一个可交付的里程碑。

### 最佳实践：垂直切片 (Vertical Slices)
**强烈建议**按“功能特性”进行垂直切片开发，而非水平技术层。
*   **定义**: 一个任务应包含从数据库到前端界面的完整路径。
*   **Sprint 1 示例**: "实现基本的 LLM 对话回路"（而非 "设计数据库架构"）。
*   **优势**: 尽早验证集成风险，提供可演示的成果。

## 2. 生命周期
1.  **启动 (Planning)**:
    * 创建 `docs/plans/sprint_{xx}_plan.md` (总计划)。
    * 拆分具体任务为 `docs/plans/sprint_{xx}_task_{yy}_{name}.md`。
2.  **执行 (Execution)**:
    * 按照子任务计划执行开发工作流。
3.  **结项 (Closing)**:
    * 编写 `docs/archive/sprint_{xx}_summary.md`。
    * 将 `docs/plans/` 下该阶段的文档移动至 `docs/archive/sprint_{xx}/`。
    * 更新 `tech.md` 中的状态。

## 3. 状态管理
* **Pending**: 计划中。
* **In Progress**: 正在执行。
* **Archived**: 已完成并归档。
