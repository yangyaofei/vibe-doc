# Python / FastAPI Style Guide

## 1. Project Structure (Web & Agents)
FastAPI 项目应根据复杂度选择结构。

### 1.1 Standard Layout (Recommended for Agents/Services)
适用于大多数中型应用。
```text
project_root/
├── src/
│   ├── api/            # Route Controllers
│   ├── core/           # Config, Security
│   ├── schemas/        # Pydantic Models (see Core Style)
│   ├── services/       # Business Logic
│   └── main.py         # Entry Point
├── .env
└── requirements.txt
```

### 1.2 Modular Layout (Recommended for Complex Monoliths)
适用于包含多个独立子系统的应用（如 Crawler + LLM + API）。
```text
project_root/
├── server/
│   ├── modules/
│   │   ├── crawler/    # Isolated Module
│   │   └── llm/
│   └── main.py
└── Dockerfile
```

## 2. Application Setup

### 2.1 Lifecycle (OnStart / OnShutdown)
使用 `lifespan` 上下文管理器替代旧的 `on_event`。
适用于初始化数据库连接、启动后台调度器（APScheduler）等。

```python
from contextlib import asynccontextmanager
from fastapi import FastAPI
from apscheduler.schedulers.background import BackgroundScheduler

scheduler = BackgroundScheduler()

@asynccontextmanager
async def lifespan(app: FastAPI):
    # --- Startup ---
    print("Startup: Initializing resources...")
    scheduler.start()
    
    yield  # Application runs here
    
    # --- Shutdown ---
    print("Shutdown: Cleaning up...")
    scheduler.shutdown()

app = FastAPI(lifespan=lifespan)
```

### 2.2 Middleware (CORS)
如果前端与后端分离部署，需要配置 CORS。

```python
from fastapi.middleware.cors import CORSMiddleware

# 根据项目需求决定是否开启
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Production: specific domains
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### 2.3 Static Files (SPA Support)
使用自定义的 `StaticFiles` 类以支持 SPA 路由（404 Fallback 到 `index.html`）。

```python
import os
from starlette.exceptions import HTTPException
from starlette.responses import FileResponse
from starlette.staticfiles import StaticFiles

class SpaStaticFiles(StaticFiles):
    """支持 SPA 的静态文件服务 (404 -> index.html)"""
    def __init__(self, directory: str, index_html: str = "index.html", **kwargs):
        super().__init__(directory=directory, **kwargs)
        self.index_html = index_html

    async def get_response(self, path: str, scope):
        try:
            return await super().get_response(path, scope)
        except HTTPException as e:
            if e.status_code == 404:
                index_path = os.path.join(self.directory, self.index_html)
                if os.path.exists(index_path):
                    return FileResponse(index_path)
            raise e

# Usage
# app.mount("/", SpaStaticFiles(directory="dist", html=True), name="static")
```

## 3. Running & Deployment
*   **Command**: 使用 `uvicorn` 启动。
*   **Dev**: `uvicorn src.main:app --reload`
*   **Prod**: `uvicorn src.main:app --host 0.0.0.0 --port 8000 --workers 4`

## 4. Key Patterns
*   **Sync vs Async**: 
    *   **Prefer Sync**: 在大多数业务逻辑中，尽量编写简单的同步代码 (`def`)，除非有明确的高并发 I/O 需求。同步代码更易于调试和维护。
