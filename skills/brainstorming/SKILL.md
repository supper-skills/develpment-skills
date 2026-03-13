---
name: brainstorming
description: MANDATORY first step before any creative work—including creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements, and design solutions before implementation. Transforms ideas into complete design specifications through collaborative dialogue. Triggers when users mention "new feature", "build", "create component", "add functionality", "implement", or start any development work.
license: MIT
metadata:
  version: "1.0.0"
---

# Brainstorming Skill

This skill is the MANDATORY first step before any creative work. It transforms ideas into complete design specifications through collaborative dialogue.

## Trigger Conditions

Activate this skill proactively when:

- User mentions "new feature", "build", "create component"
- User mentions "add functionality", "implement", "develop"
- Starting any development work that creates or modifies behavior
- User provides requirements and wants to plan before implementation
- Any request that involves creating something new

---

## Core Principles

### Start Declaration

Always begin by declaring:

> "I am using the brainstorming skill to explore your requirements and create a design specification."

### Critical Rule

**BEFORE submitting design and getting user approval, you MUST NOT:**

- Call any implementation skills
- Write any code
- Set up project scaffolding
- Take any implementation actions

This rule applies to ALL projects regardless of apparent complexity.

### Anti-Pattern

> "This is too simple, no design needed"

ALL projects must follow this process. Todo lists, single-feature tools, config changes—no exceptions. "Simple" projects often cause the most resource waste due to unexamined assumptions. Design documents can be brief (truly simple projects need only a few sentences), but design must be submitted and approved.

---

## Checklist

Must create tasks for each of the following and complete in order:

1. **Explore project context** — Check files, documentation, recent commits
2. **Ask clarifying questions** — Understand goals/constraints/success criteria one by one
3. **Propose 2-3 approaches** — Include trade-offs and your recommendation
4. **Present design** — Show in sections by complexity, get approval for each part
5. **Write design document** — Save to `design/specs/YYYY-MM-DD-<topic>-design.md`
6. **Spec review loop** — Dispatch spec document reviewer subagent; fix issues and re-dispatch until approved (max 5 iterations, then escalate to human)
7. **User reviews written spec** — Ask user to review spec file before continuing
8. **Transition to implementation** — Call writing-plan skill to create implementation plan

**Terminal state is calling write-plan, do NOT call other skills.**

---

## Process

### Understanding Core Concepts

- First check current project state (files, documentation, recent commits)
- Before asking for details, assess scope: if request involves multiple independent subsystems (e.g., "build a platform with chat, file storage, billing, and analytics"), flag this immediately. Do not spend time detailing a project that needs decomposition first.
- If project is too large for a single spec, help user decompose into sub-projects: What are independent modules? How do they relate? What order should they be built? Then brainstorm the first sub-project following normal design flow. Each sub-project gets its own spec → plan → implementation cycle.
- For appropriately scoped projects, ask questions one by one to refine the idea
- Prefer multiple-choice questions, but open-ended is acceptable
- Each message contains only one question—if deep exploration needed, split into multiple questions
- Focus on: understanding goals, constraints, and success criteria

### Exploration Methods

- Propose 2-3 different approaches with trade-offs
- Present options in conversational format with recommendation and reasoning
- Prioritize recommending the preferred approach and explain why

### Presenting Design

- After confirming understanding of build goals, show design thinking
- Adjust section length by complexity: simple content in a few sentences, complex details can expand to 200-300 words
- After each section, ask if current content is appropriate
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if anything is unclear

### Design for Isolation and Clarity

- Split system into smaller units, each with clear single functionality, communicating through well-defined interfaces, independently understandable and testable
- For each unit, you should be able to answer: What does it do? How to use it? What components does it depend on?
- Can you understand a unit's functionality without reading its internal implementation? Can you modify its internal implementation without affecting users? If no, boundary definition needs improvement.
- Smaller, clearly bounded units are also easier to manipulate—you can more clearly understand code that can be built in context at once, and modifications are more reliable when files are focused. Large file size usually means it carries too many responsibilities.

### When Working in Existing Codebases

- Before proposing changes, understand existing structure. Follow established patterns.
- If existing code has issues affecting your work (e.g., oversized files, unclear boundaries, mixed responsibilities), include targeted improvements in design—just as good developers optimize code they maintain.
- Avoid proposing unrelated refactoring. Always focus on content serving current goals.

### Project Initialization Scenarios

When users need to create a new project from scratch, pay extra attention to the following:

**Project Structure Planning:**
- Confirm project type (Web application, CLI tool, Library/SDK, Microservice, etc.)
- Recommend appropriate project directory structure
- Determine package manager and build tools

**Infrastructure Decisions:**
- Version control strategy (Git branching model, commit conventions)
- CI/CD requirements assessment
- Containerization needs (Docker, Kubernetes)

