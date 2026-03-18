---
name: executing-plans
description: Used when there is a written implementation plan that needs to be executed in a session with review checkpoints. Load the plan, review critically, execute all tasks, and report upon completion. Triggered when users mention "execute plan", "implement plan", "run plan", or the plan document is ready for implementation.
license: MIT
metadata:
  version: "3.0.0"
---

# Executing Plans Skill

This skill is used for executing written implementation plans, strictly following documented steps and quality checkpoints.

## Reference Document Index

| Document | Purpose | When to Read |
|----------|---------|--------------|
| `references/execution-state-template.md` | Complete template for execution state file | Reference when creating state file |
| `references/workflow-examples.md` | Detailed workflow examples | Reference when needing specific execution examples |
| `references/completion-report-template.md` | Completion report template | Reference when generating report in Phase 3 |

---

## Trigger Conditions

Activate this skill in the following situations:

- User mentions "execute plan", "implement plan", "run plan"
- User provides a plan document ready for implementation
- User requests to start implementation based on existing plan
- User says "let's start" after plan creation
- Invoked by writing-plan skill (plan completed and approved by user)

---

## When Invoked by Other Skills

When invoked by the writing-plan skill:

1. **Receive Parameters**:
   - Plan document path (required)
   - Subsystem plan path list (required for multi-subsystem): in execution order
   - Outline file path, specification document path (if applicable)
2. Skip trigger condition check
3. Create execution state file
4. Proceed to Phase 1

---

## Core Constraints

> ⚠️ The following rules must always be followed and never forgotten.

### Prohibited Actions

- ❌ Skip critical review
- ❌ Skip verification steps
- ❌ Operate on main branch (unless explicit approval obtained)
- ❌ Guess or assume

### Phase Declaration

At the start of each conversation round, declare the current progress:

> 【Execution Phase X/3】Currently executing: [Phase Name]
> Current processing: [Subsystem Name] (if applicable)

---

## Execution State File Mechanism

**Purpose**: Solve the attention loss problem in multi-round conversations.

**Operation**: Immediately create an execution state file upon skill activation:

- **Path**: `design/plans/YYYY-MM-DD-<topic>-execution-state.md`
- **Purpose**: Record session state, task progress, encountered issues, context records

**Template**: See `references/execution-state-template.md`

---

## Multi-Subsystem Processing Flow

> When a plan contains multiple subsystems, execute them one by one in dependency order. See "Example 4" in `references/workflow-examples.md`.

### 0.1 Identify Number of Subsystems

- Read outline file and check subsystem list
- **Single subsystem**: Skip this section, proceed directly to Phase 1
- **Multiple subsystems**: Execute according to this section's flow

### 0.2 Verify Dependency Relationships

- Read "Subsystem Dependency Analysis" from outline file
- Arrange subsystems in execution order (do not modify outline file)

### 0.3 Create Execution State File

Create state files for the entire project and each subsystem. Template: `references/execution-state-template.md`.

### 0.4 Execute Subsystems by Dependency Order

```
For each subsystem (in execution order):
1. Check if dependencies are satisfied, read dependent subsystem's state file
2. Create execution state file for this subsystem
3. Proceed to Phase 1 (Load and Review Plan)
4. Proceed to Phase 2 (Execute Tasks)
5. Mark subsystem complete, update top-level state file
6. Continue to next subsystem
```

### 0.5 Shared Component Handling

- Read "Shared Components" information from outline file
- Implement in the first subsystem that uses the component
- Subsequent subsystems directly reference the implemented shared component

### 0.6 Multi-Subsystem Resume Execution

1. Read top-level execution state file
2. Identify interrupted subsystems (status "🔄 In Progress" or "⏳ Pending")
3. Check state files for each completed subsystem
4. Verify code and tests are working
5. Verify dependency relationships, then continue execution

---

## Phase 1: Load and Review Plan

### 1.1 Pre-flight Check

- Run `git branch --show-current` to confirm current branch
- If on main/master branch: stop and ask if should continue

### 1.2 Receive Parameters and Locate Files

- Use provided plan document path or ask user
- Common locations: `design/plans/`
- Read outline file for global constraints and shared component information

### 1.3 Create Execution State File

Create `design/plans/YYYY-MM-DD-<topic>-execution-state.md`, fill in metadata and initial state.

### 1.4 Critical Review

Before execution, critically evaluate the plan:

**Review Checklist:**

- [ ] Are goals clear and achievable?
- [ ] Are all file paths precise and correct?
- [ ] Are code snippets complete (not placeholders)?
- [ ] Are test commands accurate for the project?
- [ ] Is each step granular enough (2-5 minutes)?
- [ ] Are task dependencies clearly defined?
- [ ] Is the tech stack appropriate?

### 1.5 Decision Point

**If concerns found:**

1. Record specific concerns in execution state file
2. Discuss with human partner before proceeding
3. Wait for plan revision or clarification

**If no concerns:**

1. Create task list from plan tasks
2. Proceed with execution

---

## Phase 2: Execute Tasks

### 2.1 Task Execution Mode

For each task in the plan:

```
1. Mark task as in-progress in task list
2. Execute each step exactly as written
3. Run specified verifications
4. Mark task as completed in task list
5. [Optional] Evaluate if comments should be added to code (see 2.1.1)
6. Update execution state file
7. Commit if plan specifies (frequent commits)
```

