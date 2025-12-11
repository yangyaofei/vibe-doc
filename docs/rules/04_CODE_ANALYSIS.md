# 代码规范分析协议 (Code Analysis Protocol)

## 1. 目标
从现有的代码库（`src/` 或参考资料 `data/`）中提取隐式的编程风格和架构模式，将其显式化为文档，存入 `docs/prefs/`。

## 2. 触发时机
*   接手一个新项目，且 `docs/prefs/` 为空时。
*   需要编写一种新语言/新框架的代码，但 `docs/prefs/` 中缺少对应指南时。
*   用户明确指令：“分析当前代码风格”。

## 3. 分析维度 (Analysis Dimensions)

### A. 语言与语法 (Language Specifics)
*   **Naming**: PascalCase vs camelCase vs snake_case (类、方法、变量、常量)。
*   **Typing**: 强类型 (TS/Java) 的使用严格程度。
*   **Formatting**: 缩进 (2 space/4 space)、分号、括号风格。

### B. 架构与分层 (Architecture)
*   **Directory Structure**: 典型的目录树是什么样的？
*   **Layering**: Controller -> Service -> Repository? 还是其他模式？
*   **Data Flow**: DTO 的使用位置？Entity 是否直接暴露？

### C. 库与框架 (Libraries)
*   **Core**: 使用了哪些核心框架 (Spring Boot 2 vs 3, Vue 2 vs 3)？
*   **Utils**: 偏好哪个工具库 (Lombok, Hutool, Lodash, date-fns)？

## 4. 输出产物
在 `docs/prefs/` 下创建对应文件，例如：
*   `java_style.md`
*   `vue_style.md`
*   `project_structure.md`

**内容示例**:
```markdown
# Java Coding Preferences
*   **Entity**: 使用 Lombok `@Data`。
*   **Controller**: 必须返回 `Result<T>` 包装类。
*   **Service**: 接口与实现分离 (IUserService + UserServiceImpl)。
```