**Key Questions Checklist:**
- Who are the primary target users of the project?
- Expected project scale and complexity?
- Need to support multiple environments (development, testing, production)?
- Are there compliance or security requirements?

### Technology Selection Guidance

When determining technical solutions, systematically evaluate technology choices:

**Evaluation Dimensions:**

| Dimension | Key Considerations |
|-----------|-------------------|
| Team Familiarity | Does the team have relevant experience? What's the learning curve? |
| Community Ecosystem | Documentation quality, community activity, problem-solving resources |
| Long-term Maintenance | Project activity, version update frequency, backward compatibility |
| Performance Characteristics | Does it meet performance requirements? Any known bottlenecks? |
| Integration Difficulty | Compatibility with existing systems, migration costs |

**Selection Process:**
1. Clarify technical constraints (team skills, existing tech stack, budget limits)
2. List candidate technical solutions (usually 2-3)
3. Conduct comparative analysis by evaluation dimensions
4. Provide recommended solution with rationale
5. Document selection decisions and trade-off considerations

**Avoid Common Pitfalls:**
- Don't choose new technology just because it's "popular"
- Don't ignore team learning costs
- Don't choose solutions lacking long-term maintenance support
- Don't over-engineer the technical architecture

### Risk Assessment

Must identify and assess potential risks during the design phase:

**Risk Categories:**

| Category | Example Risks |
|----------|---------------|
| Technical Risks | Unproven technical solutions, unstable dependencies, performance bottlenecks |
| Scope Risks | Requirements creep, unclear feature boundaries, dependency on external systems |
| Resource Risks | Insufficient personnel, tight timelines, skill gaps |
| Integration Risks | Third-party API changes, complex data migration, compatibility issues |
| Security Risks | Data breaches, authentication vulnerabilities, permission control defects |

**Risk Assessment Process:**
1. **Identify Risks** — List all factors that could affect the project
2. **Assess Impact** — Grade by severity (High/Medium/Low)
3. **Assess Probability** — Estimate likelihood of occurrence (High/Medium/Low)
4. **Develop Mitigation Strategies** — Create response plans for high-impact/high-probability risks
5. **Document Risk Register** — Include risk section in design document

**Risk Mitigation Strategy Examples:**

- **Technical Validation**: Prototype validation for uncertain technical solutions
- **Incremental Delivery**: Break large features into independently deliverable small features
- **Backup Plans**: Prepare alternatives for critical dependencies
- **Monitoring Alerts**: Establish monitoring mechanisms for key metrics

---

## After Design is Complete

- Write validated design (spec) to `design/specs/YYYY-MM-DD-<topic>-design.md`

### Spec Review Loop

After writing spec document:

- Dispatch spec document reviewer subagent (see [spec-document-reviewer-prompt](./references/spec-document-reviewer-prompt.md))
- If issues found: fix, re-dispatch, repeat until approved
- If loop exceeds 5 iterations, submit to human for guidance

### User Review Gate

After spec review loop passes, ask user to review written spec before continuing:

> "Spec document has been written and submitted to `<path>`. Please review and let me know if any changes are needed before we start creating the implementation plan."

Wait for user response. If user requests changes, make changes and re-run spec review loop. Only continue after user approval.

### Implementation

- Call writing-plan skill and provide spec document path `<path>` to create detailed implementation plan
- Do NOT call any other skills. Writing plan is the next step.

---

## Key Principles

- **One question at a time** - Avoid overwhelming with multiple questions
- **Prefer multiple-choice** - Easier to answer than open-ended when feasible
- **Strictly follow YAGNI** - Remove unnecessary features from all designs
- **Explore alternatives** - Always propose 2-3 approaches before settling
- **Progressive validation** - Show current design, get approval before continuing
- **Stay flexible** - Go back and clarify when encountering unclear content

---

## Workflow Example

```
User: I need to add a user authentication system to my app.

Agent:
1. Declares: "I am using the brainstorming skill to explore your requirements and create a design specification."
2. Explores project context - checks existing code structure, tech stack
3. Asks clarifying questions one by one:
   - "What authentication methods do you want to support?"
   - "Do you need social login integration?"
   - "What are your session management requirements?"
4. Proposes 2-3 approaches with trade-offs
5. Presents design sections, getting approval for each
6. Writes design doc to design/specs/2024-01-15-user-auth-design.md
7. Dispatches spec reviewer, fixes any issues
8. Asks user to review spec
9. After approval, calls writing-plan skill
```

---

## Notes

1. **Always declare skill usage** at the start
2. **Never write code or implement** during brainstorming
3. **One question per message** - avoid overwhelming
4. **Always propose alternatives** before settling on approach
5. **Get approval incrementally** - section by section
6. **Spec review before user review** - catch issues early
7. **User approval required** before transitioning to planning
8. **Only call writing-plan** as the final step
