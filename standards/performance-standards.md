# 性能基线与SLA/SLO规范 (Performance Standards)

## 1. 性能基线指标
以下为企业级Web应用的基线性能参考值。各业务线可在此基础上定义更严格的目标。

### 1.1 接口响应时间
| 接口类型 | P50 | P95 | P99 | 超时上限 |
|---------|-----|-----|-----|---------|
| 简单查询 (单实体) | ≤ 50ms | ≤ 100ms | ≤ 200ms | 1s |
| 列表查询 (分页) | ≤ 100ms | ≤ 300ms | ≤ 500ms | 3s |
| 写操作 (创建/更新) | ≤ 100ms | ≤ 300ms | ≤ 500ms | 5s |
| 复杂聚合/报表 | ≤ 500ms | ≤ 2s | ≤ 5s | 30s |
| 文件上传/导出 | - | - | - | 60s |

### 1.2 前端性能 (Core Web Vitals)
| 指标 | 目标值 | 说明 |
|------|--------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 最大内容绘制时间 |
| INP (Interaction to Next Paint) | ≤ 200ms | 交互响应性 |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 视觉稳定性 |
| TTFB (Time To First Byte) | ≤ 800ms | 服务器首字节响应 |

## 2. 容量设计原则
- **冗余系数**：系统设计容量须为预期峰值流量的 **3倍**。
- **弹性扩缩**：应用层必须支持水平扩展 (Horizontal Scaling)，禁止在应用层持有本地状态。
- **降级策略**：核心链路须有明确的降级方案（如关闭推荐算法以保障下单主流程）。

## 3. 性能测试要求
- 每个版本发布前，必须通过**基准性能测试** (Benchmark Test)。
- Major 版本需执行**压力测试** (Stress Test)，找到系统崩溃点。
- 性能测试结果须存档，作为后续版本回归对比的数据基线。
- 推荐工具：JMeter / k6 / Gatling / Locust。

## 4. 性能编码规范
- 数据库查询必须避免全表扫描，使用 `EXPLAIN` 验证执行计划。
- 禁止在循环中执行 I/O 操作（网络请求/DB查询）。
- 大对象缓存须设置合理 TTL 和淘汰策略。
- 前端禁止同步加载大型 JS Bundle（必须 Code Split + Lazy Load）。

## 5. SLA 定义参考
参见 `governance/sla-slo-definitions.md` 获取完整的服务等级定义。
