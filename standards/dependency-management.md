# 依赖与供应链管理规范 (Dependency Management)

## 1. 版本锁定策略
- 生产环境的依赖必须使用**精确版本号** (Exact Version Pinning)，禁止使用 `^` 或 `~` 通配范围。
- Lock 文件（`package-lock.json`, `pom.xml`, `go.sum`）必须提交至版本控制。
- 依赖升级是一个主动、有计划的工程行为，不应由构建工具的自动解析隐式触发。

## 2. 依赖引入评审
在向项目添加新的第三方依赖前，须回答以下审查问题：
1. **必要性**：是否可以用现有依赖或少量自研代码替代？
2. **活跃度**：该库最近 6 个月是否有 commit？Issues 响应是否及时？
3. **社区规模**：GitHub Stars / npm 周下载量 / Maven Central 引用数是否达到合理的信任门槛？
4. **许可证合规**：是否为允许商用的许可证（MIT, Apache-2.0, BSD）？如涉及 GPL/AGPL 类许可证需法务审查。
5. **安全记录**：是否有历史 CVE 漏洞？当前版本是否是安全版本？
6. **包体积影响**：特别是前端库，引入后对 Bundle Size 的影响是否可接受？

## 3. 自动化安全扫描
- 项目 CI 管线必须集成依赖漏洞扫描工具：
  - Node.js：`npm audit` / Snyk
  - Java：OWASP Dependency-Check / Dependabot
  - Python：`pip-audit` / Safety
  - Go：`govulncheck`
- 发现 `HIGH` 或 `CRITICAL` 级别漏洞时，CI 管线必须失败并阻断合并。

## 4. 依赖升级节奏
| 优先级 | 触发条件 | 响应时间 |
|--------|---------|---------|
| 紧急 | 安全漏洞 (CRITICAL/HIGH CVE) | 24 小时内修复 |
| 高 | 主要框架大版本 EOL | 1 个季度内迁移 |
| 中 | 性能优化或重要 Bug 修复 | 下一个 Sprint |
| 低 | 常规次版本/补丁版本更新 | 每月批量升级一次 |

## 5. 内部私有包库
- 公司内部共享的工具包/SDK 应发布到私有 Registry（如 Verdaccio, Nexus, Artifactory）。
- 内部包须和外部三方依赖使用相同的版本管理与发布规范 (Semantic Versioning)。
