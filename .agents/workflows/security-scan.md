---
description: 自动化安全漏洞扫描与合规检查
---

# 安全扫描工作流 (Security Scan)

端到端的自动化安全审查流程，整合代码级和依赖级的安全检测。

## 步骤指南

1. **静态应用安全测试 (SAST)**
   - 调用 `error-detection` 技能，扫描目标代码中的安全漏洞：
     - SQL/NoSQL 注入风险
     - XSS 跨站脚本漏洞
     - 硬编码凭证（密码、API Key、Token）
     - 不安全的加密方法（MD5/SHA-1 用于密码存储）
     - 路径遍历漏洞
   - 产出按 CRITICAL/HIGH/MEDIUM/LOW 分级的漏洞报告。

2. **依赖供应链扫描 (SCA)**
   - 扫描 `package.json`/`pom.xml`/`requirements.txt` 等依赖清单。
   - 匹配已知 CVE 漏洞数据。
   - 检查许可证合规性（标记 GPL/AGPL 等限制性许可）。

3. **配置安全审查**
   - 检查 Docker 镜像是否以 root 运行。
   - 验证 CORS、CSP、HSTS 等 HTTP 安全头配置。
   - 审查环境变量中是否有默认密码（如 `password=admin`）。

4. **合规基线对照**
   - 将扫描结果与 `standards/security-standards.md` 和 `compliance/` 目录下的合规清单进行交叉验证。
   - 产出合规差距报告 (Gap Analysis)。

5. **修复指引**
   - 对于每个发现的漏洞，提供具体的修复代码片段或配置调整建议。
   - CRITICAL 级别漏洞标记为"必须在下一次发布前修复"。
