# Development Skills

[简体中文](./README.zh-CN.md) | English

**Turn your ideas into production-ready code.** One sentence is all it takes to start building.

## What This Skill Pack Does

Development Skills transforms your ideas into fully implemented projects through a structured, quality-assured workflow. Simply describe what you want to build, and the AI assistant will guide you from concept to completion.

```
Your Idea → Design Specification → Implementation Plan → Working Code
```

## Core Workflow

The skill pack provides three interconnected skills that work together seamlessly:

### 1. brainstorming

**When you say**: "I want to create a TODO List app"

The AI assistant will:
- Collaborate with you to explore requirements and goals
- Propose multiple solution approaches with trade-off analysis
- Create a complete design specification document
- Ensure consensus before any code is written

### 2. writing-plan

**After design approval**, the AI assistant will:
- Break down the specification into granular implementation steps
- Define precise file structures and responsibilities
- Create test-driven development tasks
- Prepare a comprehensive implementation plan

### 3. executing-plans

**After plan approval**, the AI assistant will:
- Execute each step exactly as documented
- Run all validations and tests at checkpoints
- Track progress and handle blockers
- Generate completion reports

## Example

```txt
User: I want to create a blog platform with markdown support

AI: [Activates brainstorming skill]
    Let me understand your requirements better...
    Who are the primary users of this platform?
    [Collaborative dialogue continues...]

    [Creates design specification]
    [Activates writing-plan skill]
    [Creates implementation plan]
    [Activates executing-plans skill]
    [Implements the feature]

    ✅ Your blog platform is ready!
```

## Additional Skills

### code-commentator

Code annotation supplementation and standardization expert:
- Automatic language detection for multiple programming languages
- Bilingual comments (Chinese and English)
- Standardized format (JSDoc, docstring, etc.)
- Complete annotations for functions, classes, properties

### project-context

Manages user profiles and project context across sessions:
- Remembers your preferences and technical background
- Tracks project status and completed features
- Provides context for future planning

## Installation

Install skills using the [vercel-labs/skills](https://github.com/vercel-labs/skills) CLI tool:

```bash
# Install all skills
npx skills add https://github.com/supper-skills/development-skills

# Install a specific skill
npx skills add https://github.com/supper-skills/development-skills --skill brainstorming

# Install to global directory
npx skills add https://github.com/supper-skills/development-skills -g
```

## Usage

After installation, skills activate automatically when you describe what you want to build:

```txt
User: I want to add user authentication to my app
User: Create a dashboard component
User: Build a REST API for product management
```

The AI assistant will automatically invoke the appropriate skill and guide you through the process.

## Why Development Skills?

| Traditional Approach | Development Skills |
|---------------------|-------------------|
| Vague requirements → Rework | Clear specification → First-time right |
| Ad-hoc implementation → Bugs | Planned execution → Quality assured |
| Lost context → Inconsistency | Persistent context → Consistent results |
| Manual tracking → Missed steps | Automatic tracking → Complete coverage |

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Related Links

- [vercel-labs/skills](https://github.com/vercel-labs/skills) - Skills CLI tool
- [skills.sh](https://skills.sh) - Discover more skills
