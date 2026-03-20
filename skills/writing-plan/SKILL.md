---
name: writing-plan
description: Implementation plan creation skill for multi-step tasks. Use when there are specifications or requirements, before directly touching code. Create detailed, executable implementation plans. Activate when user mentions "create plan", "implementation plan", "write plan", "plan", "task breakdown", or starts complex multi-step development work with existing specifications.
license: MIT
metadata:
  version: "3.0.1"
---

# Writing Plan Skill

This skill is used to create comprehensive implementation plans for multi-step development tasks. Use when there are specifications or requirements, before directly touching any code.

---

## Core Principles

### Plan First

Before the plan is completed, do NOT:

- Invoke any implementation skills
- Write any code
- Create or modify project files (except plan documents)
- Take any implementation actions

### Session State Management

Use a unified session state file to track progress:

- **Path**: `design/.session-state.md`
- **Template**: `references/plan-template.md` (shared)

**When to Operate**:

- Skill activation → **Create/update state file**
- After completing phase milestones → **Update state file**
- At the start of each dialogue round → Read state file to restore context
- **After each phase completion → Update state file**

### Termination Condition

The only way to terminate this skill is to complete the plan document and notify user that execution is ready.

---

## Workflow

### Phase 1: Context and Scope Analysis

**Goal**: Understand specification document, identify subsystems.

**Actions**:

1. Receive specification document path passed from brainstorming
2. Read specification document, understand requirements
3. Assess if multiple independent subsystems are involved

**Subsystem Identification Criteria**:

| Characteristic | Description |
| ------------ | ------------------------ |
| Independent Data Model | Subsystem has its own data structure |
| Independent Interface | Subsystem provides independent API externally |
| Independent Deployment | Subsystem can be deployed and run independently |
| Clear Boundaries | Subsystems communicate through explicit interfaces |

**Handling Strategy**:

- Single subsystem → Proceed directly to Phase 2
- Multiple subsystems → Create outline file first, then write plans for each subsystem

**Completion Criteria**: Requirements understood, subsystem division identified

---

### Phase 2: File Structure Planning

**Goal**: Plan files to be created or modified and their responsibilities.

**Design Principles**:

- Single Responsibility: Each file should have a single clear responsibility
- Context-friendly: Code understandable within one context window
- Focused files: Prefer small, focused files

**Output Format**:

```markdown
## File Structure

### New Files

- `path/to/new/file.ts` - Responsibility description

### Modified Files

- `path/to/existing/file.ts` - Modification content description

### Test Files

- `tests/path/to/test.ts` - Test responsibilities
```

**Code Comment Planning**:

**Explicitly note comment requirements in file structure planning**:

For each new or modified file, annotate comment requirements:

```markdown
### New Files

- `src/utils/helper.ts` - Responsibility description
  - Comment requirements: Need documentation comments for all public functions
  - Complexity: Medium (contains complex algorithms, needs detailed comments)
```

**Comment Requirements Evaluation Criteria**:

- **High Priority**: Public APIs, core business logic, complex algorithms
- **Medium Priority**: Utility functions, data processing logic
- **Low Priority**: Simple utility functions, configuration files

**Completion Criteria**: File structure planned, test files identified, comment requirements evaluated, user confirmed

---

### Phase 3: Task Definition

**Goal**: Define specific implementation tasks.

**Task Granularity**: Each step should correspond to one operation (taking 2-5 minutes).

**Task Structure**:

```markdown
### Task N: [Task Name]

**Files**:

- Create: `path/to/file.ts`
- Test: `tests/path/to/test.ts`

- [ ] **Step 1**: Write failing test
- [ ] **Step 2**: Run test to verify failure
- [ ] **Step 3**: Write minimal implementation
- [ ] **Step 4**: Run test to verify passing
```

**Task Requirements**:

- Precise file paths, no vague references
- Complete code in plan, no placeholders
- Precise commands and expected output
- **Test-Driven Development (TDD)**: Each task must define test file and test cases first

**Test Requirements**:

⚠️ **Tasks must include test steps**, the following are prohibited:

- ❌ Only write implementation code, no tests
- ❌ Test file path is empty or uses placeholders
- ❌ Test cases are incomplete or too simple
- ❌ Skip "Write failing test" step

**Test Coverage Standards**:

- Each function/method has at least one positive test case
- Edge conditions have corresponding tests
- Error handling paths have test coverage
- Test files must be created before task starts

**Completion Criteria**: All tasks defined, each task includes complete test plan, user confirmed

---

### Phase 4: Plan Save and Confirmation

**Goal**: Save plan document, obtain user approval.

**Actions**:

1. Save plan to `design/plans/YYYY-MM-DD-<feature>.md`
2. Request user to confirm plan content
3. If user approves, ask if execution should begin

**Standard Phrase**:

> "The plan is complete and saved. Please confirm the following:
>
> **Plan Document**: `design/plans/<filename>.md`
> **Total Tasks**: [count]
>
> Should I begin execution after confirmation?"

---

### Phase 5: Execution Handover

**Goal**: Invoke executing-plans skill.

**Invocation Format**:

```
Invoke executing-plans skill, plan document path: <path>
```

**Termination**: After this phase completes, this skill ends.

---

## Multi-Subsystem Handling

When multiple subsystems are identified:

### 1. Create Outline File

**Path**: `design/plans/YYYY-MM-DD-<topic>-outline.md`

**Content**:

```markdown
# [Project Name] Implementation Plan Outline

## Subsystem Division

| Subsystem | Scope | Dependency | Status |
| ------- | ------ | ---- | ------ |
| SubsystemA | [scope] | None | To be written |
| SubsystemB | [scope] | A | To be written |

## Execution Order

1. SubsystemA (no dependencies)
2. SubsystemB (depends on A)

## Shared Components

| Component | Using Subsystems | Definition Location |
| -------- | ---------- | ------------- |
| [Component name] | A, B | In SubsystemA plan |
```

### 2. Write Plans for Each Subsystem

Each subsystem independently writes plan documents, update outline file status after completion.

---

## Reference Guide

| Reference Document | Purpose |
| ----------------------------- | ------------ |
| `references/plan-template.md` | Plan template |
| `references/patterns.md`      | Common plan patterns |

---

## FAQ

### Plan needs modification?

Handling:

1. Record changes in outline file
2. Update affected plan documents
3. Notify user of change scope

### How to recover after dialogue interruption?

Handling:

1. Read session state file `design/.session-state.md`
2. Continue execution based on "Next Step"
