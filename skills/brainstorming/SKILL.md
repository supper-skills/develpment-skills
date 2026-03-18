---
name: brainstorming
description: This skill must be executed before any creative work - including creating features, building components, adding functionality, or modifying behavior. It explores user intent, requirements, and design solutions before implementation. Through natural collaborative dialogue, ideas are transformed into complete design specifications. Triggered when users mention "new feature", "build", "create component", "add functionality", "implement", or start any development work.
license: MIT
metadata:
  version: "2.1.0"
---

# Brainstorming Skill

This skill is an essential prerequisite for any creative work, transforming ideas into complete design specifications through collaborative dialogue.

---

## Core Constraints

> ⚠️ The following rules must always be followed and never forgotten.

### Prohibited Actions (Until User Approval)

Before user approval of the design document, **absolutely prohibited**:

- ❌ Invoke any implementation skill
- ❌ Write any code
- ❌ Set up project scaffolding
- ❌ Take any implementation action

**No exceptions**: No matter how simple the project appears, this workflow must be followed.

### Termination Condition

The **only way to terminate** this skill is by invoking the `writing-plan` skill and passing the specification document path.

### Activation Declaration

Upon skill activation, immediately declare:

> "I am using the brainstorming skill to explore your requirements and create a design specification."

### Phase Declaration

At the start of each conversation round, declare the current progress:

> 【Phase X/8】Currently executing: [Phase Name]

---

## State-Driven Workflow

> 📍 Each conversation focuses only on the current phase, then proceeds to the next.

### State File Mechanism

**Purpose**: Solve the attention loss problem in multi-round conversations.

**Operation**: Immediately create a state file upon skill activation:

- **Path**: `design/specs/YYYY-MM-DD-<topic>-state.md`
- **Template**: See `references/state-template.md`

**At the start of each conversation**: Read state file → Restore context → Declare current phase

**After each user confirmation**: Update state file → Check if can proceed to next phase

---

### Phase 1/8: Explore Project Background

**Objective**: Understand the current project status and evaluate the scope of requirements.

**Actions**:

1. Check project file structure
2. Review related documentation
3. Check recent commit history (if version control exists)
4. Evaluate if requirements involve multiple independent subsystems

**Scope Check**:

- If the request involves multiple independent subsystems, **immediately mark it**
- Help users decompose into subprojects, each undergoing independent brainstorming

**Completion Criteria**: Project tech stack and existing structure understood, requirements scope confirmed as appropriate

---

### Phase 2/8: Ask Clarifying Questions

**Objective**: Understand goals, constraints, and success criteria one by one.

**Execution Rules**:

- Ask **only one question per message**
- Prefer multiple-choice format
- Open-ended questions are also acceptable

**Core Question List** (in order):

| # | Question Type | Example Question |
|---|--------------|------------------|
| 1 | Goal定位 | "Who are the primary users of this feature?" |
| 2 | Constraints | "Are there time or tech stack limitations?" |
| 3 | Success Criteria | "How do we determine if this feature is successfully delivered?" |
| 4 | Edge Cases | "Are there edge cases that need special handling?" |

**Completion Criteria**: Goal clearly defined, constraints understood, success criteria verifiable

---

### Phase 3/8: Propose Solution Options

**Objective**: Provide 2-3 different solutions with trade-off analysis.

**Actions**:

1. Propose 2-3 different solutions
2. Explain pros and cons of each
3. Provide recommended solution with reasoning

**Presentation Format**:

```markdown
## Solution Comparison

### Option A: [Name] (Recommended)

- **Pros**: ...
- **Cons**: ...
- **Recommendation Reason**: ...

### Option B: [Name]

- **Pros**: ...
- **Cons**: ...
```

**Completion Criteria**: User has selected a solution

---

### Phase 4/8: Present Design Solution

**Objective**: Present design chapter by chapter, with each part approved by user.

**Execution Rules**:

- Adjust chapter length based on complexity
- Simple content can be summarized in a few sentences
- Complex details can expand to 200-300 words
- After completing each part, ask if it's acceptable

**Required Chapters**:

| Chapter | Content Requirements |
|---------|---------------------|
| Overview | Feature goals, background context |
| Architecture | System structure, component division |
| Data Flow | How data flows |
| Error Handling | Exception handling strategy |
| Testing Strategy | How to verify correctness |

