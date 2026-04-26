# SDD - Software Development Discipline
### 企业级 AI 编程范式解决方案

> 覆盖软件全生命周期的工程化治理框架，通过 AI 智能代理赋能团队实现编码质量、安全合规和工程效率的全面提升。
> 支持跨行业定制（金融/医疗/电商/政务），从小团队到百人规模渐进式采纳。

---

## 📋 框架总览与全生命周期链路

本框架包含 **7 大模块**，共计 **68 个文件**，覆盖从需求分析到生产运维的完整生命周期。

### 🔄 全生命周期使用图谱

```mermaid
graph TD
    classDef domain fill:#e3f2fd,stroke:#1976d2,stroke-width:2px;
    classDef standard fill:#f3e5f5,stroke:#7b1fa2;
    classDef agent fill:#e8f5e9,stroke:#388e3c;
    classDef gov fill:#fff3e0,stroke:#f57c00;

    subgraph Phase1 [1. 需求与架构阶段]
        A1[业务需求输入] --> S1(业务文档标准<br>business-documentation)
        S1 --> A2(追溯矩阵规范<br>traceability-matrix)
        
        A2 -.->|AI 赋能| AG1{{business-analysis<br>AI拆解任务}}:::agent
        A2 -.->|AI 赋能| AG2{{requirement-traceability<br>自动追溯}}:::agent
        
        ADR(架构决策<br>adr-template) --> ARCH(架构设计与选型<br>architecture-patterns)
    end
    class Phase1 domain

    subgraph Phase2 [2. 开发与编码阶段]
        ARCH --> DEV[代码编写]
        DEV --> S2(代码风格<br>code-style-guide)
        DEV --> S3(命名约定<br>naming-conventions)
        DEV --> S4(API设计<br>api-design-guide)
        DEV --> S5(数据管理<br>database-standards)
        
        DEV -.->|开箱即用| TPL[项目脚手架 Templates]
        DEV -.->|AI 赋能| AG3{{code-generation<br>脚手架/CRUD生成}}:::agent
    end
    class Phase2 domain

    subgraph Phase3 [3. 验证与审查阶段]
        DEV --> TEST[测试与合规审查]
        TEST --> S6(测试规范<br>testing-standards)
        TEST --> S7(安全编码<br>security-standards)
        TEST --> S8(依赖审计<br>dependency-management)
        TEST --> C1(GDPR/数据分级<br>Compliance)
        
        TEST -.->|AI 赋能| AG4{{code-review<br>智能评审}}:::agent
        TEST -.->|AI 赋能| AG5{{security-scan<br>漏洞扫描}}:::agent
    end
    class Phase3 domain

    subgraph Phase4 [4. 部署与运维阶段]
        TEST --> DEPLOY[CI/CD 部署]
        DEPLOY --> S9(DevOps管线<br>devops-cicd)
        DEPLOY --> G1(分级部署审批<br>deployment-governance):::gov
        
        DEPLOY -.->|变更预判| AG6{{impact-analysis<br>影响影响分析}}:::agent
        
        DEPLOY --> OPS[线上监控]
        OPS --> S10(日志与监控<br>logging-monitoring)
        OPS --> S11(异常与容错<br>error-handling)
        OPS --> G2(SLA/故障分级<br>incident-severity):::gov
        
        OPS -.->|AI 赋能| AG7{{performance-profiling<br>性能剖析}}:::agent
    end
    class Phase4 domain

    %% 阶段流转关系
    Phase1 ==> Phase2 ==> Phase3 ==> Phase4
    
    %% 重构/优化闭环
    Phase4 -.->|发现技术债| OPS_L[演进重构]
    OPS_L -.->|遗留系统改造| AG8{{legacy-transform<br>AI代码重构}}:::agent
    AG8 -.-> Phase2

    %% 规约说明
    class S1,A2,ADR,ARCH,S2,S3,S4,S5,S6,S7,S8,S9,S10,S11,C1 standard
```

### 🗂 目录结构明细

