---
name: writing-plan
description: Implementation plan creation skill for multi-step tasks. Use this skill when you have a specification or requirements, before directly touching any code. Creates a comprehensive implementation plan. Triggered when users mention "create plan", "implementation plan", "write plan", "planning", "task breakdown", or start complex multi-step development work with existing specifications.
license: MIT
metadata:
  version: "3.0.1"
---

# Writing Plan Skill

This skill is used for creating comprehensive implementation plans for multi-step development tasks. Use when you have a specification or requirements, before directly touching any code.

---

## Core Principles

### Plan First

Before plan completion, **must not**:

- Invoke any implementation skill
- Write any code
- Create or modify project files (except plan documents)
- Take any implementation action

### Session State Management

Use a unified session state file to track progress:

- **Path**: `design/.session-state.md`
- **Template**: `references/session-state-template.md` (shared)

**Operation Timing**:

- When skill activates → Create/update state file
- After completing phase milestones → Update state file
- At the start of each conversation round → Read state file to restore context

### Termination Condition

The **only way to terminate** this skill is by completing the plan document and notifying the user that it's ready for execution.

---

## Workflow

### Phase 1: Context and Scope Analysis

**Objective**: Understand specification document, identify subsystems.

**Actions**:

1. Receive specification document path from brainstorming
2. Read specification document, understand requirements
3. Evaluate if requirements involve multiple independent subsystems

**Subsystem Identification Criteria**:

| Characteristic | Description |
|---------------|-------------|
| Independent data model | Subsystem has independent data structure |
| Independent interface | Subsystem provides independent API externally |
| Independent deployment | Subsystem can be deployed and run independently |
| Clear boundaries | Subsystems communicate through explicit interfaces |

**Handling Strategy**:
- Single subsystem → Proceed directly to Phase 2
- Multiple subsystems → First create outline file, then write plan for each subsystem

**Completion Criteria**: Requirements understood, subsystem division identified

---

### Phase 2: File Structure Planning

**Objective**: Plan which files will be created or modified and their responsibilities.

**Design Principles**:
- Single Responsibility: Each file should have a single clear responsibility
- Context Friendly: Code that can be understood in one context window
- Focused Files: Prefer small, focused files

**Output Format**:

```markdown
## File Structure

### New Files
- `path/to/new/file.ts` - Responsibility description

### Modify Files
- `path/to/existing/file.ts` - Modification content description

### Test Files
- `tests/path/to/test.ts` - Test responsibility
```

**Completion Criteria**: File structure planned, user confirmed

---

### Phase 3: Task Definition

**Objective**: Define specific implementation tasks.

**Task Granularity**: Each step should correspond to one operation (takes 2-5 minutes).

**Task Structure**:

```markdown
### Task N: [Task Name]

**Files**:
- Create: `path/to/file.ts`
- Test: `tests/path/to/test.ts`

- [ ] **Step 1**: Write failing test
- [ ] **Step 2**: Run test to verify failure
- [ ] **Step 3**: Write minimal implementation
- [ ] **Step 4**: Run test to verify pass
```

**Task Requirements**:
- Precise file paths, no ambiguous references
- Complete code in plan, not placeholders
- Precise commands and expected output
- Test-first approach (TDD)

**Completion Criteria**: All tasks defined, user confirmed

---

### Phase 4: Plan Save and Confirmation

**Objective**: Save plan document, get user approval.

**Actions**:

1. Save plan to `design/plans/YYYY-MM-DD-<feature>.md`
2. Ask user to confirm plan content
3. If user approves, ask whether to start execution

**Standard Script**:

> "Plan complete and saved. Please confirm the following:
>
> **Plan Document**: `design/plans/<filename>.md`
> **Total Tasks**: [Count]
>
> Confirm to start execution?"

---

### Phase 5: Execution Handover

**Objective**: Invoke executing-plans skill.

**Invocation Format**:

```
Invoke executing-plans skill with plan document path: <path>
```

**Termination**: Upon completion of this phase, this skill ends.

---

## Multi-Subsystem Processing

When multiple subsystems are identified:

### 1. Create Outline File

**Path**: `design/plans/YYYY-MM-DD-<topic>-outline.md`

**Content**:

```markdown
# [Project Name] Implementation Plan Outline

## Subsystem Division

| Subsystem | Scope | Dependencies | Status |
|-----------|-------|--------------|--------|
| SubsystemA | [Scope] | None | Pending |
| SubsystemB | [Scope] | A | Pending |

## Execution Order

1. SubsystemA (no dependencies)
2. SubsystemB (depends on A)

## Shared Components

| Component | Using Subsystems | Definition Location |
|-----------|-----------------|---------------------|
| [Component Name] | A, B | In SubsystemA plan |
```

### 2. Write Plan for Each Subsystem

Each subsystem independently writes plan document, after completion update outline file status.

---

## Reference Guides

| Reference Document | Purpose |
|-------------------|---------|
| `references/plan-template.md` | Plan template |
| `references/patterns.md` | Common plan patterns |

---

## Common Issues

### Plan Needs Modification?

Handling:
1. Record changes in outline file
2. Update affected plan documents
3. Notify user of change impact scope

### How to Resume After Conversation Interruption?

Handling:
1. Read session state file `design/.session-state.md`
2. Continue execution based on "Next Step"
