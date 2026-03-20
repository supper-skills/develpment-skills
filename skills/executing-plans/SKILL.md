---
name: executing-plans
description: Use when there is a written implementation plan to execute in the session. Load the plan, review it, execute all tasks, and report upon completion. Activate when user mentions "execute plan", "implement plan", "run plan", "start execution", or when a plan document is ready for implementation.
license: MIT
metadata:
  version: "3.0.0"
---

# Executing Plans Skill

This skill is used to execute written implementation plans, strictly following documented steps.

---

## Core Principles

### Execution First

Before the plan is completed, do NOT:

- Skip the review step
- Skip verification steps
- Operate on main branch (unless explicitly approved)
- Guess or assume

### Session State Management

Use a unified session state file to track progress:

- **Path**: `design/.session-state.md`
- **Template**: `references/execution-state-template.md` (shared)

**When to Operate**:

- Skill activation → **Immediately create/update state file**
- After completing a task → **Immediately update state file**
- At the start of each dialogue round → Read state file to restore context
- **After each phase/task completion → Immediately update state file**

### Termination Condition

The only way to terminate this skill is to complete all tasks and generate a completion report.

---

## Task Status

| Status | Description |
| ------ | ------------------------ |
| Completed | Task completed, all verifications passed |
| In Progress | Task is being executed |
| Pending | Task has not started |
| Blocked | Task is blocked by issues |

---

## Workflow

### Phase 1: Load and Review Plan

**Goal**: Load plan document, conduct critical review.

**Actions**:

1. Run `git branch --show-current` to confirm current branch
2. If on main/master branch, stop and ask if should continue
3. Read plan document
4. Conduct critical review of plan
5. **Verify test coverage**

**Review Checklist**:

- [ ] Are goals clear and achievable?
- [ ] Are all file paths precise and correct?
- [ ] Are code snippets complete (not placeholders)?
- [ ] Are test commands accurate for the project?
- [ ] Is each step granular enough (2-5 minutes)?
- [ ] Does each task include test steps?
- [ ] Are test file paths clear and complete?
- [ ] Do test cases cover main functionality?

**Test Coverage Verification**:

⚠️ **Mandatory Check Items**:

- Check if each task defines test file path
- Verify test file paths are not empty or placeholders
- Confirm test cases cover core functionality
- If test coverage is insufficient, immediately stop and require test plan to be supplemented

**Decision Points**:

- If concerns found → Record issues, discuss with user before continuing
- If test coverage insufficient → Request return to writing-plan to supplement tests
- If no concerns → Create task list, proceed to Phase 2

**Completion Criteria**: Plan reviewed, test coverage verified, task list created

---

### Phase 2: Execute Tasks

**Goal**: Execute each task according to the plan.

**Execution Rules**:

For each task in the plan:

1. Mark task as "In Progress" in task list
2. **Verify test file exists** (if it doesn't exist, create test file first)
3. Execute each step exactly as written
4. Execute tests following TDD flow, tests must pass, test failures must be fixed
5. Run specified verifications
6. **Check if code comments need to be added**
7. Mark task as "Completed" in task list
8. Update session state file
9. Commit if plan specifies

**Code Comment Invocation Format**:

```
Invoke code-commentator skill, target files: [file paths]
```

**Step Execution Rules**:

- Read existing files before making modifications
- Use exact code from the plan
- Execute commands exactly as specified in the plan
- Check if actual output matches expected output

**Verification Requirements**:

Each task must pass its verification before moving to the next:

- Tests must pass (not just run)
- Build must succeed
- Lint must pass
- Code comments added (if needed)

**Error Handling**:

When errors occur:

1. Record error to session state file
2. Stop and seek help

**Completion Criteria**: All tasks executed, all tests passed, code comments added, verifications passed

---

### Phase 3: Completion and Reporting

**Goal**: Generate completion report, update project context.

**Actions**:

1. Run final verification suite
2. Update session state file marking completion
3. Generate completion report
4. **Use project-context skill to update project context**
5. **Use project-context skill to update user profile** (if new preferences identified)

**Completion Report Format**:

```markdown
## Implementation Complete

**Plan**: [plan file path]
**Status**: ✅ All tasks completed

### Summary

[Brief description of what was built]

### Changed Files

- New: [new file list]
- Modified: [modified file list]

### Verification Results

- Tests: ✅ Passed
- Build: ✅ Succeeded
- Lint: ✅ Clean
```

**Completion Criteria**: Report generated, project context updated, user profile updated (if changed)

---

## When to Stop and Seek Help

**Immediately stop execution in the following situations**:

| Situation | Action |
| ---------------- | ---------------------- |
| Missing dependencies | Request user to install or provide |
| Tests repeatedly failing | Debug and seek guidance when stuck |
| Instructions unclear | Request clarification, don't guess |
| Critical plan defects | Return to Phase 1 for plan revision |
| Unexpected errors occur | Record error and seek help |

**Stop Protocol**:

1. Record obstacle to session state file
2. Explain what was attempted
3. Pose specific questions
4. Wait for guidance

---

## Multi-Subsystem Handling

When plan contains multiple subsystems:

1. Read outline file, identify number of subsystems
2. Verify dependencies, order by execution sequence
3. Execute each subsystem in dependency order (Phase 1 → Phase 2 → Phase 3)
4. Shared components implemented in the first subsystem that uses them

---

## Invocation by Other Skills

When invoked by writing-plan skill:

**Received Parameters**:

- `plan_path`: Plan document path (required)
- `subsystem_paths`: Subsystem plan path list (required for multi-subsystem)
- `outline_path`: Outline file path (if applicable)

**Skip trigger condition check**, directly create session state file and proceed to Phase 1.

---

## Reference Guide

| Reference Document | Purpose |
| ------------------------------------------ | ---------------- |
| `references/execution-state-template.md`   | Execution state record template |
| `references/completion-report-template.md` | Completion report template |

---

## FAQ

### How to recover after dialogue interruption?

Handling:

1. Read session state file `design/.session-state.md`
2. Verify completed task code and tests
3. Report recovery options to user

### Plan needs modification?

Handling:

1. Return to Phase 1 for plan review
2. Discuss modification plan with user
3. Re-execute after modification

### Encountered obstacles?

Handling:

1. Record issue to session state file
2. Stop and ask user
3. Don't try to force through obstacles
