---
name: brainstorming
description: This skill must be executed before any creative work - including creating features, building components, adding functionality, or modifying behavior. It explores user intent, requirements, and design solutions before implementation. Through natural collaborative dialogue, ideas are transformed into complete design specifications. Triggered when users mention "new feature", "build", "create component", "add functionality", "implement", or start any development work. This skill automatically invokes the project-context skill to get user profile and workflow path recommendations.
license: MIT
metadata:
  version: "3.0.0"
---

# Brainstorming Skill

This skill is an essential prerequisite for any creative work, transforming ideas into complete design specifications through collaborative dialogue.

---

## Core Principles

### Design First

Before user approval of the design document, **must not**:

- Invoke any implementation skill
- Write any code
- Set up project scaffolding
- Take any implementation action

### Session State Management

Use a unified session state file to track progress:

- **Path**: `design/.session-state.md`
- **Template**: `references/session-state-template.md`

**Operation Timing**:

- When skill activates → Create state file
- After user confirmation → Update state file
- At the start of each conversation round → Read state file to restore context

### Termination Condition

The **only way to terminate** this skill is by invoking the `writing-plan` skill and passing the specification document path.

---

## Workflow

### Phase 1: Explore Background

**Objective**: Understand current project status, evaluate requirements scope.

**Actions**:

1. Invoke `project-context` skill to get user profile
2. Read project context (if exists): `design/context/project-context.md`
3. Check project file structure
4. Evaluate if requirements involve multiple independent subsystems

**Scope Check**:

- If request involves multiple independent subsystems, help user decompose into subprojects
- Each subproject undergoes independent brainstorming

**Completion Criteria**: Project tech stack and existing structure understood, requirements scope confirmed

---

### Phase 2: Confirm Requirements

**Objective**: Understand goals, constraints, and success criteria one by one.

**Execution Rules**:

- Ask only one question per message
- Prefer multiple-choice format

**Core Question List** (in order):

| # | Question Type | Example Question |
|---|--------------|------------------|
| 1 | Goal Positioning | "Who are the primary users of this feature?" |
| 2 | Constraints | "Are there time or tech stack limitations?" |
| 3 | Success Criteria | "How do we determine if this feature is successfully delivered?" |
| 4 | Edge Cases | "Are there edge cases that need special handling?" |

**Completion Criteria**: Goal clearly defined, constraints understood, success criteria verifiable

---

### Phase 3: Solution Selection

**Objective**: Provide 2-3 different solutions with trade-off analysis.

**Actions**:

1. Propose 2-3 different solutions
2. Explain pros and cons of each
3. Provide recommended solution with reasoning

**Completion Criteria**: User has selected a solution

> Reference: `references/tech-selection-guide.md`

---

### Phase 4: Design Document

**Objective**: Write the approved design into a specification document.

**Actions**:

1. Create specification document: `design/specs/YYYY-MM-DD-<topic>-design.md`
2. Include all confirmed content
3. Ensure no TODO, TBD, or placeholder content

**Document Structure**:

| Section | Content Requirements |
|---------|---------------------|
| Overview | Feature goals, background context |
| Goal Positioning | Primary users and use cases |
| Constraints | Technical, time, resource limitations |
| Success Criteria | Verifiable delivery criteria |
| Architecture Design | System structure and component division |
| Data Flow | How data flows |
| Error Handling | Exception handling strategy |
| Testing Strategy | How to verify correctness |

**Completion Criteria**: Document written to specified path, no placeholder content

> Reference: `references/spec-template.md`

---

### Phase 5: Handover

**Objective**: Get user approval, invoke writing-plan skill.

**Actions**:

1. Present specification document path to user
2. Ask user to review and confirm
3. If user approves, invoke writing-plan skill

**Standard Script**:

> "The specification document has been written and committed to `<path>`. Please review, and confirm to start creating the implementation plan."

**Invocation Format**:

```
Invoke writing-plan skill with specification document path: <path>
```

**Termination**: Upon completion of this phase, this skill ends.

---

## Reference Guides

| Reference Document | Purpose |
|-------------------|---------|
| `references/session-state-template.md` | Session state file template |
| `references/spec-template.md` | Specification document template |
| `references/tech-selection-guide.md` | Technology selection guide |
| `references/risk-assessment-template.md` | Risk assessment template |

---

## Common Issues

### User Insists on Skipping Design and Going Straight to Implementation?

Reply:

> "I understand you want to move quickly. The design document can be brief, but it needs to be recorded and approved by you to ensure we have consensus on the goals, avoiding rework later."

### Project Scope Too Large?

Handling:

1. Mark as multi-subsystem project
2. Help user decompose into independent subprojects
3. Start brainstorming for the first subproject
4. Each subproject undergoes independent specification → planning → implementation cycle

### How to Resume After Conversation Interruption?

Handling:

1. Read session state file `design/.session-state.md`
2. Continue execution based on "Next Step"
