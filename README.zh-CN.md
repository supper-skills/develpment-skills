# Development Skills

简体中文 | [English](./README.md)

**将你的想法变为可落地的项目。** 一句话需求，即刻开始构建。

## 这个技能包能做什么

Development Skills 通过结构化、质量保证的工作流程，将你的想法转化为完整实现的项目。只需描述你想构建什么，AI 助手就会引导你从概念到完成。

```
你的想法 → 设计规格说明 → 实施计划 → 可运行代码
```

## 核心工作流

技能包提供三个相互关联的技能，无缝协作：

### 1. brainstorming

**当你说**："我想创建一个 TODO List 应用"

AI 助手将：
- 与你协作探索需求和目标
- 提出多个方案并进行权衡分析
- 创建完整的设计规格说明文档
- 确保在编写任何代码前达成共识

### 2. writing-plan

**设计通过后**，AI 助手将：
- 将规格说明分解为细粒度的实施步骤
- 定义精确的文件结构和职责
- 创建测试驱动的开发任务
- 准备全面的实施计划

### 3. executing-plans

**计划确认后**，AI 助手将：
- 严格按照文档记录执行每个步骤
- 在检查点运行所有验证和测试
- 追踪进度并处理阻碍
- 生成完成报告

## 示例

```txt
用户：我想创建一个支持 markdown 的博客平台

AI：[激活 brainstorming 技能]
    让我更好地理解您的需求...
    这个平台的主要用户是谁？
    [协作对话继续...]

    [创建设计规格说明]
    [激活 writing-plan 技能]
    [创建实施计划]
    [激活 executing-plans 技能]
    [实施功能]

    ✅ 您的博客平台已就绪！
```

## 附加技能

### code-commentator

代码注释补充与规范化专家：
- 自动识别多种编程语言
- 双语注释（中英文）
- 规范化格式（JSDoc、docstring 等）
- 为函数、类、属性添加完整注释

### project-context

跨会话管理用户画像和项目上下文：
- 记住你的偏好和技术背景
- 追踪项目状态和已完成功能
- 为未来规划提供上下文

## 安装

使用 [vercel-labs/skills](https://github.com/vercel-labs/skills) CLI 工具安装技能：

```bash
# 安装所有技能
npx skills add https://github.com/supper-skills/development-skills

# 安装特定技能
npx skills add https://github.com/supper-skills/development-skills --skill brainstorming

# 安装到全局目录
npx skills add https://github.com/supper-skills/development-skills -g
```

## 使用方法

安装后，当你描述想要构建的内容时，技能会自动激活：

```txt
用户：我想为我的应用添加用户认证功能
用户：创建一个仪表盘组件
用户：构建产品管理的 REST API
```

AI 助手将自动调用适当的技能并引导你完成整个过程。

## 为什么选择 Development Skills

| 传统方式 | Development Skills |
|---------|-------------------|
| 需求模糊 → 返工 | 规格清晰 → 一次做对 |
| 随意实施 → Bug | 计划执行 → 质量保证 |
| 上下文丢失 → 不一致 | 持久上下文 → 结果一致 |
| 手动追踪 → 遗漏步骤 | 自动追踪 → 完整覆盖 |

## 许可证

本项目采用 MIT 许可证。详见 [LICENSE](LICENSE) 文件。

## 相关链接

- [vercel-labs/skills](https://github.com/vercel-labs/skills) - Skills CLI 工具
- [skills.sh](https://skills.sh) - 发现更多技能
