---
name: writing-plan
description: Implementation plan creation skill for multi-step tasks. Use this skill when you have a specification or requirements and before directly touching any code. Creates a comprehensive implementation plan, assuming the engineer has zero knowledge of the codebase. Triggered when users mention "create plan", "implementation plan", "write plan", "planning", "task breakdown", or start complex multi-step development work with existing specifications.
license: MIT
metadata:
  version: "2.3.0"
---

# Writing Plan Skill

This skill is used for creating comprehensive implementation plans for multi-step development tasks. Use when you have a specification or requirements, and before directly touching any code.

---

## Reference Document Index

| Document | Purpose | When to Read |
|----------|---------|--------------|
| [plan-template.md](references/plan-template.md) | Plan template | Reference when writing plans |
| [plan-document-reviewer-prompt.md](references/plan-document-reviewer-prompt.md) | Review criteria | Reference when reviewing |
| [patterns.md](references/patterns.md) | Common plan pattern library | When common patterns identified |
| [planning-guides.md](references/planning-guides.md) | Dependency management, environment configuration, rollback strategy | When detailed planning needed |
| [change-management.md](references/change-management.md) | Plan change management | When changes occur |
| [quality-checklist.md](references/quality-checklist.md) | Quality checklist | During final check |
| [workflow-examples.md](references/workflow-examples.md) | Flowcharts and examples | When understanding workflows |

---

## Core Constraints

> ⚠️ The following rules must always be followed and never forgotten.

### Prohibited Actions (Until Plan Complete)

Before the plan is complete, **absolutely prohibited**:

- ❌ Invoke any implementation skill
- ❌ Write any code
- ❌ Create or modify project files (except plan documents)
- ❌ Take any implementation action

**No exceptions**: No matter how simple the project appears, this workflow must be followed.

### Termination Condition

The **only way to terminate** this skill is by completing the plan document and notifying the user that it's ready for execution.

### Activation Declaration

Upon skill activation, immediately declare:

> "I am using the writing-plan skill to create an implementation plan."

### Phase Declaration

At the start of each conversation round, declare the current progress:

> 【Plan Writing Phase X/7】Currently executing: [Phase Name]
> Current processing: [Subsystem Name] (if applicable)

---

## Target Audience Assumption

Assume the engineer reading this plan:

- Has **zero knowledge** of our codebase
- Has **questionable taste** in software design
- Is a **skilled developer** but unfamiliar with our tooling or problem domain
- Is **not familiar** with good testing design

Your plan must document everything they need to know.

### Core Values

