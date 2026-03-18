# Execution State File Template

This document provides the template structure for execution state files, used to solve the attention loss problem in multi-round conversations.

---

## State File Path

### Single Subsystem

```
design/plans/YYYY-MM-DD-<topic>-execution-state.md
```

### Multi-Subsystem Project

```
Top-level state file: design/plans/YYYY-MM-DD-<topic>-execution-state.md
│
├── Subsystem A State: design/plans/YYYY-MM-DD-<topic>-subsystem-a-execution.md
├── Subsystem B State: design/plans/YYYY-MM-DD-<topic>-subsystem-b-execution.md
└── Subsystem C State: design/plans/YYYY-MM-DD-<topic>-subsystem-c-execution.md
```

---

## Complete Template

### Single Subsystem Template

```markdown
# [Feature Name] Execution State

## Metadata

- **Plan Document**: [Plan document path]
- **Outline File**: [Outline file path] (if applicable)
- **Specification Document**: [Specification document path] (if applicable)
- **Start Time**: YYYY-MM-DD HH:mm
- **Last Updated**: YYYY-MM-DD HH:mm

## Execution Phase

Phase X/3: [Phase Name]

## Current Progress

- **Current Task**: [Task Number] - [Task Name]
- **Current Step**: [Step Number]
- **Next Action**: [Specific action]

## Task Progress

| Task | Status | Completed At | Notes |
|------|--------|-------------|-------|
| Task 1: [Name] | ✅ Complete | HH:mm | - |
| Task 2: [Name] | 🔄 In Progress | - | Step 2/4 |
| Task 3: [Name] | ⏳ Pending | - | - |

## Context Records

| Time | Operation | Result | Notes |
|------|-----------|--------|-------|
| HH:mm | [Operation description] | [Success/Failure] | [Notes] |

## Decision Records

| Decision | Rationale | Impact Scope | Decision Time |
|----------|-----------|-------------|---------------|
| [Decision content] | [Why this decision] | [Which modules affected] | HH:mm |

## Issues Encountered

### Resolved

| Issue | Solution | Resolved At |
|-------|----------|-------------|
| [Issue description] | [How it was resolved] | HH:mm |

### Pending

- [ ] [Issue description] - [Current status]

## Change Records

| Change Time | Change Content | Change Reason | Decision Time |
|------------|---------------|---------------|---------------|
| HH:mm | [Change content] | [Why changed] | HH:mm |

## Global Constraints

- [Global constraints applicable to entire execution]
```

### Multi-Subsystem Top-Level State File Template

```markdown
# [Project Name] Execution State

## Metadata

- **Outline File**: [Read-only, record source]
- **Number of Subsystems**: [Count]
- **Start Time**: YYYY-MM-DD HH:mm
- **Last Updated**: YYYY-MM-DD HH:mm

## Execution Phase

Phase X/3: [Phase Name]

## Subsystem Execution Progress

| Subsystem | Status | Execution State File |
|-----------|--------|-------------------|
| Subsystem A | ✅ Complete | subsystem-a-execution.md |
| Subsystem B | 🔄 In Progress | subsystem-b-execution.md |
| Subsystem C | ⏳ Pending | - |

## Current Subsystem

- **Current**: Subsystem B
- **Current Task**: Task 4 - [Task Name]
- **Next Action**: Execute task 5

## Context Records

| Time | Operation | Result | Notes |
|------|-----------|--------|-------|
| HH:mm | [Operation description] | [Success/Failure] | [Notes] |

## Issues Encountered

### Resolved

| Issue | Solution | Resolved At |
|-------|----------|-------------|
| [Issue description] | [How it was resolved] | HH:mm |

### Pending

- [ ] [Issue description] - [Current status]

## Global Constraints

- [Global constraints applicable to entire execution]
```

### Subsystem State File Template

