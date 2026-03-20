# Implementation Plan Template

This document provides the standard structure for implementation plans.

---

## Document Path

```
design/plans/YYYY-MM-DD-<feature>.md
```

---

## Single Subsystem Plan Template

```markdown
# [Feature Name] Implementation Plan

**Goal**: [One-sentence description of what this feature builds]

**Architecture**: [2-3 sentences about the approach]

**Tech Stack**: [Key technologies/libraries]

---

## File Structure

### New Files
- `path/to/new/file.ts` - Responsibility description

### Modified Files
- `path/to/existing/file.ts` - Modification content description

### Test Files
- `tests/path/to/test.ts` - Test responsibilities

---

## Task List

### Task 1: [Task Name]

**Files**:
- Create: `path/to/file.ts`
- Test: `tests/path/to/test.ts`

- [ ] **Step 1**: Write failing test
- [ ] **Step 2**: Run test to verify failure
- [ ] **Step 3**: Write minimal implementation
- [ ] **Step 4**: Run test to verify passing

### Task 2: [Task Name]

[Continue with same pattern...]
```

---

## Multi-Subsystem Outline File Template

```markdown
# [Project Name] Implementation Plan Outline

## Subsystem Division

| Subsystem | Scope | Dependency | Status |
|--------|------|------|------|
| SubsystemA | [scope] | None | To be written |
| SubsystemB | [scope] | A | To be written |

## Execution Order

1. SubsystemA (no dependencies)
2. SubsystemB (depends on A)

## Shared Components

| Component | Using Subsystems | Definition Location |
|------|------------|----------|
| [Component name] | A, B | In SubsystemA plan |
```

---

## Chunking Guidelines

| Metric | Standard | Reason |
|------|------|------|
| Line Count | 300-500 lines | Fits context window |
| Task Count | 5-10 tasks | Maintains logical integrity |

**Chunk Boundaries**:
- Chunk by feature module
- Chunk by implementation phase (infrastructure, core features, integration tests)
- Chunk by subsystem

---

## Task Requirements

- Precise file paths, no vague references
- Complete code in plan, no placeholders
- Precise commands and expected output
- Test-driven development (TDD)
- Each step completable in 2-5 minutes
