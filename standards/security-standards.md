# 企业级安全编码标准 (Security Standards)

## 1. OWASP Top 10 防御
所有开发人员在编写代码时必须默认防御以下常见攻击：

### 1.1 注入防护 (Injection)
- **SQL 注入**：严禁字符串拼接构造 SQL。必须使用 ORM 框架或参数化查询 (Prepared Statements)。
- **命令注入**：避免应用直接调用系统 Shell 层。确需执行命令时，须对参数进行白名单转义校验。
- **XSS (跨站脚本)**：所有输出到客户端的内容必须经过上下文感知的编码（HTML Entity Encode）。前端应启用 CSP (Content Security Policy) 头。

### 1.2 身份验证与会话管理
- **密码存储**：禁止明文或使用弱哈希（如 MD5、SHA-1）。必须使用 `Bcrypt` 或 `Argon2` 配合强随机盐值 (Salt)。
- **会话/Token**：
  - JWT Secrets 至少 256位（32字节）随机字符。
  - Cookie 必须标清 `HttpOnly` 和 `Secure` 属性。
  - 登录接口必须配置针对 IP 或用户的暴力破解防范（Rate Limiting）。

## 2. 敏感数据与配置管理
- 代码库中**绝对禁止**硬编码任何密码、API 密钥、私钥和数据库连接串。
- 如发现硬编码的敏感凭据，视为严重安全事故。
- 机密信息应通过环境变量注入配置，或使用集中式的 Secret Management Service (如 HashiCorp Vault、AWS Secrets Manager)。

## 3. 文件上传安全
- 文件上传接口必须验证真实的文件头 Magic Bytes，单纯后缀名校验无效。
- 将用户上传文件存储在无执行权限的专有隔离目录（或对象存储如 S3），通过 CDN 提供访问。
- 不得使用用户指定的文件名直接保存文件，防止目录遍历攻击 (`../../`)。

## 4. 数据最小化与合规
- 日志中禁止记录明文密码、个人身份可识别信息 (PII)（如信用卡号、完整身份证等）。若需记录，须进行脱敏 (Masking)。
- 对外接口返回实体时，使用 DTO (Data Transfer Object) 隔离领域层，确保不把无用的敏感字段泄漏给外部调用方。

## 5. 第三方依赖管理 (Supply Chain Security)
- 使用如 `npm audit` 或 `Dependabot` 定期扫描引用的三方包已知漏洞。
- 拒绝引入停止维护长达两年以上或社区评价极低的三方库。

## 6. AI Agent 辅助安全检查
集成 `.agents/workflows/security-scan.md` 流程。Agent 带有专门的安全检测技能 (`.agents/skills/error-detection`)，能够在 Code Review 阶段通过静态语法分析提示潜在的安全隐患。
