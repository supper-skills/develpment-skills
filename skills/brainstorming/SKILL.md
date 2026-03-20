---
name: brainstorming
description: Execute before any creative work — including creating features, building components, adding functionality, or modifying behavior. Explore user intent, requirements, and design solutions before implementation. Transform ideas into complete design specifications through natural collaborative dialogue. Activate when user mentions "new feature", "build", "create component", "add functionality", "implement", or starts any development work. This skill automatically invokes the project-context skill to obtain user profile and workflow path recommendations.
license: MIT
metadata:
  version: "3.0.0"
---

# Brainstorming Skill

This skill is a required step before any creative work, transforming ideas into complete design specifications through collaborative dialogue.

---

## Core Principles

### Design First

Before user approval of the design document, do NOT:

- Invoke any implementation skills
- Write any code
- Set up project scaffolding
- Take any implementation actions

### Session State Management

Use a unified session state file to track progress:

- **Path**: `design/.session-state.md`
- **Template**: `references/session-state-template.md`

**When to Operate**:

- Skill activation → **Create state file**
- After user confirmation → **Update state file**
- At the start of each dialogue round → Read state file to restore context
- **After each phase completion → Update state file**

### Termination Condition

The only way to terminate this skill is to invoke the `writing-plan` skill and pass the specification document path.

---

## Workflow

### Phase 1: Explore Background

**Goal**: Understand current project status and assess requirement scope.

**Actions**:

1. Invoke `project-context` skill to get user profile
2. Read project context (if exists): `design/context/project-context.md`
3. Check project file structure
4. Assess if requirements involve multiple independent subsystems
5. **Proactively update user profile** (if new preferences or technical background identified)

**Scope Check**:

- If request involves multiple independent subsystems, assist user in breaking down into sub-projects
- Each sub-project undergoes brainstorming independently

**Completion Criteria**: Project tech stack and existing structure understood, requirement scope confirmed, user profile updated (if changed)

---

### Phase 2: Confirm Requirements

**Goal**: Understand goals, constraints, and success criteria one by one.

**Rules**:

- Ask only one question per message
- Prefer multiple-choice format

**Core Question List** (in order):

| # | Question Type | Example Question |
| ---- | -------- | -------------------------------- |
| 1    | Goal Positioning | "Who are the primary users of this feature?" |
| 2    | Constraints | "Are there any time or tech stack limitations?" |
| 3    | Success Criteria | "How do we determine if this feature is successfully delivered?" |
| 4    | Edge Cases | "Are there any edge cases that need special handling?" |

**Completion Criteria**: Goal positioning clear, constraints identified, success criteria verifiable

---

### Phase 3: Solution Selection

**Goal**: Provide 2-3 different solutions with trade-off analysis.

**Actions**:

1. Propose 2-3 different solutions
2. Explain pros and cons of each solution
3. Provide recommended solution with reasoning

**Completion Criteria**: User has selected a solution

> Reference: `references/tech-selection-guide.md`

---

### Phase 4: Design Document

**Goal**: Write validated design into specification document.

**Actions**:

1. Create specification document: `design/specs/YYYY-MM-DD-<topic>-design.md`
2. Include all confirmed content
3. Ensure no TODOs, TBDs, or placeholders

**Document Structure**:

| Section | Content Requirements |
| -------- | -------------------- |
| Overview | Feature goals, background context |
| Goal Positioning | Primary users and use cases |
| Constraints | Technical, time, resource limitations |
| Success Criteria | Verifiable delivery standards |
| Architecture Design | System structure and component division |
| Data Flow | How data flows |
| Error Handling | Exception handling strategies |
| Testing Strategy | How to verify feature correctness |

**Completion Criteria**: Document written to specified path, no placeholder content

> Reference: `references/spec-template.md`

---

### Phase 5: Handover

**Goal**: Obtain user approval, invoke writing-plan skill.

**Actions**:

1. Present specification document path to user
2. Request user review and confirmation
3. If user approves, invoke writing-plan skill

**Standard Phrase**:

> "The specification document has been written and submitted to `<path>`. Please review it. Once confirmed, I will begin creating the implementation plan."

**Invocation Format**:

```
Invoke writing-plan skill, specification document path: <path>
```

**Termination**: After this phase completes, this skill ends.

---

## Reference Guide

| Reference Document | Purpose |
| ---------------------------------------- | ---------------- |
| `references/session-state-template.md`   | Session state file template |
| `references/spec-template.md`            | Specification document template |
| `references/tech-selection-guide.md`     | Technology selection guide |
| `references/risk-assessment-template.md` | Risk assessment template |

---

## FAQ

### User insists on skipping design and implementing directly?

Response:

> "I understand you want to move quickly. The design document can be brief, but it needs to be documented and approved by you. This ensures we have consensus on the goals and avoids rework later."

### What if the project scope is too large?

Handling:

1. Mark as multi-subsystem project
2. Assist user in breaking down into independent sub-projects
3. Start brainstorming for the first sub-project
4. Each sub-project goes through specification → planning → implementation cycle independently

### How to recover after dialogue interruption?

Handling:

1. Read session state file `design/.session-state.md`
2. Continue execution based on "Next Step"
