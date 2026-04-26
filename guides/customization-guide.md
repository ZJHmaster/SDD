# 企业定制指南 (Customization Guide)

本指南帮助不同行业、不同规模、不同技术栈的企业将 SDD 框架定制为适合自身的标准体系。

## 1. 定制原则
- **增量定制**：在 SDD 基础规范之上**叠加**企业特有规则，而非修改基础规范。
- **兼容性**：定制后的规范不得与 SDD 核心规范产生矛盾。
- **可识别性**：企业自定义的规则须使用明确的标记（如 `[CUSTOM]` 前缀），便于后续与 SDD 基线合并。

## 2. 按行业定制

### 金融 / 银行
追加规范：
- `standards/` ← 新增"交易幂等性设计规范"
- `compliance/` ← 新增"等保三级合规清单"、"反洗钱 (AML) 数据标记规则"
- `governance/` ← SLA 调整为 99.99% (四个九)
- `standards/error-handling.md` ← 追加"资金操作双向对账"容错要求

### 医疗健康
追加规范：
- `compliance/` ← 新增"HIPAA 合规清单"（美国市场）、"卫生健康信息数据分级保护标准"
- `standards/data-governance.md` ← 追加"患者数据特殊保护条款"
- `governance/` ← ADR 中增加"伦理委员会审查"字段

### 电商 / 零售
追加规范：
- `standards/performance-standards.md` ← 调整为高并发场景基线（大促期间 10x 峰值）
- `standards/` ← 新增"库存一致性与分布式锁规范"
- `.agents/skills/` ← 新增"促销规则引擎审查"技能

### 政务 / 公共服务
追加规范：
- `standards/accessibility-i18n.md` ← 将无障碍等级提升至 WCAG 2.1 AAA
- `compliance/` ← 新增"国产化适配清单"（信创要求）
- `governance/` ← 变更管理流程对接政务审批系统

## 3. 按技术栈定制

### 扩展 `.agents/skills/`
在 `skills/` 目录下创建框架专属的技能：
```
.agents/skills/
├── spring-boot/SKILL.md        # Spring Boot 特定最佳实践
├── nestjs/SKILL.md             # NestJS 特定最佳实践
├── flutter/SKILL.md            # Flutter 特定最佳实践
└── golang/SKILL.md             # Go 特定最佳实践
```

### 扩展 `templates/`
```
templates/
├── spring-boot-service/        # Spring Boot 微服务模板
├── nextjs-app/                 # Next.js 全栈模板
├── flutter-app/                # Flutter 移动端模板
└── go-service/                 # Go 微服务模板
```

## 4. 按团队规模定制

### 小团队 (≤ 10 人)
- 简化 RACI 矩阵（合并角色）。
- Code Review 可由 AI Agent 替代部分人工审核。
- 降低 ADR 强制性（仅重大决策记录）。

### 大团队 (50+ 人)
- 引入架构委员会 (Architecture Board)。
- 强化 `governance/change-management.md` 审批层级。
- 按产品线分设 SDD Owner 角色，负责该产品线的规范执行。

## 5. 定制步骤
1. Fork SDD 基线仓库到企业内部私有仓库。
2. 在各目录下创建 `_custom/` 子目录存放企业特有规范。
3. 在 `README.md` 中注明基线版本和定制内容索引。
4. 定期（每季度）与 SDD 基线仓库同步更新。
