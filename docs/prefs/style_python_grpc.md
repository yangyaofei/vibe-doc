# Python / gRPC Style Guide

## 1. Project Structure
gRPC 项目通常作为更大系统的一部分或独立微服务存在。

```text
project_root/
├── protos/                 # .proto source files
│   └── service.proto
├── src/                    # Python Source
│   ├── grpc_generated/     # Generated Python Code (Ignored by Git)
│   └── server.py           # gRPC Server Implementation
├── setup.py                # Build automation
└── requirements.txt
```

## 2. Dependencies
必须包含以下核心依赖：
*   `grpcio`
*   `grpcio-tools`
*   `protobuf`

## 3. Automation (`setup.py`)
使用 `setup.py` 中的 `cmdclass` 自动编译 `.proto` 文件为 Python 代码。这避免了手动运行 `protoc` 命令，确保构建的一致性。

### `setup.py` Template
```python
#!/usr/bin/env python3
import os
import sys
from setuptools import setup, find_packages
from grpc_tools import command

setup(
    name="my-grpc-service",
    version="0.1.0",
    packages=find_packages(),
    # Define dependencies
    install_requires=[
        "grpcio>=1.50.0",
        "grpcio-tools>=1.50.0",
        "protobuf>=4.21.0",
    ],
    # Auto-generate proto code during build
    cmdclass={
        'build_proto_modules': command.BuildPackageProtos
    },
)
```

## 4. Integration Rules
*   **Git Ignore**: 永远不要提交生成的 `*_pb2.py` 和 `*_pb2_grpc.py` 文件。