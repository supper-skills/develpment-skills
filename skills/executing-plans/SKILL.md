---
name: executing-plans
description: Used when there is a written implementation plan that needs to be executed in a session. Load the plan, review critically, execute all tasks, and report upon completion. Triggered when users mention "execute plan", "implement plan", "run plan", "start execution", or the plan document is ready for implementation.
license: MIT
metadata:
  version: "3.0.0"
---

# Executing Plans Skill

This skill is used for executing written implementation plans, strictly following documented steps.

---

## Core Principles

### Execution First

Before plan completion, **must not**:

- Skip review steps
- Skip verification steps
- Operate on main branch (unless explicit approval obtained)
- Guess or assume

### Session State Management

Use a unified session state file to track progress:

- **Path**: `design/.session-state.md`
- **Template**: `references/session-state-template.md` (shared)

**Operation Timing**:

- When skill activates → Create/update state file
- After task completion → Update state file
- At the start of each conversation round → Read state file to restore context

### Termination Condition

The **only way to terminate** this skill is by completing all tasks and generating a completion report.

---

## Task Status

| Status | Description |
|--------|-------------|
| Complete | Task completed, all verifications passed |
| In Progress | Task is being executed |
| Pending | Task not yet started |
| Blocked | Task blocked by issues |

---

## Workflow

### Phase 1: Load and Review Plan

**Objective**: Load plan document, perform critical review.

**Actions**:

1. Run `git branch --show-current` to confirm current branch
2. If on main/master branch, stop and ask whether to continue
3. Read plan document
4. Critical review of plan

**Review Checklist**:

- [ ] Are goals clear and achievable?
- [ ] Are all file paths precise and correct?
- [ ] Are code snippets complete (not placeholders)?
- [ ] Are test commands accurate for the project?
- [ ] Is each step granular enough (2-5 minutes)?

**Decision Point**:

- If concerns found → Record issues, discuss with user before continuing
- If no concerns → Create task list, proceed to Phase 2

**Completion Criteria**: Plan reviewed, task list created

---

### Phase 2: Execute Tasks

**Objective**: Execute each task according to plan.

**Execution Rules**:

For each task in the plan:

1. Mark task as "In Progress" in task list
2. Execute each step exactly as written
3. Run specified verifications
4. Mark task as "Complete" in task list
5. Update session state file
6. Commit if plan specifies

**Step Execution Rules**:

- Read existing files before modifying
- Use exact code from the plan
- Execute commands as specified in the plan
- Check if actual output matches expected output

**Verification Requirements**:

Each task must pass its verification before moving to the next:
- Tests must pass (not just run)
- Build must succeed
- Lint must pass

**Error Handling**:

When errors occur:
1. Record error to session state file
2. Stop and seek help

**Completion Criteria**: All tasks executed, verifications passed

---

### Phase 3: Completion and Reporting

**Objective**: Generate completion report, update project context.

**Actions**:

1. Run final verification suite
2. Update session state file to mark complete
3. Generate completion report
4. Update project context

**Completion Report Format**:

```markdown
## Implementation Complete

**Plan**: [Plan file path]
**Status**: ✅ All tasks completed

### Summary

[Brief description of what was built]

### Changed Files

- New: [New file list]
- Modified: [Modified file list]

### Verification Results

- Tests: ✅ Passed
- Build: ✅ Success
- Lint: ✅ Clean
```

**Project Context Update**:

Check if `design/context/project-context.md` exists:
- If not exists, create using template
- If exists, append completed feature

**Completion Criteria**: Report generated, project context updated

---

## When to Stop and Seek Help

**Stop execution immediately in the following situations**:

| Situation | Action |
|-----------|--------|
| Missing dependencies | Request user to install or provide |
| Tests repeatedly fail | Debug and seek guidance when stuck |
| Instructions unclear | Request clarification, do not guess |
| Critical plan defects | Return to Phase 1 for plan revision |
| Unexpected errors | Record error and seek help |

**Stop Protocol**:

1. Record obstacle to session state file
2. Explain what was tried
3. Ask specific questions
4. Wait for guidance

---

## Multi-Subsystem Processing

When plan contains multiple subsystems:

1. Read outline file, identify number of subsystems
2. Verify dependency relationships, arrange in execution order
3. Execute each subsystem in dependency order (Phase 1 → Phase 2 → Phase 3)
4. Shared components implemented in first subsystem that uses them

---

## Invoked by Other Skills

When invoked by writing-plan skill:

**Received Parameters**:
- `plan_path`: Plan document path (required)
- `subsystem_paths`: Subsystem plan path list (required for multi-subsystem)
- `outline_path`: Outline file path (if applicable)

**Skip trigger condition check**, directly create session state file and proceed to Phase 1.

---

## Reference Guides

| Reference Document | Purpose |
|-------------------|---------|
| `references/execution-state-template.md` | Execution state recording template |
| `references/completion-report-template.md` | Completion report template |

---

## Common Issues

### How to Resume After Conversation Interruption?

Handling:
1. Read session state file `design/.session-state.md`
2. Verify code and tests for completed tasks
3. Report recovery options to user

### Plan Needs Modification?

Handling:
1. Return to Phase 1 for plan review
2. Discuss modification plan with user
3. Re-execute after modification

### Encountered Blocker?

Handling:
1. Record issue to session state file
2. Stop and ask user
3. Do not force through blocker
