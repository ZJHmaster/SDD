# API 设计规范 (API Design Guide)

## 1. RESTful API 最佳实践

### 1.1 资源导向的 URI
- URI 应该代表资源，必须使用**名词**，且建议使用**复数形式**。
- 🚫 错误：`/api/getUser`, `/api/createOrder` (混杂了动词)
- ✅ 正确：`GET /api/users`, `POST /api/orders`

### 1.2 HTTP 方法的准确映射
- **GET**：读取资源，必须是幂等的，不产生副作用。
- **POST**：创建新资源或执行不具有特定语义的操作。
- **PUT**：幂等性更新资源的整个实体内容。
- **PATCH**：局部更新资源实体的特定字段。
- **DELETE**：删除资源。

## 2. 状态码使用规范
绝不允许所有请求都无脑返回 `200 OK` 然后在返回体里包一个业务 Error 字段（除 GraphQL 等特殊协议外）。
- `200 OK` / `201 Created` / `204 No Content`（用于成功）
- `400 Bad Request`（参数校验失败）
- `401 Unauthorized`（未登绿/Token失效）
- `403 Forbidden`（已登录但无权限访问该资源）
- `404 Not Found`（资源不存在）
- `422 Unprocessable Entity`（业务规则冲突）
- `500 Internal Server Error`（服务端兜底未知异常）

## 3. 数据载荷结构
企业级 API 响应需保持稳定的最外层结构外壳：
```json
{
  "code": "SUCC",                  // 内部业务码，"SUCC" 为通用成功
  "message": "Operation success", // 友好的用户提示或开发报错
  "data": { ... },                // 真正的业务返回体实体（列表或对象）
  "traceId": "abc123xyz"          // 全链路追踪使用的唯一请求ID
}
```

## 4. 版本管理与限流
- 破坏性更新必须引入版本号隔离，如：`/api/v1/users` -> `/api/v2/users`。
- 公共 API 必须提供限流并在 Header 返回 `X-RateLimit-Limit` 和 `X-RateLimit-Remaining`。