| 模块 | 目录 | 文件数 | 职责 |
|------|------|:------:|------|
| 📐 工程规范 | [`standards/`](./standards/) | 19 | 编码风格、架构、安全、测试、数据库、业务文档等全维度标准 |
| 🤖 AI 技能库 | [`.agents/skills/`](./.agents/skills/) | 12 | 代码生成/重构/优化/安全检测 + 业务分析/影响预判 |
| ⚙️ 智能工作流 | [`.agents/workflows/`](./.agents/workflows/) | 14 | 自动化代码评审、工程审计、需求追溯、发布管理等 |
| 🏗️ 项目模板 | [`templates/`](./templates/) | 3 类 | 微服务/前端/公共库开箱即用的项目骨架 |
| 🔒 合规框架 | [`compliance/`](./compliance/) | 3 | GDPR/个保法清单、数据分级、审计追踪 |
| 🏛️ 工程治理 | [`governance/`](./governance/) | 7 | 技术雷达、ADR、RACI、故障分级、SLA、变更管理、部署治理 |
| 📚 实施指南 | [`guides/`](./guides/) | 8 | 快速上手、团队导入、培训、定制、成熟度模型、ROI、业务文档实施 |

共计 **68 个文件**，覆盖从需求分析到生产运维的完整生命周期。

---

## 🚀 快速开始

### 1. 最小起步集
如果你的团队刚接触 SDD，从这里开始：
```
阅读：standards/code-style-guide.md
阅读：standards/naming-conventions.md
阅读：standards/git-workflow.md
执行：/standards-check  ← 让 AI 检查你的代码
```

### 2. 进阶采纳
```
阅读：standards/architecture-patterns.md
阅读：standards/security-standards.md
阅读：standards/testing-standards.md
执行：/code-review  ← 让 AI 做全面的代码评审
```

### 3. 业务文档标准化（当前重点）
```
阅读：standards/business-documentation.md    ← 业务文档编写标准
阅读：standards/traceability-matrix.md       ← 需求-代码追溯规范
阅读：guides/business-doc-implementation.md  ← 分步实施手册
执行：/business-audit                        ← 业务文档审计
执行：/requirement-traceability              ← 需求追溯扫描
```

### 4. 全面落地
```
阅读：guides/team-adoption.md     ← 团队导入策略
阅读：guides/maturity-model.md    ← 评估当前水平
执行：/project-health             ← 项目健康度检查
执行：/engineering-audit           ← 工程化审计
```

详细入门指南请查看 [`guides/quick-start.md`](./guides/quick-start.md)。

---

## 🤖 可用的 AI 斜杠命令

### 核心工程流程
| 命令 | 功能 |
|------|------|
| `/standards-check` | 代码规范一致性检查 |
| `/code-review` | 智能代码评审 |
| `/security-scan` | 安全漏洞扫描 |
| `/project-health` | 项目健康度评估 |
| `/engineering-audit` | 全面工程审计 |

### 业务与需求追溯
| 命令 | 功能 |
|------|------|
| `/business-audit` | 业务文档完整性与一致性审计 |
| `/requirement-traceability` | 需求-代码-测试追溯扫描 |

### 发布与运维
| 命令 | 功能 |
|------|------|
| `/release-management` | 版本发布管理 |
| `/incident-response` | 故障响应复盘 |
| `/dependency-audit` | 依赖安全审计 |
| `/performance-profiling` | 性能瓶颈剖析 |

### 团队与文档
| 命令 | 功能 |
|------|------|
| `/onboarding` | 新人技术引导 |
| `/documentation-audit` | 文档完整性审计 |
| `/legacy-transform` | 存量代码改造 |

---

## 🏢 企业定制

SDD 框架支持按行业和团队规模定制。详见 [`guides/customization-guide.md`](./guides/customization-guide.md)：
- 金融/银行、医疗健康、电商零售、政务公共服务
- 小团队 (≤10人) 到大团队 (50+人) 的差异化配置

---

## 📊 投资回报

落地效果通过 DORA 指标 + 质量指标 + 效率指标量化度量。
详见 [`guides/roi-metrics.md`](./guides/roi-metrics.md)。

---

## 📝 许可
本框架为企业内部工程治理工具。请根据企业实际情况调整后使用。