```markdown
# Subsystem [Name] Execution State

## Metadata

- **Project**: [Project name]
- **Outline File**: [Outline file path] (read-only)
- **Plan Document**: [Subsystem plan path]
- **Dependency Subsystem**: [Names of dependent subsystems] (if none, write "None")
- **Dependency Status**: [Status of dependent subsystems] (if no dependency, write "None")
- **Start Time**: YYYY-MM-DD HH:mm
- **Last Updated**: YYYY-MM-DD HH:mm

## Execution Phase

Phase X/3: [Phase Name]

## Current Progress

- **Current Task**: [Task Number] - [Task Name]
- **Current Step**: [Step Number]
- **Next Action**: [Specific action]

## Subsystem Task Progress

| Task | Status | Completed At | Notes |
|------|--------|-------------|-------|
| Task 1: [Name] | ✅ Complete | HH:mm | - |
| Task 2: [Name] | 🔄 In Progress | - | Step 2/4 |
| Task 3: [Name] | ⏳ Pending | - | - |

## Context Records

| Time | Operation | Result | Notes |
|------|-----------|--------|-------|
| HH:mm | [Operation description] | [Success/Failure] | [Notes] |

## Shared Component Usage

| Component Name | Tasks Using It | Source Subsystem |
|---------------|---------------|-----------------|
| [Component name] | Task 2, 3 | Subsystem A |

## Issues Encountered

### Resolved

| Issue | Solution | Resolved At |
|-------|----------|-------------|
| [Issue description] | [How it was resolved] | HH:mm |

### Pending

- [ ] [Issue description] - [Current status]
```

---

## Field Descriptions

### Metadata

| Field | Description | Required |
|-------|-------------|----------|
| Plan Document | Path to the plan document being executed | Yes |
| Outline File | Path to associated outline file (read-only) | Required for multi-subsystem |
| Specification Document | Path to original specification document | No |
| Number of Subsystems | Number of subsystems in the project | Required for multi-subsystem |
| Start Time | Timestamp when execution started | Yes |
| Last Updated | Timestamp of last state file update | Automatic |

### Execution Phase

| Phase | Description |
|-------|-------------|
| Phase 1/3 | Load and Review Plan |
| Phase 2/3 | Execute Tasks |
| Phase 3/3 | Completion and Reporting |

### Task Status

| Status | Description |
|--------|-------------|
| ✅ Complete | Task completed, all verifications passed |
| 🔄 In Progress | Task is being executed |
| ⏳ Pending | Task not yet started |
| ⚠️ Blocked | Task blocked by issues |

### Subsystem Status

| Status | Description |
|--------|-------------|
| ✅ Complete | All subsystem tasks completed |
| 🔄 In Progress | Subsystem is being executed |
| ⏳ Pending | Subsystem not yet started (waiting for dependencies) |
| ⚠️ Blocked | Subsystem blocked by issues |

---

## Usage Instructions

### Single Subsystem

#### When Skill Activates

1. Create execution state file
2. Fill in metadata (plan document, start time, etc.)
3. Set execution phase to "Phase 1/3: Load and Review Plan"
4. Initialize task progress table (all tasks status "⏳ Pending")

#### At the Start of Each Conversation

1. Read execution state file
2. Restore context based on state file
3. Declare current phase

#### After Completing Each Task

1. Update task progress table (status "✅ Complete")
2. Record completion time
3. Update current task to next task
4. Update top-level state file (if exists)

### Multi-Subsystem

#### When Skill Activates

1. Read outline file, identify subsystems
2. Create top-level execution state file
3. Create independent execution state files for each subsystem
4. Fill in metadata, set all subsystem status to "⏳ Pending"

#### Subsystem Execution Flow

1. Check if dependencies are satisfied
2. Update subsystem status to "🔄 In Progress"
3. Update top-level state file's current subsystem
4. Execute Phase 1 → Phase 2 → Phase 3 for that subsystem
5. After subsystem completion, update subsystem status to "✅ Complete"
6. Update top-level state file's subsystem progress
7. Continue to next subsystem

#### When Resuming Execution

1. Read top-level execution state file
2. Identify interrupted subsystems
3. Check state files for completed subsystems
4. Verify dependency relationships
5. Continue execution from interruption location

---

## Comparison with Other Skill State Files

| Skill | State File | Path Format | Purpose |
|-------|-----------|-------------|---------|
| brainstorming | State file | `design/specs/YYYY-MM-DD-<topic>-state.md` | Track brainstorming phase |
| writing-plan | Outline file | `design/plans/YYYY-MM-DD-<topic>-outline.md` | Track plan writing phase |
| executing-plans | Execution state file | `design/plans/YYYY-MM-DD-<topic>-execution-state.md` | Track execution phase |

---

## Notes

1. **Do not modify outline file** - executing-plans only reads writing-plan's outline file, does not modify it
2. **State files stored independently** - All execution state information stored in executing-plans' own state files
3. **Subsystems and top-level separated** - Multi-subsystem projects use top-level state file + independent subsystem state files
4. Execution state files should be saved in the same directory as plan documents
5. Save file after each update to ensure state persistence
6. First read execution state file when resuming execution
7. Decision records help with subsequent review and issue tracing
