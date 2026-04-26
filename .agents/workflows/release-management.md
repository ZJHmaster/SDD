---
description: 自动化版本发布管理与变更日志生成
---

# 发布管理工作流 (Release Management)

结构化的版本发布流程，确保每次发版的质量可控与可追溯。

## 步骤指南

1. **预发布检查**
   - 确认当前 `main` 分支 CI 管线全部通过（绿色）。
   - 运行 `/project-health` 获取最新健康度报告，确认无 CRITICAL 级别阻塞项。
   - 验证所有计划内的 JIRA/工单已关闭或移出当前版本范围。

2. **语义化版本号决策**
   - 根据自上个版本以来的 Commit 类型，自动推断版本号增量：
     - 包含 `BREAKING CHANGE` → Major 升级 (x.0.0)
     - 包含 `feat` → Minor 升级 (0.x.0)
     - 仅有 `fix`/`perf` → Patch 升级 (0.0.x)

3. **CHANGELOG 生成**
   - 调用 `documentation-gen` 技能，基于 Conventional Commits 自动生成结构化 CHANGELOG 内容块。
   - 插入到现有 CHANGELOG.md 顶部。

4. **创建 Release 分支/标签**
   - 建议创建 Git Tag: `v<MAJOR.MINOR.PATCH>`。
   - 如需发布裁剪，创建 `release/v<version>` 分支。

5. **发布后确认**
   - Staging 环境冒烟测试通过。
   - 生产环境部署后监控告警静默期观察（建议 30 分钟）。
   - 确认核心业务指标（订单量/支付成功率/错误率）无异常波动。

6. **回退预案**
   - 产出本次发布的回退步骤文档。
   - 如使用蓝绿/金丝雀部署，明确回退的流量切换操作。
