# Handover Document: Python Structure Refinement

## 1. Status (当前状态)
*   **Python 风格指南重构**: Python 相关规范已拆分为核心基础 (`Core`)、Web 框架 (`FastAPI`) 和 RPC 通信 (`gRPC`) 三个独立文档，结构更加清晰。

## 2. History (本次变更)
*   **Refactored**: 将原 `style_python_fastapi.md` 拆分并重组。
*   **New `docs/prefs/style_python_core.md`**:
    *   **Config**: 确立了 `pydantic-settings` 的核心地位。
    *   **Schema**: 规范了 `schemas/` 目录和命名。
    *   **Gitignore**: 定义了标准的 Python 忽略规则（含 IDE 和 gRPC 产物）。
*   **Updated `docs/prefs/style_python_fastapi.md`**:
    *   **Structure**: 定义了 Standard (src) 和 Modular (modules) 两种项目结构。
    *   **Lifecycle**: 强制使用 `lifespan` 替代旧的 `on_event`。
    *   **Features**: 增加了 Static Files 挂载和 CORS 中间件配置规范。
*   **New `docs/prefs/style_python_grpc.md`**:
    *   **Automation**: 引入了基于 `setup.py` 的 proto 自动编译流程。
    *   **Integration**: 明确了生成文件的管理规则（不提交 Git）。

## 3. Next Steps (下一步计划)
*   **验证**: 在新项目中试用这套分层规范，验证 gRPC 自动构建流程的兼容性。
