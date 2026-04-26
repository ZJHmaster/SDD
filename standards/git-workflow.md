# Git 工作流与提交规范 (Git Workflow)

## 1. 分支策略 (Branching Strategy)

### 1.1 推荐：基于主干开发 (Trunk-Based) + 短命特性分支
适用于持续集成/持续交付团队。核心原则是：所有开发者须**每天至少向主干合并一次**。

```
main (永在可发布状态)
 ├── feature/USER-1234-add-payment-method   ← 生命周期 ≤ 2天
 ├── feature/USER-5678-fix-login-timeout    ← 生命周期 ≤ 2天
 ├── hotfix/PROD-999-critical-data-loss     ← 紧急修复分支
 └── release/v2.3.0                         ← 可选，仅需发布裁剪时创建
```

### 1.2 分支命名规范
| 类型 | 格式 | 范例 |
|------|------|------|
| 特性 | `feature/<TICKET-ID>-<简短描述>` | `feature/ORD-123-add-refund-logic` |
| 修复 | `fix/<TICKET-ID>-<简短描述>` | `fix/ORD-456-null-pointer-on-pay` |
| 热修复 | `hotfix/<TICKET-ID>-<简短描述>` | `hotfix/PROD-789-data-corruption` |
| 发布 | `release/v<MAJOR.MINOR.PATCH>` | `release/v2.3.0` |

## 2. Commit Message 规范 (Conventional Commits)
团队强制遵循 [Conventional Commits](https://www.conventionalcommits.org/) 格式。

### 2.1 格式
```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

### 2.2 Type 枚举
| Type | 含义 | 是否触发版本升级 |
|------|------|:---:|
| `feat` | 新增功能 | minor |
| `fix` | 修复缺陷 | patch |
| `docs` | 仅文档变更 | - |
| `style` | 格式调整(不影响逻辑) | - |
| `refactor` | 重构(不改变外部行为) | - |
| `perf` | 性能优化 | patch |
| `test` | 添加/修正测试 | - |
| `chore` | 构建流程/辅助工具变动 | - |
| `ci` | CI/CD 配置变更 | - |
| `BREAKING CHANGE` | 破坏性变更 | major |

### 2.3 示例
```
feat(payment): 新增微信支付渠道对接

- 实现 WeChatPayGateway 适配器
- 添加签名验证与回调处理
- 编写单元测试覆盖核心签名逻辑

Refs: ORD-1234
```

## 3. Pull Request / Merge Request 模板
每次创建 PR/MR 须包含以下内容：
- **关联工单号**
- **变更类型**（feat/fix/refactor/...）
- **变更描述**：用两三句话概括此 PR 的核心目的
- **测试验证**：说明通过了哪些测试（自测截图/自动化报告链接）
- **自检清单**：确认已通过 `/standards-check`
- **影响范围**：标注是否涉及数据库变更、配置变更、外部依赖升级

## 4. 保护规则
- `main` 分支启用分支保护：禁止直接推送，至少需要一位 Reviewer 批准。
- 合并前须通过完整的 CI 管线（Lint + 单元测试 + 安全扫描）。
- Commit 历史推荐 **Squash Merge**，保持主干 git log 简洁。
