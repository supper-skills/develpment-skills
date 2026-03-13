---
name: executing-plans
description: Use when there is a written implementation plan that needs to be executed in session with review checkpoints. Loads plan, reviews critically, executes all tasks, reports completion. Triggers when users mention "execute plan", "implement plan", "run plan", or when a plan document is ready for implementation.
license: MIT
metadata:
  version: "1.0.0"
---

# Executing Plans Skill

This skill executes written implementation plans with strict adherence to documented steps and quality checkpoints.

## Trigger Conditions

Activate this skill when:

- User mentions "execute plan", "implement plan", "run plan"
- User provides a plan document ready for implementation
- User asks to start implementation based on existing plan
- User says "let's start" after a plan has been created
- Called by writing-plan skill (plan completed and user approved)

## Called by Other Skills

When called by writing-plan skill:

1. Receives parameter: specification document path
2. Skips trigger condition check
3. Proceeds directly to Phase 1

---

## Core Principles

### Start Declaration

Always begin by declaring:

> "I am using the executing-plans skill to implement this plan."

### Core Values

- **Critical Review First** - Never blindly execute; evaluate the plan
- **Strict Adherence** - Follow each step exactly as written
- **No Skipping Verification** - Run all specified validations
- **Stop on Blockers** - Ask for help rather than guess
- **No Main Branch Without Consent** - Never start implementation on main branch without explicit user approval

---

## Phase 1: Load and Review Plan

### 1.0 Pre-check

- Run `git branch --show-current` to confirm current branch
- If on main/master branch:
  - Stop and ask user whether to continue
  - Suggest creating a feature branch

### 1.1 Locate Plan File

- Ask user for plan file location if not provided
- Common locations: `design/plans/`
- File format: typically `.md` files

### 1.2 Critical Review

Before execution, critically evaluate the plan:

**Review Checklist:**

- [ ] Is the goal clear and achievable?
- [ ] Are all file paths precise and correct?
- [ ] Are code snippets complete (not placeholders)?
- [ ] Are test commands accurate for the project?
- [ ] Is each step granular enough (2-5 minutes)?
- [ ] Are dependencies between tasks clear?
- [ ] Is the tech stack appropriate?

### 1.3 Decision Point

**If concerns found:**

1. Document specific concerns
2. Discuss with human partner before proceeding
3. Wait for plan revision or clarification

**If no concerns:**

1. Create todo list from plan tasks
2. Proceed to execution

---

## Phase 2: Execute Tasks

### 2.1 Task Execution Pattern

For each task in the plan:

```
1. Mark task as in_progress in todo list
2. Execute each step exactly as written
3. Run specified validations
4. Mark task as completed
5. Commit if plan specifies (frequent commits)
```

### 2.2 Step Execution Rules

- **Read before modify** - Always read existing files before making changes
- **Complete code only** - Use exact code from plan, not approximations
- **Run commands exactly** - Execute commands as specified in plan
- **Verify outputs** - Check that actual output matches expected output

### 2.3 Verification Requirements

Each task must pass its verification before moving to next:

- Tests must pass (not just run)
- Build must succeed
- Lint must pass
- Any specified checks must pass

### 2.4 Progress Persistence and Recovery

To ensure execution process is interruptible and recoverable, use task markers in plan documents to track progress.

#### Progress Tracking Mechanism

**Task Markers in Plan Document:**

```markdown
- [ ] **Step 1: Write failing test**    ← Not completed
- [x] **Step 2: Run test to verify failure** ← Completed
- [x] **Step 3: Write minimal implementation**    ← Completed
- [ ] **Step 4: Run test to verify pass** ← Not completed (interruption point)
```

**Interruption Point Identification:**
- Scan task checkboxes in plan document
- First `- [ ]` marker is the interruption point
- Completed tasks are marked as `- [x]`

#### Recovery Execution Process

**When resuming execution after session interruption:**

```
1. Read plan document, scan task marker status
2. Identify interruption point (first uncompleted task)
3. Execute code verification:
   - Check Git status: confirm if working directory is clean
   - Check if completed task code exists
   - Run relevant tests to verify completed tasks are working

4. Report recovery options to user:

   > "Detected plan execution interruption:
   > - Plan: design/plans/2024-01-15-auth.md
   > - Completed: Tasks 1-3 (of 8 total tasks)
   > - Interruption point: Task 4 - Run test to verify pass
   > - Code verification: ✅ Completed task code exists and tests pass
   > 
   > Please select recovery method:
   > a) Continue execution - Resume from interruption point
   > b) Re-execute - Re-execute interrupted task (current task 4)
   > c) Execute from start - Clear progress, start all tasks from beginning"

5. Execute corresponding operation based on user selection
```

#### Recovery Verification Checks

**Must verify before recovery:**

