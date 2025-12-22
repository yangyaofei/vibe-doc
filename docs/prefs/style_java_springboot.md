# Java / Spring Boot 代码风格偏好

## 1. 架构分层
*   **技术栈核心:**
    *   **Java 版本:** JDK 21+ LTS (利用 Virtual Threads 优化高并发 I/O)。
    *   **构建工具:** Gradle (推荐 Kotlin DSL 或 Groovy)。
*   **分层架构:**
    *   `config`: 配置类 (`@Configuration`)。
    *   `controller`: REST 控制器 (`@RestController`)。
    *   `service`: 业务逻辑层 (`@Service`)。
    *   `entity`: 数据传输对象 (DTO)/请求对象 (`@Data`)，示例中常直接用作实体。
    *   `model`: 自定义 AI/API 模型。
    *   `repository`: (通过 Spring Data JPA 隐式使用)。

## 2. 编码约定
*   **Lombok:** 广泛使用 `@Data`, `@NoArgsConstructor`, `@AllArgsConstructor`, `@Accessors(chain = true)`, `@Slf4j` 等注解，简化样板代码。
*   **数据验证:** 使用 `jakarta.validation` (`@Valid`, `@NotEmpty`) 进行数据输入验证。
*   **实时通信 (Real-time):**
    *   **SSE (Server-Sent Events):** 用于单向流式数据（如 LLM 打字机效果）。使用 `SseEmitter`。
    *   **WebSocket (+STOMP):** 用于复杂的双向交互（如多人游戏）。
*   **AI 集成:**
    *   使用 `Spring AI` (`ChatClient`, `OpenAiChatModel`) 进行 AI 模型交互。
    *   **规范模式:** 使用 `chatClient.prompt().user(...).call().entity(Class.class)` 模式来获取结构化的 JSON 输出。
    *   **Prompt 编写:** Prompt (提示词) 使用 Java 文本块 (`""" ... """`) 直接嵌入在 Service 层中，或者从资源文件加载。
*   **控制器 (Controller Rules):**
    *   **依赖注入:** 推荐使用构造函数注入（Constructor Injection）服务依赖。
    *   **返回值:** 方法返回 `ResponseEntity` 或直接的业务对象。
    *   **API 文档:** 使用 `@Tag` 注解增强 OpenAPI/Swagger 文档。
*   **文档注释 (至关重要):**
    *   **Javadoc:** 每个类、字段和方法都必须包含详细的 Javadoc 注释。
    *   **类头注释:** 说明类的用途、功能列表。
    *   **方法头注释:** 描述方法功能、参数详情、返回值详情。

## 3. 示例代码片段
```java
/**
 * 案例解析服务
 * 负责解析案例内容并转换为结构化格式
 */
@Slf4j
@RestController
@RequestMapping("/api/v1")
public class ExampleController {
    private final ExampleService service;

    public ExampleController(ExampleService service) {
        this.service = service;
    }

    /**
     * 解析接口
     * @param request 请求体
     * @return 响应实体
     */
    @PostMapping("/parse")
    public ResultDto parse(@RequestBody @Valid RequestDto request) {
        return service.process(request);
    }
}
```