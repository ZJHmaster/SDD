# CI/CD 与 DevOps 规范 (DevOps & CI/CD)

## 1. CI 管线 (Continuous Integration Pipeline)
### 1.1 必选阶段
每次向主干或特性分支推送代码时，CI 管线须自动执行以下有序阶段：

```
┌─────────┐  ┌──────────┐  ┌──────────┐  ┌────────────┐  ┌──────────┐
│  Lint   │→│  Build   │→│  Test    │→│  Security  │→│ Artifact │
│ 代码检查 │  │ 编译构建  │  │ 单元/集成 │  │ 漏洞扫描   │  │ 产物归档  │
└─────────┘  └──────────┘  └──────────┘  └────────────┘  └──────────┘
```

| 阶段 | 内容 | 失败策略 |
|------|------|---------|
| Lint | 代码格式、命名、静态分析 | 阻断 |
| Build | 编译/打包 | 阻断 |
| Test | 单元测试 + 集成测试 | 阻断 |
| Security | 依赖漏洞 + SAST | CRITICAL/HIGH 阻断 |
| Artifact | 构建产物归档（Docker Image/JAR/Bundle） | 仅通知 |

### 1.2 CI 性能要求
- 整条管线的端到端执行时间控制在 **15分钟以内**。
- 超过此阈值须调查并优化（并行化测试、缓存依赖、增量构建）。

## 2. CD 管线 (Continuous Delivery/Deployment)
### 2.1 环境分级
| 环境 | 用途 | 部署触发 |
|------|------|---------|
| `dev` | 开发自测 | 特性分支推送自动部署 |
| `staging` | 集成验收/QA | 合并到 main 后自动部署 |
| `pre-prod` | 预发布/灰度 | 手动触发或计划性发布 |
| `production` | 生产环境 | 经审批后手动或标签触发 |

### 2.2 发布策略
- **默认**：滚动更新 (Rolling Update)。
- **高风险变更**：蓝绿部署 (Blue-Green) 或 金丝雀发布 (Canary Release)。
- 生产环境的发布必须经过至少一人审批 + staging 环境验收通过。

## 3. 基础设施即代码 (Infrastructure as Code)
- 所有基础设施定义（服务器、网络、数据库、消息队列）须以代码形式管理（Terraform/Pulumi/CloudFormation）。
- 基础设施变更经 PR 评审后合并，由 CI/CD 自动执行。
- 禁止通过控制台手动点击创建/修改生产环境资源。

## 4. 容器与编排
- 应用须 Docker 容器化，`Dockerfile` 遵循最佳实践（多阶段构建、非 root 用户运行、最小基础镜像）。
- Kubernetes 部署清单（或 Helm Chart）须纳入版本控制。
- 资源限制（CPU/Memory Requests & Limits）必须配置。

## 5. 环境配置管理
- 不同环境的配置通过环境变量或专用配置服务注入。
- 配置文件中禁止出现任何环境特定的硬编码值。
- 敏感配置（密钥、证书）通过 Secret Manager 管理，绝不存入代码仓库。
