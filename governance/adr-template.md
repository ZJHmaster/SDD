# 架构决策记录模板 (ADR Template)

> 每个重要的技术决策必须通过 ADR 正式记录。
> ADR 一旦 "Accepted"，不可修改，只能通过新 ADR 取代。

---

## ADR-XXXX: [决策标题]

**状态**：[Proposed | Accepted | Deprecated | Superseded by ADR-YYYY]

**日期**：YYYY-MM-DD

**决策者**：[姓名 / 角色]

---

### 上下文 (Context)
> 描述促成该决策的背景情况、业务需求和技术约束。

[在此填写]

### 决策 (Decision)
> 清晰陈述所做的技术决策。

我们决定 [采用/使用/实施] ________，因为 ________。

### 考虑过的替代方案 (Alternatives Considered)

| 方案 | 优点 | 缺点 | 结论 |
|------|------|------|------|
| 方案 A | ... | ... | 采纳 ✅ |
| 方案 B | ... | ... | 放弃 ❌ |
| 方案 C | ... | ... | 放弃 ❌ |

### 后果 (Consequences)

**正面影响**：
- [列出此决策带来的好处]

**负面影响 / 权衡 (Trade-offs)**：
- [列出此决策的缺点或需要额外付出的成本]

**风险**：
- [列出可能的风险及缓解措施]

### 相关 ADR
- 取代了：ADR-XXXX（如适用）
- 被取代于：ADR-YYYY（如适用）
- 关联：ADR-ZZZZ

---

## 使用指南
1. 将此模板复制到项目的 `docs/adr/` 目录。
2. 按递增编号命名：`ADR-0001-use-postgresql.md`。
3. 新的 ADR 须经团队技术负责人评审后将状态改为 "Accepted"。
4. 禁止修改已 Accepted 的 ADR 内容，如需变更需创建新的 ADR 并将旧 ADR 标记为 "Superseded"。
