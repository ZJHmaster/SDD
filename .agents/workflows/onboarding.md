---
description: 新成员技术入职引导自动化流程
---

# 新人接入工作流 (Onboarding)

帮助新加入团队的开发者快速了解项目技术栈、工程规范和工作方式。

## 步骤指南

1. **环境初始化引导**
   - 检测新成员本地环境配置（Node/Java/Python 版本、包管理器、IDE 配置）。
   - 引导安装和配置必要工具链。
   - 确认能够成功 clone、build、run 项目。

2. **规范认知构建**
   - 引导阅读以下核心文档，并进行要点提示：
     - `standards/code-style-guide.md` — 代码怎么写
     - `standards/naming-conventions.md` — 变量怎么命名
     - `standards/git-workflow.md` — 代码怎么提交
     - `standards/review-checklist.md` — 代码怎么审查
   - 可交互式地提问与回答，确保理解到位。

3. **架构认知构建**
   - 产出项目当前的架构概览图。
   - 解释核心模块的职责和数据流。
   - 说明分层结构和关键设计决策（引導阅读 ADR 记录）。

4. **首次贡献引导**
   - 推荐一个适合新人的待办工单（标记为 `good-first-issue`）。
   - 演示完整的开发流程：拉取分支 → 编码 → 提交 → 触发 CI → 提交 MR。
   - 在新人首次提交时主动运行 `/standards-check` 和 `/code-review` 提供友好反馈。

5. **文化融入**
   - 解释团队的协作方式和沟通规范。
   - 介绍定期的技术分享会和代码评审节奏。
   - 指引 `guides/faq.md` 回答常见问题。
