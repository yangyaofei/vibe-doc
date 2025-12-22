# Python .gitignore 规范

本文档汇总了通用 Python 项目的 `.gitignore` 忽略规则。

## 1. 核心 Python 运行产物
用于忽略字节码、运行时缓存及构建产物。

```gitignore
__pycache__/
*.py[cod]
*$py.class
*.pyd
*.pyc
*.so
.Python
```

## 2. 虚拟环境隔离 (Environment)
```gitignore
venv/
.venv/
env/
/venv/
.env
```

## 3. 开发工具与 IDE (Development Tools)
*   **JetBrains (IntelliJ/PyCharm)**: `.idea/`, `*.iws`, `*.iml`
*   **VS Code**: `.vscode/`
*   **System**: `.DS_Store`
*   **AI Context**: `.claude`, `.gemini`
*   **Editor**: `*.swp`

## 4. 条件性添加 (按需开启)

### 4.1 构建与分发 (Build & Distribution)
如果项目涉及打包和分发。

```gitignore
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg
```

### 4.2 gRPC 开发 (gRPC Support)
如果项目涉及 gRPC 通信并生成 Python 代码。

```gitignore
# gRPC Generated files
*_pb2.py
*_pb2.pyi
*_pb2_grpc.py
*_pb2*
```

### 4.3 Web 框架与本地调试 (FastAPI/Web)
适用于 Web 后端包含本地配置或集成前端构建的情况。

```gitignore
# Local environment
*.local
config.env

# Logs
logs/
*.log

# Shared artifacts (if frontend is integrated)
node_modules/
```
