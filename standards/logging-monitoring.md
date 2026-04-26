# 日志、监控与可观测性规范 (Logging & Monitoring)

## 1. 结构化日志 (Structured Logging)
### 1.1 格式
所有服务必须输出 JSON 格式的结构化日志，禁止使用纯文本拼接。
```json
{
  "timestamp": "2026-04-26T09:30:00.123Z",
  "level": "ERROR",
  "service": "order-service",
  "traceId": "abc-123-def-456",
  "spanId": "span-789",
  "userId": "u_10001",
  "message": "Payment gateway timeout",
  "error": {
    "type": "GatewayTimeoutException",
    "stack": "..."
  },
  "context": {
    "orderId": "ORD-20260426-001",
    "amount": 199.00,
    "gateway": "wechat"
  }
}
```

### 1.2 日志级别使用规范
| 级别 | 用途 | 生产默认开启 |
|------|------|:---:|
| `TRACE` | 极其细粒度的调试信息 | ❌ |
| `DEBUG` | 开发调试用的上下文信息 | ❌ |
| `INFO` | 关键业务流转节点 | ✅ |
| `WARN` | 异常但系统可自愈的状况 | ✅ |
| `ERROR` | 需要人工介入的系统错误 | ✅ |
| `FATAL` | 导致服务不可用的致命错误 | ✅ |

### 1.3 必须记录的 INFO 日志节点
- 请求入口（包含 traceId）
- 关键业务状态变迁（订单创建→支付→发货）
- 外部系统调用的出入参与耗时
- 定时任务的开始与结束

## 2. 全链路追踪 (Distributed Tracing)
- 每个入站请求必须生成或传播 `traceId`。
- 跨服务调用必须在 HTTP Header 透传追踪上下文（如 `X-Trace-Id`, `X-Span-Id`），推荐接入 OpenTelemetry 标准。
- 日志、指标、追踪三者必须通过 `traceId` 实现关联。

## 3. 核心监控指标 (Metrics)
每个服务必须暴露以下黄金指标：
- **延迟 (Latency)**：P50 / P95 / P99 响应时间。
- **流量 (Traffic)**：QPS（每秒查询次数）。
- **错误率 (Error Rate)**：5xx 错误占比。
- **饱和度 (Saturation)**：CPU/内存/连接池利用率。

## 4. 告警策略
- 告警必须分级：P0（立即电话通知）> P1（15分钟内钉钉/飞书）> P2（工单跟进）。
- 严禁"告警疲劳"——每条告警规则须有明确的阈值和有效的响应 SOP（标准操作流程）。
- 建议运用 `governance/incident-severity.md` 中的事故分级与告警联动。

## 5. 隐私红线
- 日志中严禁记录明文密码、完整银行卡号、身份证全号。
- PII 数据在日志中须脱敏：手机号 `138****1234`，邮箱 `u***@example.com`。