**Design Principles**:

- Decompose system into smaller units
- Each unit has a clear single responsibility
- Communicate through clear interfaces
- Can be independently understood and tested

**Completion Criteria**: All chapters presented, user approved overall design

---

### Phase 5/8: Write Design Document

**Objective**: Write the approved design into a specification document.

**Actions**:

1. Create specification document: `design/specs/YYYY-MM-DD-<topic>-design.md`
2. Include all confirmed content
3. Ensure no TODO, TBD, or placeholder content

**Document Template**: See `references/spec-template.md`

**Completion Criteria**: Document written to specified path, no placeholder content

---

### Phase 6/8: Specification Review Loop

**Objective**: Ensure specification quality through sub-agent review.

**Actions**:

1. Use review criteria from `references/spec-document-reviewer-prompt.md`
2. Deploy review sub-agent to check specification document
3. If issues found: fix and re-review
4. Maximum 5 iterations, then escalate to human handling

**Review Focus**:

- Completeness: No TODO/TBD/placeholder
- Consistency: No internal contradictions
- Clarity: Requirements testable/verifiable
- YAGNI: No unrequested features
- Clear boundaries: Units independently understandable

**Completion Criteria**: Review status is ✅ Approved

---

### Phase 7/8: User Review

**Objective**: Obtain user's final approval of the specification document.

**Actions**:

1. Present the specification document path to user
2. Ask user to review and confirm

**Standard Script**:

> "The specification document has been written and committed to `<path>`. Please review, and let me know if any modifications are needed before we begin creating the implementation plan."

**Handling User Feedback**:

- If user requests modifications: modify, then re-execute Phase 6 (specification review loop)
- If user approves: proceed to Phase 8

**Completion Criteria**: User explicitly indicates approval

---

### Phase 8/8: Transition to Implementation Phase

**Objective**: Invoke writing-plan skill to create implementation plan.

**Actions**:

1. Invoke `writing-plan` skill
2. Pass specification document path

**Invocation Format**:

```txt
Invoke writing-plan skill with specification document path: <path>
```

**Termination**: Upon completion of this phase, this skill ends.

---

## Reference Guides

> 📚 The following content is consulted as needed and does not affect the core workflow.

| Reference Document | Purpose |
|-------------------|---------|
| `references/state-template.md` | State file template |
| `references/spec-template.md` | Specification document template |
| `references/spec-document-reviewer-prompt.md` | Specification review criteria |
| `references/tech-selection-guide.md` | Technology selection guide |
| `references/risk-assessment-template.md` | Risk assessment template |
| `references/project-initialization-guide.md` | Project initialization scenarios |
| `references/faq.md` | Frequently asked questions |

---

## Workflow Overview Diagram

```txt
┌─────────────────────────────────────────────────────────────────┐
│                        Brainstorming Workflow                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1/8  Explore Project Background ──→ Understand status, assess scope │
│         │                                                       │
│         ▼                                                       │
│  2/8  Ask Clarifying Questions ──→ Understand goals/constraints/success criteria │
│         │                                                       │
│         ▼                                                       │
│  3/8  Propose Solution Options ──→ 2-3 options + recommendation │
│         │                                                       │
│         ▼                                                       │
│  4/8  Present Design Solution ──→ Present by chapter, approve one by one │
│         │                                                       │
│         ▼                                                       │
│  5/8  Write Design Document ──→ Write to design/specs/          │
│         │                                                       │
│         ▼                                                       │
│  6/8  Specification Review Loop ──→ Sub-agent review, fix issues │
│         │                                                       │
│         ▼                                                       │
│  7/8  User Review ──→ User final approval                       │
│         │                                                       │
│         ▼                                                       │
│  8/8  Transition to Implementation ──→ Invoke writing-plan       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Quick Reference: Key Principles

| Principle | Description |
|-----------|-------------|
| One Question Per Message | Ask only one question per message |
| Compare Options | Must propose 2-3 options before deciding |
| Incremental Verification | Each design part must be approved before proceeding |
| State Persistence | Use state files to prevent attention loss |
| YAGNI | Remove unnecessary features from design |
| Single Exit | Can only terminate by invoking writing-plan |
