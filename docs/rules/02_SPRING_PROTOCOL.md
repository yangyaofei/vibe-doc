# Spring 迭代协议 (Spring Protocol)

## 1. 迭代定义
项目按 **Spring 1, 2, 3...** 分阶段推进。每个 Spring 代表一个可交付的里程碑。

## 2. 生命周期
1.  **启动 (Planning)**:
    * 创建 `docs/plans/spring_{xx}_plan.md` (总计划)。
    * 拆分具体任务为 `docs/plans/spring_{xx}_task_{yy}_{name}.md`。
2.  **执行 (Execution)**:
    * 按照子任务计划执行开发工作流。
3.  **结项 (Closing)**:
    * 编写 `docs/archive/spring_{xx}_summary.md`。
    * 将 `docs/plans/` 下该阶段的文档移动至 `docs/archive/spring_{xx}/`。
    * 更新 `tech.md` 中的状态。

## 3. 状态管理
* **Pending**: 计划中。
* **In Progress**: 正在执行。
* **Archived**: 已完成并归档。