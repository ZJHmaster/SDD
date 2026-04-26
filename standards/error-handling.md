# 异常处理与容错设计规范 (Error Handling)

## 1. 异常分层设计
### 1.1 异常分类体系
| 异常类型 | 定义 | 处理策略 | HTTP Status |
|---------|------|---------|:-----------:|
| **业务异常** (BusinessException) | 可预见的业务规则冲突（余额不足、库存为零） | 向调用方返回友好错误码与提示 | 400/422 |
| **参数异常** (ValidationException) | 入参校验失败 | 返回具体的字段错误信息 | 400 |
| **认证/授权异常** (AuthException) | 身份验证或权限校验失败 | 标准401/403，不泄露内部信息 | 401/403 |
| **系统异常** (SystemException) | 不可预见的内部错误（NPE、OOM） | 记录完整堆栈，返回兜底错误信息 | 500 |
| **第三方异常** (ExternalException) | 依赖的外部服务不可用或超时 | 触发重试/降级/熔断策略 | 502/503 |

### 1.2 异常类层级建议
```
BaseException (基类，携带errorCode + message)
├── BusinessException
│   ├── InsufficientBalanceException
│   └── OrderAlreadyPaidException
├── ValidationException
├── AuthException
│   ├── UnauthenticatedException
│   └── AccessDeniedException
├── SystemException
└── ExternalServiceException
    ├── PaymentGatewayException
    └── SmsServiceException
```

## 2. 铁律约束
1. **禁止空 Catch**：`catch (Exception e) {}` 是代码级别的严重事故。异常必须被处理（日志/重抛/降级）。
2. **不要用异常控制业务流程**：异常不是 `if-else`的替代品品。预期的业务岔路应使用返回值/Result模式。
3. **统一全局异常拦截器**：在框架层提供 `GlobalExceptionHandler`（如 Spring 的 `@ControllerAdvice`），确保任何未处理的异常都被兜底捕获并以标准错误格式返回。
4. **错误信息不泄露内部**：返回给客户端的错误信息绝不能包含堆栈、SQL 语句、内部类名等。

## 3. 容错设计模式
### 3.1 重试 (Retry)
- 仅对幂等操作进行重试（GET 请求、带去重键的写操作）。
- 重试策略：指数退避 + 抖动（Exponential Backoff with Jitter）。
- 最大重试次数 ≤ 3。

### 3.2 熔断 (Circuit Breaker)
- 当下游服务连续失败率超过阈值（如 50% 在 10 秒窗口内），自动开启熔断，直接返回降级响应。
- 半开状态下放部分流量探测恢复。

### 3.3 降级 (Fallback)
- 非核心功能在熔断时提供静态/缓存数据或简化版逻辑响应。
- 核心链路有明确的预案文档（参见 `governance/incident-severity.md`）。

## 4. 统一错误码体系
建议使用 `<服务代码>_<模块代码>_<错误序号>` 格式：
```
ORD_PAY_001 = "支付渠道不可用"
ORD_PAY_002 = "订单金额与支付金额不一致"
USR_AUTH_001 = "Token 已过期"
```
错误码须在项目的 `error-codes.md` 或配置文件中集中维护，禁止散落在代码各处。
