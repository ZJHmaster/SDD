# 文档编写标准 (Documentation Standards)

## 1. 文档分层体系
企业项目的文档不是一堆散落的 Word 文件，它是一套多层级、有明确受众的知识系统。

| 层级 | 文档类型 | 受众 | 更新频率 |
|------|---------|------|---------|
| L1 | 产品需求文档 (PRD) | PM/全体 | 按版本 |
| L2 | 架构决策记录 (ADR) | 架构师/技术负责人 | 按决策 |
| L3 | API 参考文档 | 前后端/外部合作方 | 随代码 |
| L4 | 代码内注释 (JSDoc/JavaDoc) | 开发者 | 随代码 |
| L5 | 运维手册 / Runbook | SRE/运维 | 按发布 |
| L6 | 变更日志 (CHANGELOG) | 全体 | 每次发版 |

## 2. 架构决策记录 (ADR - Architecture Decision Records)
每一个重要的技术选型或架构决策，皆须通过 ADR 进行记录，格式参见 `governance/adr-template.md`。

### 核心规则
- ADR 一旦被接受 (Accepted)，不得修改，只能通过新的 ADR 来"取代"旧的决策。
- 编号递增：`ADR-0001`, `ADR-0002`, ...
- 存放位置：项目根目录 `/docs/adr/` 目录下。

## 3. API 文档规范
- RESTful API 必须使用 **OpenAPI 3.0 (Swagger)** 规范编写。
- API 文档应当与代码同仓 (Code-First 或 Spec-First 均可)，禁止在独立的 Wiki 中手动维护而与代码脱节。
- 每个端点必须包含：描述、请求参数 Schema、响应 Schema、错误码列表、请求示例。

## 4. README 最低要求
项目根目录 README.md 必须至少包含：
1. **项目简介**：一句话说明本项目是什么。
2. **快速启动**：从 clone 到 run 的完整命令序列。
3. **架构图**：一张高层级的模块/服务关系图。
4. **目录结构说明**。
5. **环境变量列表**。
6. **贡献指南**链接。

## 5. 变更日志 (CHANGELOG)
遵循 [Keep a Changelog](https://keepachangelog.com/) 格式：
```markdown
## [2.3.0] - 2026-04-26
### Added
- 新增微信支付渠道
### Fixed
- 修复订单超时后未释放库存的问题
### Changed
- 优化搜索接口响应速度(P95 从 800ms 降至 200ms)
### Deprecated
- 废弃旧版 V1 退款接口，将于 V3.0 移除
```

## 6. Agent 自动化文档审计
配套的 `.agents/workflows/documentation-audit.md` 能够自动扫描项目，检查以下内容的完整度：
- 公开函数是否缺失 Doc 注释
- README 是否包含最低信息
- ADR 目录是否有新的未登记决策