- **DRY** (Don't Repeat Yourself) - No redundant information
- **YAGNI** (You Aren't Gonna Need It) - Only implement what's needed
- **TDD** (Test-Driven Development) - Write tests first
- **Frequent commits** - Commit after each working step

---

## Outline File Mechanism

**Purpose**: Solve the attention loss problem in multi-round conversations, uniformly manage project information, decision records, and progress.

**Operation**: Immediately create an outline file upon skill activation:

- **Path**: `design/plans/YYYY-MM-DD-<topic>-outline.md`
- **Purpose**: Record session state, decision records, project information, subsystem progress

**At the start of each conversation**:

1. Read outline file
2. Restore context based on outline file (including decisions already made)
3. Declare current phase

**After completing each subsystem plan**:

1. Update subsystem status in outline file
2. Check if can proceed to next subsystem

### Outline File Template

```markdown
# [Project Name] Implementation Plan Outline

## Session State

- **Specification Document**: [Source specification document path]
- **Current Phase**: Phase X/7: [Phase Name]
- **Current Processing**: [Subsystem Name or "Single Subsystem"]
- **Next Action**: [Specific action]
- **Pending Issues**: [Issue list, leave empty if none]

## Decision Records

| Decision | Rationale | Impact Scope | Decision Time |
|----------|-----------|-------------|---------------|
| [Decision content] | [Why this decision] | [Which modules/subsystems affected] | YYYY-MM-DD |

## Project Overview

[One sentence describing project goal]

## Subsystem Division (Fill for multi-subsystem projects)

### Subsystem A: [Name]

- **Scope**: [Feature scope description]
- **Dependency**: None
- **Plan Document**: `design/plans/YYYY-MM-DD-subsystem-a.md`
- **Status**: ⏳ Pending / 🔄 In Progress / ✅ Complete

## Execution Order (Fill for multi-subsystem projects)

1. Subsystem A (no dependency, execute first)
2. Subsystem B (depends on A)

## Shared Components (Fill for multi-subsystem projects)

| Component | Using Subsystems | Plan Location |
|-----------|-----------------|---------------|
| [Component name] | A, B | Defined in Subsystem A plan |

## Change History

| Change Time | Change Content | Impact Scope | Change Reason |
|------------|----------------|-------------|--------------|
| YYYY-MM-DD | [Change content] | [Impact scope] | [Change reason] |

## Global Constraints

- [Constraints applicable to all subsystems/the entire project]
```

**Single subsystem projects**: Only need to fill in "Session State", "Decision Records", "Project Overview", "Global Constraints", other sections can be omitted.

---

## Phase 1/7: Context and Scope Analysis

### 1.1 Receive Input

Receive from brainstorming skill:

- Specification document path
- Project background information

### 1.2 Create Outline File

Immediately create outline file: `design/plans/YYYY-MM-DD-<topic>-outline.md`

### 1.3 Scope Check and Subsystem Identification

**Key**: Before proceeding, evaluate if the specification covers multiple independent subsystems.

**Subsystem Identification Criteria**:

| Characteristic | Description |
|---------------|-------------|
| Independent data model | Subsystem has independent data structure |
| Independent interface | Subsystem provides independent API externally |
| Independent deployment | Subsystem can be deployed and run independently |
| Clear boundaries | Subsystems communicate through explicit interfaces |

**Handling Strategy**:

- **Single subsystem**: Proceed directly to Phase 2
- **Multiple subsystems**: Proceed to multi-subsystem handling flow (see [workflow-examples.md](references/workflow-examples.md))

### 1.4 Multi-Subsystem Handling Flow

When multiple subsystems are identified:

**Step 1: Analyze Subsystem Dependencies**

Record dependency analysis in outline file:

```markdown
## Subsystem Dependency Analysis

| Subsystem | Depends On | Depended On By |
|-----------|-----------|---------------|
| SubsystemA | None | B, C |
| SubsystemB | A | C |
```

**Step 2: Enhance Outline File**

Fill in "Subsystem Division", "Execution Order", "Shared Components" sections of the outline file.

**Step 3: Write Plans for Subsystems One by One

- Only handle one subsystem at a time
- Before starting, read outline to confirm dependencies are satisfied
- After completion, update status in outline
- Continue to next subsystem

### 1.5 Ask About Save Location

Ask user where to save the plan:

- Default directory: `design/plans/`
- File name format: `YYYY-MM-DD-<feature-name>.md`

### 1.6 Record Key Decisions

During plan writing, must record decisions when encountering:

| Decision Type | Example |
|--------------|---------|
| Technology selection | Choose framework, library, database |
| Architecture decision | Layered structure, communication method |
| Design pattern | Which design pattern to use |
| Implementation strategy | How to handle edge cases |

### 1.7 Scope Review

Present scope analysis results to user for confirmation:

> "Scope analysis complete. Please confirm the following:
>
> **Subsystem Division**: [List identified subsystems]
> **Dependency Relationships**: [List dependency relationships]
> **Execution Order**: [List execution order]
> **Key Decisions**: [List recorded decisions]
>
> Is the above correct? Please let me know if any adjustments are needed."

**Completion Criteria**:

- Outline file created
- Subsystems identified and recorded
- Save location confirmed
- Key decisions recorded

---

## Phase 2/7: File Structure Planning

**Before defining tasks**, plan which files will be created or modified and their responsibilities.

### 2.1 Design Principles

- **Single Responsibility**: Each file should have a single clear responsibility
- **Context Friendly**: Code that can be understood in one context window
- **Focused Files**: Prefer small, focused files over large multi-purpose files
- **Colocation**: Files that change together should be placed together
- **Split by Responsibility**: Organize by responsibility, not by technical layer

### 2.2 Existing Codebase Patterns

In existing codebase:

- Follow established patterns
- Don't unilaterally refactor large files
- If modifying bloated files, **ask developer** if refactoring should be included in the plan

### 2.3 File Structure Template

```markdown
## File Structure

### New Files
- `path/to/new/file.<ext>` - Responsibility description

### Modify Files
- `path/to/existing/file.<ext>` - Content to be modified

### Test Files
- `tests/path/to/test_file.<ext>` - Test responsibility
```

### 2.4 Structure Review

Present file structure to user for confirmation:

> "File structure planning complete. Please confirm the following:
>
> **New Files**: [List new files and responsibilities]
> **Modify Files**: [List modify files and modifications]
> **Test Files**: [List test files]
>
> Is the above file structure reasonable? Please let me know if any adjustments are needed."

---

## Phase 3/7: Plan Document Title

Each plan must start with this title:

```markdown
# [Feature Name] Implementation Plan

> **For Agent Workers:** Required: Use executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** [One sentence describing what this feature builds]

**Architecture:** [2-3 sentences about the approach]

**Tech Stack:** [Key technologies/libraries]

**Outline File:** [Outline file path] (if applicable)
```

---

## Phase 4/7: Task Definition

### 4.1 Task Granularity

Each step should correspond to **one operation** (takes 2-5 minutes).

### 4.2 Task Structure Template

```markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.<ext>`
- Modify: `exact/path/to/existing.<ext>#L123-145`
- Test: `tests/exact/path/to/test.<ext>`

- [ ] **Step 1: Write failing test**

```<language>
// Example code
```

- [ ] **Step 2: Run test to verify failure**

Run: `<test-command>`
Expected: Fail, showing appropriate error message

- [ ] **Step 3: Write minimal implementation**

```<language>
// Minimal implementation that passes the test
```

- [ ] **Step 4: Run test to verify pass**

Run: `<test-command>`
Expected: Pass

### 4.3 Test Commands by Language

| Language | Test Framework | Command |
|---------|----------------|---------|
| TypeScript/JavaScript | Jest | `npm test` or `jest tests/path/test.ts` |
| TypeScript/JavaScript | Vitest | `vitest run tests/path/test.ts` |
| Python | pytest | `pytest tests/path/test.py::test_name -v` |
| Rust | cargo test | `cargo test test_name` |
| Go | go test | `go test ./path/to/package -run TestName` |
| Java | JUnit | `mvn test -Dtest=TestClassName` |
| C# | xUnit/NUnit | `dotnet test --filter TestName` |

### 4.4 Task Requirements

- **Precise file paths** - No ambiguous references
- **Complete code in plan** - Not "add validation" but actual code
- **Precise commands** - Exact commands and expected output
- **Test-first approach** - Each task starts with failing test
- **Language adaptation** - Use project's programming language for all examples

### 4.5 Task Review

Present task overview to user for confirmation:

> "Task definition complete. Please confirm the following:
>
> **Total Tasks**: [Count]
> **Task List**:
> 1. [Task Name] - [File]
> ...
>
> Is the above task definition reasonable? Please let me know if any adjustments are needed."

---

## Phase 5/7: Chunking Output and Review

### 5.1 Chunking Strategy

| Metric | Standard | Reason |
|--------|----------|--------|
| Lines | 300-500 lines | Fit AI context window |
| Tasks | 5-10 tasks | Maintain logical integrity |
| Dependencies | Self-contained within chunk | Reduce cross-chunk references |

**Chunk Boundary Identification**:

1. **Chunk by functional module**: Related tasks belong to one chunk
2. **Chunk by implementation phase**: Such as "infrastructure", "core features", "integration testing"
3. **Chunk by subsystem**: Each subsystem is one chunk

### 5.2 Chunk Format

```markdown
## Chunk 1: Infrastructure

### Task 1: Project Initialization
...

---

## Chunk 2: Core Features

### Task 3: Data Model
...
```

### 5.3 Review Trigger Matrix

| Trigger Point | Review Type | Review Scope | Review Method |
|--------------|-------------|-------------|--------------|
| Phase 1 complete | Scope Review | User confirmation |
| Phase 2 complete | Structure Review | Subsystem identification, dependency relationships | User confirmation |
| Phase 4 complete | Task Review | Task definition | User confirmation |
| Each chunk complete | Chunk Review | Code completeness, test coverage, precise paths | Sub-agent review |
| Subsystem complete | Subsystem Review | Overall consistency, dependency satisfaction, shared components | Sub-agent review |
| All complete | Final Review | All plans | User confirmation |
| Change occurs | Change Review | Overall quality, execution order, outline completeness | Sub-agent review |
| | | Change impact scope | Sub-agent review |

Detailed review criteria: see [plan-document-reviewer-prompt.md](references/plan-document-reviewer-prompt.md).

### 5.4 Chunk-Level Review Flow

After completing each plan chunk:

1. **Dispatch plan document reviewer sub-agent** to review current chunk
2. **If issues found (❌)**: Fix issues, re-review
3. **If approved (✅)**: Continue to next part

### 5.5 Handling Multi-Subsystem Scenarios

**After each subsystem completes**:

1. Update subsystem status in outline file
2. Confirm next subsystem's dependencies are satisfied
3. Start writing plan for next subsystem

**Coordination between subsystems**:

- Shared components defined in first subsystem that uses them
- Subsequent subsystems reference already-defined shared components
- Record shared component locations in outline file

---

## Phase 6/7: Plan Save and Confirmation

### 6.1 Save Plan

1. Save plan to user-specified directory (default: `design/plans/`)
2. Use file name format: `YYYY-MM-DD-<feature-name>.md`
3. Update outline file to mark complete

### 6.2 Final Review

Execute final review (checklist: see [quality-checklist.md](references/quality-checklist.md)):

1. **Overall quality check**
2. **Execution order verification**
3. **Outline completeness check**

### 6.3 User Confirms Plan

After final review passes, **must ask user to confirm plan content**:

> "Plan complete and saved. Please confirm the following:
>
> **Plan Document**: `design/plans/<filename>.md`
> **Key Decisions**: [List 2-3 most important decisions]
> **Execution Order**: [List task/subsystem execution order]
>
> Does the plan content meet expectations? Please let me know if any modifications are needed."

---

## Phase 7/7: Execution Handover

### 7.1 Ask About Execution Intent

After user confirms plan, **ask about execution intent**:

> "Plan confirmed. Would you like to start executing the plan now?
>
> Options:
> - **Execute now**: Execute the plan in current session via executing-plans skill
> - **Execute later**: Save the plan, execute manually later"

### 7.2 Wait for User Confirmation

**If user selects "Execute now"**:

Invoke executing-plans skill, passing the following parameters:

- **Plan Document Path**: `design/plans/YYYY-MM-DD-<feature-name>.md`
- **Outline File Path** (if applicable): `design/plans/YYYY-MM-DD-<topic>-outline.md`
- **Specification Document Path** (if applicable): Specification document path

**Invocation format**:

```
Invoke executing-plans skill with the following parameters:
- Plan document path: design/plans/YYYY-MM-DD-<feature-name>.md
- Outline file path: design/plans/YYYY-MM-DD-<topic>-outline.md (if applicable)
- Specification document path: design/specs/YYYY-MM-DD-<topic>-design.md (if applicable)
```

**Multi-subsystem projects**: Pass all subsystem plan document paths in execution order.

**If user selects "Execute later"**: End this skill, inform user they can execute via executing-plans skill later

---

## Change Management

When user requests plan modifications, execute the change management process. Detailed process: see [change-management.md](references/change-management.md).

**Core steps**:

1. Register change (in outline file "Change History" table)
2. Impact analysis
3. Update plan
4. Change review
5. Notify user

---

## Common Plan Patterns

When common patterns are identified, directly reference predefined templates. Detailed patterns: see [patterns.md](references/patterns.md).

| Pattern | Applicable Scenario |
|---------|--------------------|
| CRUD Module | Data create, read, update, delete operations |
| Authentication Module | User authentication and authorization |
| API Integration | Third-party service integration |
| Middleware/Plugin | Request handling pipeline, plugin systems |

---

## Dependency and Environment Planning

Detailed guide: see [planning-guides.md](references/planning-guides.md), including:

- Dependency management planning
- Environment configuration planning
- Rollback strategy planning

---

## Flowcharts and Examples

Detailed flowcharts and workflow examples: see [workflow-examples.md](references/workflow-examples.md), including:

- Plan writing flowchart
- Multi-subsystem handling flowchart
- Workflow examples
- Common issue handling
