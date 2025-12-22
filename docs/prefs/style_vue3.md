# Vue 3 前端代码风格偏好

## 1. 架构分层
*   **项目结构:**
    *   `src/services`: 负责 API 逻辑 (`axios`, `sse.js` 集成)。
    *   `src/schemas`: 定义 JavaScript 类作为 DTO (数据传输对象)。
    *   `src/stores`: Pinia 状态管理模块。
    *   `src/views`: 页面级别的组件。
    *   `src/components`: 可复用的 UI 组件。
*   **技术栈:** Vue 3 (Composition API), Vite, Pinia, Axios, SSE.js。
*   **推荐库 (Libraries):**
    *   **UI 组件:** Ant Design Vue (后台/企业级) 或 Element Plus。
    *   **可视化:** Apache ECharts。
    *   **渲染:** PixiJS (用于 2D 游戏/高交互场景)。

## 2. 编码约定
*   **Vue Script Setup:** 使用 `<script setup>` 语法糖。
*   **Schema 定义:** 为 API 响应定义显式的 JavaScript 类 (例如 `ChatResponse`, `ChatResponseItem`)，以便处理类型和默认值。
*   **SSE 处理:**
    *   使用 `sse.js` 库处理 Server-Sent Events。
    *   服务层 (`services`) 负责处理 SSE 连接和消息 (`onmessage` 事件)。
    *   通过回调函数更新 UI 层的响应式变量。
*   **Pinia:** 采用标准选项存储风格 (`state`, `actions`, `getters`)。
*   **CSS 样式:** 使用 Scoped CSS，并利用 CSS 变量实现主题化 (例如 `--el-bg-color` 模仿 Element Plus)。
*   **文档注释:** JavaScript 文件中的类/函数也使用类似 Javadoc 的注释风格。

## 3. 示例代码片段

### Schema
```javascript
// Schemas mimicking backend DTOs
export const MessageType = {
  TEXT: "text",
  CONFIG: "config"
};

export class ChatResponse {
  /**
   * @param {Object} data
   */
  constructor(data = {}) {
    Object.assign(this, data);
  }
}
```

### Service
```javascript
import { SSE } from "sse.js";
const API_BASE_URL = import.meta.env.VITE_BASE_API;

export class ChatService {
  async sendStream(query, callback) {
    const sse = new SSE(`${API_BASE_URL}/stream`, { 
        payload: JSON.stringify({ query }) 
    });
    sse.onmessage = (e) => callback(JSON.parse(e.data));
    sse.stream();
  }
}
```