# 开发工作流指南 (Workflow Guidelines)

Agent 必须根据当前所处的阶段（Phase）选择对应的工作流。

## Workflow 0: 需求分析 (Requirement Analysis)
**适用**: Phase 0 (项目启动或新功能模块提出时)

1.  **Capture (捕获)**: 将用户的模糊描述写入 `docs/requirement.md`。
2.  **Clarify (澄清)**: 
    *   分析需求，找出模棱两可点。
    *   向用户提问 (e.g., "关于用户登录，是做简单的 Cookie 还是 JWT？")。
3.  **Refine (细化)**: 将确认后的内容更新到文档。
4.  **Finalize (定稿)**: 输出 `docs/requirement_detail.md`。

## Workflow 1: 核心开发循环 (Core Dev Loop)
**适用**: Phase 2 (Spring 迭代中的具体任务)

遵循 **Plan -> Analyze -> Act -> Verify -> Document** 循环：

1.  **情境化 (Contextualize)**:
    *   阅读 `tech.md` 和当前的任务计划。
2.  **风格分析 (Style Analysis)**:
    *   **Check**: 检查 `docs/prefs/` 是否有相关语言/框架的规范。
    *   **If Missing**: 执行 `docs/rules/04_CODE_ANALYSIS.md` 提取规范。
3.  **计划 (Plan)**:
    *   输出简短的执行计划 (Step 1, Step 2...)。
4.  **实施 (Implement)**:
    *   编写代码，严格模仿 `docs/prefs/` 中的风格。
5.  **验证 (Verify)**:
    *   运行测试、构建脚本或 `curl` 请求。严禁盲目提交。
6.  **总结 (Summary)**:
    *   创建 `docs/archive/step_{N}_abstract.md` (模板见下)。
7.  **提交 (Commit)**:
    *   Format: `feat(scope): Description (Step N)`

### Step Abstract 模板
```markdown
# Step {N} Summary
## 1. 变更摘要
* 简述修改了什么功能。

## 2. 关键决策
* 为什么选择这个库？
* 为什么采用这个设计模式？

## 3. 验证结果
* [x] Build Pass
* [x] Test Pass (附 log 摘要)
```
