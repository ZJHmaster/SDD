# 常见问题 FAQ

## 关于 SDD 框架

### Q: SDD 是什么？
SDD (Software Development Discipline) 是一套企业级 AI 编程范式解决方案。它整合了编码规范、AI 技能库、智能代理工作流、项目模板、合规框架和工程治理，覆盖软件开发全生命周期。

### Q: SDD 适用于什么语言/框架？
SDD 的核心规范和设计原则是**语言无关**的。它适用于 Java、TypeScript/JavaScript、Python、Go、C# 等主流语言。语言特定的规则可在各标准文档中按章节扩展。

### Q: 引入 SDD 会不会降低开发效率？
短期内会有少量学习成本。但中长期来看：
- AI Agent 自动化了代码评审和规范检查，实际上加速了流程。
- 统一的规范减少了团队内部沟通成本和争论。
- 项目模板消除了重复的初始化工作。
- 减少的线上缺陷和返工带来的时间节省远超规范学习的投入。

### Q: 我是否必须采纳全部内容？
不需要。SDD 设计为**渐进式采纳**：
- 最小起步集：`code-style-guide` + `naming-conventions` + `git-workflow` + `/standards-check` 工作流
- 逐步添加安全、测试、架构等模块
- 参见 `guides/team-adoption.md` 的三阶段导入策略

## 关于 AI Agent

### Q: AI Agent 会替代人工 Code Review 吗？
不会。AI Agent 是人工评审的**增强和前哨**，它负责拦截低级的规范违规和安全漏洞，使人工评审者能聚焦于业务逻辑和架构设计等更高层面的讨论。

### Q: AI Agent 的建议一定是对的吗？
不一定。AI 的建议是基于规范文档和代码分析的参考。开发者应保持专业判断力。如果 AI 的建议与业务上下文冲突，以业务实际为准，但须在评审记录中说明原因。

### Q: 如何添加自定义的 AI 技能？
1. 在 `.agents/skills/` 下创建新目录。
2. 创建 `SKILL.md` 文件，包含 YAML frontmatter（name, description）和 Markdown 指令。
3. 在指令中明确技能的职责、分析维度、操作规范。
4. 参考现有技能的格式即可。

## 关于团队落地

### Q: 团队成员抵触规范怎么办？
常见原因及应对：
1. **觉得多此一举** → 用 `guides/training-material.md` 中的灾难场景课来建立安全意识。
2. **觉得增加工作量** → 展示 AI Agent 的自动化能力，让他们体验而非想象。
3. **习惯了旧方式** → 不要一步到位，按 `team-adoption.md` 的三阶段计划缓慢推进。

### Q: 如何度量 SDD 落地效果？
参见 `guides/roi-metrics.md`。核心指标包括：
- 线上缺陷密度变化率
- Code Review 周转时间
- 部署频率与变更失败率 (DORA 指标)
- 开发者满意度调查

### Q: 存量项目如何接入？
使用 `/legacy-transform` 工作流和 `legacy-migration` 技能进行渐进式改造。不要试图一步到位，优先从以下入手：
1. 接入 CI 管线 + `/standards-check`（最低成本）。
2. 为核心业务逻辑补充测试。
3. 逐步重构高风险模块。
