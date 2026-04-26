---
description: 自动化审查项目文档的完整性与准确性
---

# 文档审计工作流 (Documentation Audit)

定期检查项目文档的完整性、时效性和准确性。

## 步骤指南

1. **README 完整性检查**
   - 验证 README.md 是否包含 `documentation-standards.md` 中要求的最低信息：
     - 项目简介 ✅/❌
     - 快速启动命令 ✅/❌
     - 架构图 ✅/❌
     - 目录结构说明 ✅/❌
     - 环境变量列表 ✅/❌
     - 贡献指南 ✅/❌
   - 给出 README 完整性评分（0-100%）。

2. **API 文档覆盖率**
   - 扫描所有 Controller/Router 定义的端点。
   - 检查是否存在对应的 OpenAPI/Swagger 文档或 Markdown 说明。
   - 产出未覆盖端点清单。

3. **注释覆盖率**
   - 扫描所有公开的 (public/exported) 函数和类。
   - 统计有效 JSDoc/JavaDoc 注释的覆盖率。
   - 标记缺失注释的高复杂度函数（优先级最高）。

4. **ADR 审查**
   - 检查项目中是否存在 `docs/adr/` 目录。
   - 验证近期的重要架构变更是否有对应的 ADR 记录。
   - 标记状态为 "Proposed" 超过 30 天未决议的 ADR。

5. **CHANGELOG 时效性**
   - 对比最新的 Git Tag/Release 日期与 CHANGELOG 最后更新日期。
   - 如果存在已发布但未在 CHANGELOG 中记录的版本，标记为遗漏。

6. **报告产出**
   - 产出《文档审计报告》，各项以评分 + 具体缺失清单呈现。
   - 可调用 `documentation-gen` 技能自动补全发现的缺失。
