# Agent Skills

[简体中文](./README.zh-CN.md) | English

Reusable skill instruction sets for AI coding assistants to extend their professional capabilities.

## Overview

Skills is a carefully designed skill package collection. Each skill is defined in a `SKILL.md` file, containing complete instruction sets, workflows, and quality standards to help AI assistants complete specific tasks more efficiently.

## Features

### Development Workflow Skills

**brainstorming**, **writing-plan**, and **executing-plans** are interconnected skills that trigger in sequence, forming a complete development workflow from requirements to implementation:

```
brainstorming → writing-plan → executing-plans
```

**Goal**: Transform user ideas into production-ready code through a structured, quality-assured process:
1. **Explore & Design** - Understand requirements and create design specifications
2. **Plan & Document** - Break down into granular, testable implementation steps
3. **Execute & Verify** - Implement with strict adherence and validation

#### brainstorming

Mandatory first step before any creative work. This skill provides:

- **Requirements Exploration**: Understands user intent, requirements, and design solutions through collaborative dialogue
- **Design Specification**: Transforms ideas into complete design specifications
- **Quality Assurance**: Includes spec review loop with automated validation
- **Workflow Guidance**: Step-by-step process from context exploration to implementation planning
- **Project Initialization**: Guidance for project structure, infrastructure decisions, and key questions
- **Technology Selection**: Systematic evaluation framework for choosing technologies
- **Risk Assessment**: Identifies and evaluates potential risks during design phase

**Reference Documents**: faq.md, project-initialization-guide.md, risk-assessment-template.md, spec-document-reviewer-prompt.md, spec-template.md, state-template.md, tech-selection-guide.md

#### writing-plan

Implementation plan creation skill for multi-step tasks, providing the following capabilities:

- **Context Analysis**: Evaluates scope and identifies independent subsystems
- **File Structure Planning**: Designs clear boundaries and well-defined interfaces
- **Task Definition**: Granular steps with TDD approach
- **Dependency Management**: Identifies and plans dependency installation
- **Environment Configuration**: Defines strategies for different environments
- **Rollback Strategy**: Prepares plans for implementation failures
- **Review Cycle**: Iterative review with quality checkpoints

**Reference Documents**: plan-document-reviewer-prompt.md, plan-template.md, patterns.md, planning-guides.md, change-management.md, quality-checklist.md, workflow-examples.md

#### executing-plans

Implementation plan execution skill with review checkpoints, providing the following capabilities:

- **Plan Loading**: Locates and loads written implementation plans
- **Critical Review**: Evaluates plan quality before execution
- **Strict Execution**: Follows each step exactly as documented
- **Verification**: Runs all specified validations at checkpoints
- **Blocker Handling**: Stops and seeks help when encountering obstacles
- **Progress Persistence**: Tracks progress with task markers for recovery after interruption
- **Recovery Mechanism**: Resume execution from interruption point with verification

**Reference Documents**: completion-report-template.md, execution-state-template.md, workflow-examples.md

---

### Standalone Skills

#### code-commentator

Code annotation supplementation and standardization expert, providing the following capabilities:

- **Automatic Language Detection**: Supports multiple programming languages including JavaScript, TypeScript, Python, Java, Go, Rust, and more
- **Bilingual Comments**: All comments include both Chinese and English descriptions
- **Standardized Format**: Automatically applies language-specific comment styles (JSDoc, docstring, etc.)
- **Completeness Guarantee**: Add complete comments for functions, classes, properties, enums, and other code elements

## Installation

Install skills using the [vercel-labs/skills](https://github.com/vercel-labs/skills) CLI tool:

```bash
# Install all skills
npx skills add https://github.com/supper-skills/skills

# Install a specific skill
npx skills add https://github.com/supper-skills/skills --skill doc-writer

# Install to global directory
npx skills add https://github.com/supper-skills/skills -g
```

## Usage

### Automatic Activation After Installation

After skills are installed, they will automatically activate when you issue relevant commands to the AI assistant:

```txt
User: I want to create a TODO List app
```

At this point, the `brainstorming` skill will automatically activate, and the AI assistant will collaborate with you to explore and design the requirements specification for the TODO List application according to the standards and processes defined in the skill.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Related Links

- [vercel-labs/skills](https://github.com/vercel-labs/skills) - Skills CLI tool
- [skills.sh](https://skills.sh) - Discover more skills
