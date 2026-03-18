# Agent Skills

简体中文 | [English](./README.md)

为 AI 编程助手提供可复用技能指令集，扩展其专业能力。

## 概述

Skills 是一套精心设计的服务于 AI 编程助手的技能包。每个技能都定义在 `SKILL.md` 文件中，包含完整的指令集、工作流程和质量标准，帮助 AI 助手更高效地完成特定任务。

## 功能特性

### 开发工作流技能

**brainstorming**、**writing-plan** 和 **executing-plans** 是相互关联的技能，按顺序触发，形成从需求到实现的完整开发工作流：

```
brainstorming → writing-plan → executing-plans
```

**目标**：通过结构化、质量保证的流程，将用户想法转化为生产就绪的代码：
1. **探索与设计** - 理解需求并创建设计规格说明
2. **规划与文档** - 分解为细粒度、可测试的实施步骤
3. **执行与验证** - 严格执行并验证

#### brainstorming

任何创造性工作前的必经步骤。该技能提供：

- **需求探索**：通过协作对话理解用户意图、需求和设计方案
- **设计规格**：将创意转化为完整的设计规格说明
- **质量保证**：包含规格审阅循环和自动验证
- **工作流指导**：从背景探索到实施规划的逐步流程
- **项目初始化**：项目结构、基础设施决策和关键问题指导
- **技术选型**：系统性的技术选择评估框架
- **风险评估**：在设计阶段识别和评估潜在风险

**参考文档**：faq.md、project-initialization-guide.md、risk-assessment-template.md、spec-document-reviewer-prompt.md、spec-template.md、state-template.md、tech-selection-guide.md

#### writing-plan

多步骤任务的实施计划创建技能，提供以下能力：

- **上下文分析**：评估范围并识别独立子系统
- **文件结构规划**：设计清晰的边界和明确定义的接口
- **任务定义**：采用 TDD 方法的细粒度步骤
- **依赖管理**：识别并规划依赖安装
- **环境配置**：定义不同环境的策略
- **回滚策略**：为实施失败准备计划
- **审阅循环**：迭代审阅和质量检查点

**参考文档**：plan-document-reviewer-prompt.md、plan-template.md、patterns.md、planning-guides.md、change-management.md、quality-checklist.md、workflow-examples.md

#### executing-plans

包含审查检查点的实施计划执行技能，提供以下能力：

- **计划加载**：定位并加载书面实施计划
- **批判性审阅**：在执行前评估计划质量
- **严格执行**：完全按照文档记录执行每个步骤
- **验证检查**：在检查点运行所有指定的验证
- **阻碍处理**：遇到障碍时停止并寻求帮助
- **进度持久化**：使用任务标记追踪进度，支持中断后恢复
- **恢复机制**：从中断点恢复执行并验证

**参考文档**：completion-report-template.md、execution-state-template.md、workflow-examples.md

---

### 独立技能

#### code-commentator

代码注释补充与规范化专家，提供以下能力：

- **自动识别语言**：支持 JavaScript、TypeScript、Python、Java、Go、Rust 等多种编程语言
- **双语注释**：所有注释同时包含中英文说明
- **规范格式**：自动应用语言特定的注释风格（JSDoc、docstring 等）
- **完整性保证**：为函数、类、属性、枚举等代码元素添加完整注释

## 安装

使用 [vercel-labs/skills](https://github.com/vercel-labs/skills) CLI 工具安装技能：

```bash
# 安装所有技能
npx skills add https://github.com/supper-skills/skills

# 安装特定技能
npx skills add https://github.com/supper-skills/skills --skill doc-writer

# 安装到全局目录
npx skills add https://github.com/supper-skills/skills -g
```

## 使用方法

### 安装后自动激活

技能安装后，当您向 AI 助手发出相关指令时会自动激活：

```txt
用户：我想实现一个 TODO List 应用
```

此时 `brainstorming` 技能会自动激活，AI 助手将按照技能中定义的标准和流程，与您合作探索和设计 TODO List 应用的需求规格。

## 许可证

本项目采用 MIT 许可证。详见 [LICENSE](LICENSE) 文件。

## 相关链接

- [vercel-labs/skills](https://github.com/vercel-labs/skills) - Skills CLI 工具
- [skills.sh](https://skills.sh) - 发现更多技能
