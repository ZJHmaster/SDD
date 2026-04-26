# 数据库设计与管理规范 (Database Standards)

## 1. Schema 设计原则
### 1.1 命名
- 表名和列名统一使用 `snake_case`。
- 表名使用**复数名词**：`orders`, `user_profiles`。
- 外键列命名为 `<被引用表单数>_id`，如 `order_id`, `user_id`。
- 索引命名规范：`idx_<表名>_<列名1>_<列名2>`，如 `idx_orders_user_id_status`。

### 1.2 必备元字段
每个业务表必须包含以下四个审计字段：
```sql
id           BIGINT PRIMARY KEY AUTO_INCREMENT,
created_at   TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
updated_at   TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
is_deleted   TINYINT(1) NOT NULL DEFAULT 0   -- 逻辑删除标记
```

### 1.3 规范化与反规范化
- 业务主表至少满足第三范式 (3NF)。
- 仅在已被证实存在性能瓶颈的查询场景中才可进行受控的反规范化（冗余字段），且必须在 ADR 中记录决策原因和数据同步策略。

## 2. Migration 管理
- 所有数据库结构变更（DDL）必须以版本化的 Migration 文件提交（如 Flyway/Liquibase/Alembic/Prisma），严禁直接在生产环境手动执行 SQL。
- Migration 文件编号格式：`V<YYYYMMDD>_<HHmmss>__<description>.sql`。
- 每个 Migration 必须包含 `UP` 和 `DOWN` 两个方向的脚本（可回滚设计）。

## 3. 索引策略
- 主键自动建立聚簇索引。
- 频繁出现在 `WHERE`, `JOIN`, `ORDER BY` 中的列应建立索引。
- 联合索引遵循最左前缀匹配原则。
- 在超过 500 万行规模的大表上新增索引前，须在从库或预发布环境评估加锁时间。

## 4. 安全与数据保护
- 数据库账号权限最小化：应用账号仅授予 DML 权限（SELECT/INSERT/UPDATE/DELETE），DDL 权限由 DBA 专属账号持有。
- 敏感字段（手机号、身份证、银行卡号）在数据库层面实施加密存储或脱敏处理。
- 定期执行数据库备份验证（恢复演练至少每季度一次）。

## 5. 查询规范
- 严禁 `SELECT *`，必须显式指定所需列。
- 批量操作推荐分批执行（如每批 500-1000 条），避免长事务锁表。
- ORM 层必须开启慢查询日志，阈值建议设为 200ms。