### 2.1.1 Comment Supplementation (Optional)

**Prerequisite**: `code-commentator` skill exists in the project.

**Evaluation Criteria**:

| Situation | Recommendation |
|-----------|---------------|
| Complex business logic, key algorithms, public APIs, data models | ✅ Add comments |
| Simple utility functions, boilerplate code/config | ❌ Skip |

**Invocation Method**:

```
Invoke code-commentator skill with the following parameters:
- File list: [code files created/modified in this task]
- Scope: Comments only, do not modify code
```

### 2.2 Step Execution Rules

- **Read before modifying** - Always read existing files before making changes
- **Use complete code only** - Use exact code from the plan
- **Run commands precisely** - Execute commands as specified in the plan
- **Verify output** - Check if actual output matches expected output
- **Update state** - Immediately update execution state file after each step

### 2.3 Verification Requirements

Each task must pass its verification before moving to the next:

- Tests must pass (not just run)
- Build must succeed
- Lint must pass
- Any specified checks must pass

### 2.4 Progress Persistence and Recovery

#### Progress Tracking Mechanism

Task progress in execution state file:

```markdown
| Task | Status | Completed At | Notes |
|------|--------|-------------|-------|
| Task 1: [Name] | ✅ Complete | HH:mm | - |
| Task 2: [Name] | 🔄 In Progress | - | Step 2/4 |
| Task 3: [Name] | ⏳ Pending | - | - |
```

#### Resume Execution Flow

**When resuming after session interruption:**

1. Read execution state file, restore context
2. Read plan document, scan task status markers
3. Identify interruption location
4. Execute code verification:
   - Check Git status: confirm working tree state
   - Check completed task code: confirm code exists
   - Run related tests to verify completed tasks work
5. Report recovery options to user:

   > "Detected plan execution interruption:
   > - Plan: [Plan path]
   > - State file: [State file path]
   > - Completed: [Count] (of [Total] tasks)
   > - Interruption location: [Interrupted task name]
   > - Code verification: [Verification result]
   >
   > Please choose recovery method:
   > a) Continue execution - Continue from interruption location
   > b) Re-execute - Re-execute the interrupted task
   > c) Start from scratch - Clear progress, start all tasks from beginning"

6. Execute corresponding operation based on user choice

#### Pre-Recovery Verification Checklist

| Verification Item | Command/Method | Purpose |
|-------------------|----------------|---------|
| Git status | `git status` | Confirm working tree state |
| Completed task code | Check if files exist | Confirm code written |
| Completed task tests | Run related test commands | Confirm functionality works |
| Branch status | `git branch` | Confirm on correct branch |
| Execution state file | Read state file | Confirm context correct |

---

## Phase 3: Completion and Reporting

### 3.1 All Tasks Complete

When all tasks are complete:

1. Run final verification suite
2. Update execution state file to completed status
3. Summarize what was implemented
4. List any deviations from the plan (if any)
5. Report completion status

### 3.2 Completion Report

Report template: see `references/completion-report-template.md`.

---

## When to Stop and Seek Help

**Stop execution immediately in the following situations:**

| Situation | Action |
|-----------|--------|
| Missing dependencies | Request user to install or provide |
| Tests repeatedly fail | Debug and seek guidance when stuck |
| Instructions unclear | Request clarification, do not guess |
| Critical plan defects | Return to Phase 1 for plan revision |
| Unexpected errors | Record error and seek help |
| Scope creep detected | Discuss before expanding |

### Stop Protocol

1. Clearly document obstacle in execution state file
2. Explain what you tried
3. Ask specific questions
4. Update "Encountered Issues" in execution state file
5. Wait for guidance before proceeding

---

## When to Revisit Phase 1

**Return to plan review in the following situations:**

- Human partner updated the plan based on your feedback
- Basic approach needs rethinking
- Multiple tasks blocked by the same issue
- Verification continues to fail despite following the plan

**Do not force through blocks** - Stop and ask

---

## Quality Checklist

### Before Execution

- [ ] Plan file located and readable
- [ ] Critical review completed
- [ ] Concerns resolved (if any)
- [ ] Task list created from plan
- [ ] Execution state file created
- [ ] Not on main branch (or explicit approval obtained)

### During Execution

- [ ] Each step executed exactly as written
- [ ] Verification run and passed
- [ ] Task list updated in real-time
- [ ] Execution state file updated in real-time
- [ ] Commits made as specified

### After Execution

- [ ] All tasks marked complete
- [ ] Execution state file updated to completed status
- [ ] Final verification passed
- [ ] Completion report generated
- [ ] No unreported deviations

---

## Workflow Examples

See `references/workflow-examples.md` for detailed examples, including:

- **Example 1**: Standard execution flow
- **Example 2**: Resume execution flow
- **Example 3**: Plan concerns handling
- **Example 4**: Multi-subsystem execution flow

---

## Notes

1. **Always declare skill use at start**
2. **Phase declarations are mandatory** - Declare current phase at start of each conversation
3. **Critical review is mandatory** - Never skip Phase 1
4. **State file must be maintained** - Update execution state file in real-time
5. **Stop when blocked** - Asking is better than guessing
6. **Follow precisely** - Do not improvise plan steps
7. **Report deviations** - If deviation is necessary, record reason in execution state file
8. **Frequent commits** - If specified, commit after each working step
9. **No operations on main branch without consent** - Requires explicit approval
