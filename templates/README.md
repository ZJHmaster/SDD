# 可复用项目模板 (Project Templates)

本目录包含面向不同应用类型的标准化项目脚手架模板。每个模板已内置 SDD 全套编码规范和配置，保证项目开箱即合规。

## 可用模板

| 模板 | 适用场景 | 包含内容 |
|------|---------|---------|
| [`microservice/`](./microservice/) | 后端微服务 / API 服务 | 分层目录结构、统一错误处理、健康检查、Docker、CI 配置 |
| [`frontend-app/`](./frontend-app/) | 前端 SPA 应用 | 组件化目录、i18n 配置、性能监控接入、a11y 基线 |
| [`library-package/`](./library-package/) | 内部公共库/SDK | 构建配置、API 导出规范、版本发布脚本、README 模板 |

## 使用方式

### 方法 1：手动复制
```bash
# 创建新的微服务项目
cp -r templates/microservice/ ../my-new-service/
cd ../my-new-service
# 按 README 说明初始化
```

### 方法 2：通过 AI Agent
告诉你的 AI 开发助手：
> "请基于 SDD 微服务模板，为我创建一个用户管理服务的项目骨架。"

AI 将调用 `code-generation` 技能，结合模板定义和你的业务需求，自动生成完整代码。

## 模板扩展指南
团队可以基于业务需要扩展新的模板：
1. 在 `templates/` 下创建新目录。
2. 包含标准目录结构、配置文件和 README。
3. 确保符合 `standards/` 下的所有规范。
4. 提交 PR 经架构评审后合并。

### 建议的扩展模板
- `bff-gateway/` — BFF 网关层模板
- `batch-job/` — 批处理/定时任务应用模板
- `event-consumer/` — 消息队列消费者服务模板
- `mobile-app/` — 移动端 App 模板 (React Native / Flutter)
