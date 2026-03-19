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

**Goal**: [One sentence describing what this feature builds]

**Architecture**: [2-3 sentences about the approach]

**Tech Stack**: [Key technologies/libraries]

---

## File Structure

### New Files
- `path/to/new/file.ts` - Responsibility description

### Modify Files
- `path/to/existing/file.ts` - Modification content description

### Test Files
- `tests/path/to/test.ts` - Test responsibility

---

## Task List

### Task 1: [Task Name]

**Files**:
- Create: `path/to/file.ts`
- Test: `tests/path/to/test.ts`

- [ ] **Step 1**: Write failing test
- [ ] **Step 2**: Run test to verify failure
- [ ] **Step 3**: Write minimal implementation
- [ ] **Step 4**: Run test to verify pass

### Task 2: [Task Name]

[Continue with the same pattern...]
```

---

## Multi-Subsystem Outline File Template

```markdown
# [Project Name] Implementation Plan Outline

## Subsystem Division

| Subsystem | Scope | Dependencies | Status |
|-----------|-------|--------------|--------|
| Subsystem A | [Scope] | None | Pending |
| Subsystem B | [Scope] | A | Pending |

## Execution Order

1. Subsystem A (no dependencies)
2. Subsystem B (depends on A)

## Shared Components

| Component | Using Subsystems | Definition Location |
|-----------|------------------|---------------------|
| [Component Name] | A, B | In Subsystem A plan |
```

---

## Chunking Guide

| Metric | Standard | Reason |
|--------|----------|--------|
| Lines | 300-500 lines | Fit context window |
| Tasks | 5-10 tasks | Maintain logical integrity |

**Chunk Boundaries**:
- Chunk by functional module
- Chunk by implementation phase (infrastructure, core features, integration testing)
- Chunk by subsystem

---

## Task Requirements

- Precise file paths, no ambiguous references
- Complete code in plan, not placeholders
- Precise commands and expected output
- Test-first approach (TDD)
- Each step should be completable in 2-5 minutes
