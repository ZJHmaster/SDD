# 业务文档编写标准 (Business Documentation Standards)

## 1. 定位与价值
业务文档不是"给领导看的汇报材料"，而是面向 AI 和开发团队的**结构化业务知识输入源**。它回答的核心问题是："系统为什么存在？它为用户解决了什么问题？"

## 2. 业务文档分类体系

| 文档类型 | 缩写 | 编写时机 | 负责角色 | 受众 |
|---------|:---:|---------|---------|------|
| 业务领域概览 | BDO | 项目/模块立项时 | 产品经理 + 架构师 | 全体 |
| 业务需求规格 | BRS | 每个迭代/版本 | 产品经理 | PM/开发/测试/AI |
| 业务规则清单 | BRL | 随需求新增/变更 | 产品经理 + 业务方 | 开发/AI |
| 业务流程图 | BPF | 流程新增/重构时 | 产品经理 | 全体 |
| 业务术语表 | BGS | 项目初始化 + 持续维护 | 产品经理 | 全体 (尤其AI/新人) |

## 3. 结构化模板

### 3.1 业务需求规格 (BRS) 模板
每份业务需求文档必须包含以下结构化头部（支持 AI 机器解析）：

```yaml
---
docType: BRS
docId: BRS-ORD-2026-001
title: 订单超时自动取消功能
domain: 订单域
version: 1.0
status: Approved  # Draft | Reviewing | Approved | Deprecated
author: 张三
createDate: 2026-04-26
relatedBRS: [BRS-ORD-2026-000]    # 关联的前置需求
relatedADR: [ADR-0015]            # 关联的架构决策
traceability:
  modules: [order-service/src/domain/services/OrderTimeoutService]
  apis: [POST /api/v1/orders/{id}/cancel]
  tables: [orders, order_status_logs]
  tests: [test/unit/order-timeout.test.ts]
tags: [订单, 超时, 自动化, 定时任务]
---
```

### 3.2 文档正文结构
```markdown
## 1. 业务背景与目标
[为什么需要这个功能？解决什么用户/业务问题？]

## 2. 用户故事 (User Stories)
- 作为【角色】，我希望【动作】，以便【目的】

## 3. 业务规则 (Business Rules)
- BR-001: [规则描述，如"超过30分钟未支付的订单自动取消"]
- BR-002: [规则描述]

## 4. 核心流程 (用 Mermaid 绘制)
[Mermaid 流程图]

## 5. 数据要求
[涉及的数据实体、字段及其业务含义]

## 6. 非功能性要求
[性能/可用性/安全等约束]

## 7. 验收标准 (Acceptance Criteria)
- AC-001: Given [前置条件], When [操作], Then [预期结果]

## 8. 影响范围
[影响的现有功能/模块/上下游系统]
```

### 3.3 业务规则清单 (BRL) 模板
```yaml
---
docType: BRL
domain: 订单域
lastUpdated: 2026-04-26
---
```

| 规则ID | 规则描述 | 触发条件 | 关联BRS | 实现模块 |
|--------|---------|---------|---------|---------|
| BR-ORD-001 | 未支付订单超过30分钟自动取消 | 订单状态=待支付 AND 创建时间>30min | BRS-ORD-2026-001 | OrderTimeoutService |

### 3.4 业务术语表 (BGS) 模板
```yaml
---
docType: BGS
domain: 全局
lastUpdated: 2026-04-26
---
```

| 术语 | 英文 | 定义 | 同义词 | 所属领域 |
|------|------|------|--------|---------|
| 订单 | Order | 用户对一组商品发起购买意向的承载实体 | 工单(内部旧称) | 订单域 |

## 4. 存储与组织规范
- 业务文档统一存放在项目的 `docs/biz/` 目录下。
- 按领域子目录组织：`docs/biz/order/`、`docs/biz/user/`、`docs/biz/payment/`。
- 文件名格式：`<docType>-<domain>-<YYYY>-<NNN>.md`。
- 业务文档与代码同仓管理，随代码一起版本化。

## 5. 维护规则
- 需求变更时，对应的 BRS **必须同步更新**。禁止"需求变了但文档没跟上"的情况。
- 废弃的需求文档标记 `status: Deprecated`，不删除（保留历史追溯）。
- 每月运行 `/business-audit` 工作流检查文档与代码的一致性。

## 6. 与 AI Agent 的衔接
- 结构化的 YAML front matter 使 AI 可以精准检索需求文档，而不必全文扫描。
- `traceability` 字段让 AI 能直接从需求跳转到对应代码、API、数据表和测试用例。
- `tags` 字段支持跨项目的业务模式检索。
