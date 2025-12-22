# Python Core Development Style

## 1. Project Structure & Organization
*   **Source Root**: 推荐使用 `src/` 目录作为源码根目录，保持顶层目录整洁。
*   **Dependencies**: 使用 `requirements.txt` 进行依赖管理。
*   **Type Hinting**: 
    *   **强制**: 所有函数参数和返回值必须包含 Type Annotation。
    *   **目的**: 启用静态代码分析 (mypy/pyright) 和 IDE 智能提示。
*   **Git Ignore**: 必须遵循 [Python .gitignore 规范](./style_python_gitignore.md)。

## 2. Configuration Management (config.py)
*   **Library**: 必须使用 `pydantic-settings`。
*   **Pattern**: 
    *   创建 `utils/config.py` 或 `core/config.py`。
    *   使用 `BaseSettings` 定义配置模型。
    *   使用 `settings_customise_sources` 确保环境变量优先级最高。
    *   使用 `__` 作为嵌套配置的分隔符。

### 2.1 Configuration Template
标准的 `pydantic-settings` 定义方式，支持环境变量覆盖和嵌套。

```python
from pathlib import Path
from typing import Type, Tuple
from pydantic_settings import (
    BaseSettings, 
    PydanticBaseSettingsSource, 
    SettingsConfigDict
)

class DatabaseConfig(BaseSettings):
    host: str = "localhost"
    port: int = 5432

class Settings(BaseSettings):
    APP_NAME: str = "My App"
    DEBUG: bool = False
    
    # 嵌套配置 (对应环境变量: DB__HOST)
    db: DatabaseConfig = DatabaseConfig()
    
    model_config = SettingsConfigDict(
        env_nested_delimiter='__',
        env_file=('.env', 'config.env'),
        extra='ignore'
    )

    @classmethod
    def settings_customise_sources(
        cls,
        settings_cls: Type[BaseSettings],
        init_settings: PydanticBaseSettingsSource,
        env_settings: PydanticBaseSettingsSource,
        dotenv_settings: PydanticBaseSettingsSource,
        file_secret_settings: PydanticBaseSettingsSource,
    ) -> Tuple[PydanticBaseSettingsSource, ...]:
        # 优先级: 环境变量 > DotEnv 文件 > 初始化默认值
        return env_settings, dotenv_settings, init_settings

def get_config() -> Settings:
    return Settings()
```

### 2.2 Path Resolution Utils
不要使用脆弱的 `parents[2]` 索引，建议使用辅助函数。

```python
import os
from pathlib import Path

def get_project_path() -> Path:
    """获取工程根目录 (假设此文件位于 src/utils/config.py)"""
    return Path(os.path.abspath(os.path.dirname(__file__)), "../../").resolve().absolute()

def get_project_abs_path(path: str) -> Path:
    """获取项目内文件的绝对路径"""
    return Path(get_project_path(), path).resolve().absolute()
```

### 2.3 YAML Config Source (Optional)
如果偏好 YAML 配置文件，可结合 `PyYAML` 和 `Pydantic`。

```python
import os
from functools import lru_cache
from yaml import Loader, load
from pydantic_settings import BaseSettings

class Config(BaseSettings):
    ...

@lru_cache()
def get_config_from_yaml() -> Config:
    path = get_project_path() / "config.yaml"
    if path.exists():
        with open(path, encoding="utf-8") as f:
            config_data = load(f, Loader=Loader)
        # 环境变量覆盖需依赖 Pydantic 构造函数
        return Config(**config_data)
    return Config() 
```

## 3. Data Schemas
*   **Library**: `pydantic`.
*   **Location**: 所有数据模型应存放在 `schemas/` 目录中。
*   **Naming**: 
    *   文件: `schemas/user.py`, `schemas/chat.py`
    *   类名: `UserCreate`, `UserResponse`, `ChatRequest`
*   **Validation**: 充分利用 Pydantic 的校验功能，避免在业务逻辑中进行基础类型检查。