# Monorepo 项目结构偏好

## 1. 核心原则
*   **前后端分离 (Physical Separation)**: 前端和后端代码分别位于独立的顶层目录中，互不干扰构建流程。
*   **统一编排 (Unified Orchestration)**: 使用根目录下的 `docker-compose.yml` 统一管理本地开发环境和依赖服务（如 DB, Redis）。
*   **文档即代码 (Docs as Code)**: 文档与代码同源，统一存放于 `docs/` 目录。

## 2. 标准目录结构
推荐采用以下目录结构：

```text
/ (Project Root)
├── backend/                # 后端工程 (Java/Spring Boot or Python/FastAPI)
│   ├── src/                # 源代码
│   ├── build.gradle        # (Java) 构建配置
│   ├── requirements.txt    # (Python) 依赖配置
│   └── Dockerfile          # 后端容器构建文件
│
├── frontend/               # 前端工程 (Vue 3/React)
│   ├── src/                # 源代码
│   ├── package.json        # 依赖配置
│   ├── vite.config.ts      # 构建配置
│   └── Dockerfile          # 前端容器构建文件 (通常为 Nginx 静态服务)
│
├── docs/                   # 项目文档
│   ├── rules/              # (可选) Vibe-Doc 规则
│   ├── tech.md             # 技术架构说明
│   └── ...
│
├── deploy/                 # (可选) 生产环境部署配置 (K8s yaml, Helm charts)
├── scripts/                # (可选) 自动化脚本 (数据迁移, 启动脚本)
├── docker-compose.yml      # 本地开发环境编排
└── README.md               # 项目入口文档
```

## 3. 命名约定变体
根据技术栈的不同，顶层目录命名可能存在以下变体，但结构逻辑保持一致：

*   **Standard (推荐)**: `backend` / `frontend`
*   **Legacy / Game**: `server` / `client`

## 4. 关键文件配置
*   **`.gitignore`**: 根目录应包含全局忽略规则（如 IDE 配置, `.DS_Store`），各子目录（`backend/`, `frontend/`）应包含各自技术栈特定的忽略规则。
*   **`docker-compose.yml`**: 应定义 `db` (数据库), `backend` (后端服务), `frontend` (前端服务) 等服务，并通过环境变量注入配置。