| Verification Item | Command/Method | Purpose |
|-------------------|----------------|---------|
| Git status | `git status` | Confirm working directory state |
| Completed task code | Check if files exist | Confirm code was written |
| Completed task tests | Run relevant test commands | Confirm functionality works |
| Branch status | `git branch` | Confirm on correct branch |

**Verification Result Handling:**

- **Verification passed** → Provide continue/re-execute options
- **Verification failed** → Suggest re-executing from failed task
- **Code missing** → Suggest executing from start or check Git history

#### User Selection Handling

**Selection a) Continue execution**:
- Maintain completed task status
- Resume from interruption point

**Selection b) Re-execute interrupted task**:
- Don't modify completed task code
- Re-execute current interrupted task

**Selection c) Execute from start**:
- Reset all `- [x]` to `- [ ]` in plan document
- Start from first task

---

## Phase 3: Completion and Reporting

### 3.1 All Tasks Completed

When all tasks are done:

1. Run final verification suite
2. Summarize what was implemented
3. List any deviations from plan (if any)
4. Report completion status

### 3.2 Completion Report Template

```markdown
## Implementation Complete

**Plan**: [plan-file-path]
**Status**: ✅ All tasks completed

### Summary
- [Brief description of what was built]

### Files Changed
- Created: [list of new files]
- Modified: [list of modified files]

### Verification Results
- Tests: ✅ Passed
- Build: ✅ Success
- Lint: ✅ Clean

### Notes
- [Any observations or suggestions]
```

---

## When to Stop and Seek Help

**Immediately stop execution when:**

| Situation | Action |
|-----------|--------|
| Missing dependencies | Ask user to install or provide |
| Tests fail repeatedly | Debug and ask for guidance if stuck |
| Instructions unclear | Request clarification, don't guess |
| Plan has critical flaw | Return to Phase 1 for plan revision |
| Unexpected errors | Document error and ask for help |
| Scope creep detected | Discuss with user before expanding |

### Stopping Protocol

1. Document the blocker clearly
2. Explain what you tried
3. Ask specific questions
4. Wait for guidance before proceeding

---

## When to Revisit Phase 1

**Return to plan review when:**

- Human partner updates the plan based on your feedback
- Fundamental approach needs rethinking
- Multiple tasks are blocked by same issue
- Verification keeps failing despite following plan

**Do not force through blockers** - Stop and ask

---

## Quality Checklist

### Before Execution

- [ ] Plan file located and readable
- [ ] Critical review completed
- [ ] Concerns addressed (if any)
- [ ] Todo list created from plan
- [ ] Not on main branch (or have explicit approval)

### During Execution

- [ ] Each step executed exactly as written
- [ ] Verifications run and passed
- [ ] Todos updated in real-time
- [ ] Commits made as specified

### After Execution

- [ ] All tasks marked complete
- [ ] Final verification passed
- [ ] Completion report generated
- [ ] No unreported deviations

---

## Workflow Examples

### Example 1: Standard Execution

```
User: Execute the plan at design/plans/2024-01-15-auth.md

Agent:
1. Declares: "I am using the executing-plans skill to implement this plan."
2. Informs about subagent preference
3. Loads plan from design/plans/2024-01-15-auth.md
4. Reviews plan critically - no concerns found
5. Creates todo list with 8 tasks
6. Executes each task:
   - Task 1: Write test → Run → Fail ✓
   - Task 1: Write code → Run → Pass ✓
   - Task 2: Write test → Run → Fail ✓
   - ... (continues)
7. All tasks complete
8. Runs final verification
9. Reports completion with summary
```

### Example 2: Plan Concerns

```
User: Execute the plan at plans/feature-x.md

Agent:
1. Declares: "I am using the executing-plans skill to implement this plan."
2. Loads plan
3. Reviews and finds concerns:
   - File path references non-existent directory
   - Test command uses wrong framework
4. Stops and asks user:
   "I found issues in the plan:
    - Path 'src/lib/' doesn't exist. Should it be 'src/utils/'?
    - Plan uses 'jest' but project uses 'vitest'
    Should I proceed with corrections or wait for plan revision?"
5. Waits for user guidance
```

### Example 3: Blocked During Execution

```
User: Continue with the plan

Agent:
1. Executes Task 3
2. Test fails unexpectedly
3. Debugs and finds missing dependency
4. Stops and reports:
   "Blocked on Task 3: Test requires 'lodash' but it's not installed.
    Should I:
    a) Add lodash to dependencies
    b) Wait for you to install it
    c) Modify the approach"
5. Waits for guidance
```

---

## Notes

1. **Always declare skill usage** at the start
2. **Critical review is mandatory** - never skip Phase 1
3. **Stop on blockers** - asking is better than guessing
4. **Follow exactly** - don't improvise on plan steps
5. **Report deviations** - if you must deviate, document why
6. **Frequent commits** - commit after each working step if specified
7. **No main branch without consent** - explicit approval required
