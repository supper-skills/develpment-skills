# Implementation Plan Template

This template shows the standard structure of an implementation plan. Adjust all file extensions, code examples, and test commands according to the project's programming language.

---

## Table of Contents

- [Outline File Template](#outline-file-template)
- [Single Subsystem Plan Template](#single-subsystem-plan-template)
- [Multi-Subsystem Plan Template](#multi-subsystem-plan-template)
- [Common Plan Pattern Templates](#common-plan-pattern-templates)
- [Language Examples](#language-examples)
- [Chunking Guide](#chunking-guide)
- [Change Impact Analysis Template](#change-impact-analysis-template)
- [Notes](#notes)

---

## Outline File Template

**Path**: `design/plans/YYYY-MM-DD-<topic>-outline.md`

The outline file uniformly manages session state, decision records, project information, and subsystem progress.

```markdown
# [Project Name] Implementation Plan Outline

## Session State

- **Specification Document**: [Source specification document path]
- **Current Phase**: Phase X/7: [Phase Name]
- **Current Processing**: [Subsystem Name or "Single Subsystem"]
- **Next Action**: [Specific action]
- **Pending Issues**: [Issue list, leave empty if none]

## Decision Records

> Record key decisions and rationale during plan writing to prevent repeated discussion of decided issues.

| Decision | Rationale | Impact Scope | Decision Time |
|----------|-----------|-------------|---------------|
| Use JWT instead of Session | Stateless, easy to scale | Authentication module | YYYY-MM-DD |
| Choose PostgreSQL | Team familiar, JSON support | Data layer | YYYY-MM-DD |
| Adopt microservices architecture | Independent deployment, flexible tech stack | Overall architecture | YYYY-MM-DD |

## Project Overview

[One sentence describing project goal]

## Subsystem Division (Fill for multi-subsystem projects)

### Subsystem A: [Name]

- **Scope**: [Feature scope description]
- **Dependency**: None
- **Plan Document**: `design/plans/YYYY-MM-DD-subsystem-a.md`
- **Status**: ⏳ Pending / 🔄 In Progress / ✅ Complete

### Subsystem B: [Name]

- **Scope**: [Feature scope description]
- **Dependency**: Subsystem A
- **Plan Document**: `design/plans/YYYY-MM-DD-subsystem-b.md`
- **Status**: ⏳ Pending

### Subsystem C: [Name]

- **Scope**: [Feature scope description]
- **Dependency**: Subsystem A, Subsystem B
- **Plan Document**: `design/plans/YYYY-MM-DD-subsystem-c.md`
- **Status**: ⏳ Pending

## Execution Order (Fill for multi-subsystem projects)

1. Subsystem A (no dependency, execute first)
2. Subsystem B (depends on A)
3. Subsystem C (depends on A, B)

## Shared Components (Fill for multi-subsystem projects)

| Component | Using Subsystems | Plan Location |
|-----------|-----------------|---------------|
| [Component name] | A, B, C | Defined in Subsystem A plan |
| [Component name] | B, C | Defined in Subsystem B plan |

## Change History

> Record change history for traceability and impact analysis.

| Change Time | Change Content | Impact Scope | Change Reason |
|------------|---------------|-------------|--------------|
| YYYY-MM-DD | Add cache layer | Subsystem A | Performance optimization requirement |

## Global Constraints

- [Constraints applicable to all subsystems/the entire project]
- [Tech stack requirements]
- [Coding standard requirements]
```

**Single subsystem projects**: Only need to fill in "Session State", "Decision Records", "Project Overview", "Global Constraints", other sections can be omitted.

---

## Single Subsystem Plan Template

**Path**: `design/plans/YYYY-MM-DD-<feature-name>.md`

```markdown
# [Feature Name] Implementation Plan

> **For Agent Workers:** Required: Use executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** [One sentence describing what this feature builds]

**Architecture:** [2-3 sentences about the approach]

**Tech Stack:** [Key technologies/libraries]

---

## File Structure

### New Files
- `path/to/new/file.<ext>` - Responsibility description
- `path/to/another/file.<ext>` - Responsibility description

### Modify Files
- `path/to/existing/file.<ext>` - Content to be modified
- `path/to/another/existing.<ext>` - Content to be modified

### Test Files
- `tests/path/to/test_file.<ext>` - Test responsibility

---

## Chunk 1: [Component Name]

### Task 1: [Component Name]

**Files:**
- Create: `exact/path/to/file.<ext>`
- Modify: `exact/path/to/existing.<ext>#L123-145`
- Test: `tests/exact/path/to/test.<ext>`

- [ ] **Step 1: Write failing test**

```<language>
// Adjust to your language
// Example: TypeScript with Jest
describe('functionName', () => {
  it('should return expected result for given input', () => {
    const result = functionName(input);
    expect(result).toBe(expected);
  });
});
```

- [ ] **Step 2: Run test to verify failure**

Run: `<test-command>` (e.g., `npm test`, `pytest`, `cargo test`)
Expected: Fail, showing appropriate error message

- [ ] **Step 3: Write minimal implementation**

```<language>
// Minimal implementation that passes the test
// Adjust to your language
export function functionName(input: InputType): OutputType {
  return expected;
}
```

- [ ] **Step 4: Run test to verify pass**

Run: `<test-command>`
Expected: Pass

---

### Task 2: [Another Component]

**Files:**
- Create: `exact/path/to/another.<ext>`
- Test: `tests/exact/path/to/test_another.<ext>`

- [ ] **Step 1: Write failing test**

```<language>
// Adjust to your language
```

- [ ] **Step 2: Run test to verify failure**

Run: `<test-command>`
Expected: Fail

- [ ] **Step 3: Write minimal implementation**

```<language>
// Adjust to your language
```

- [ ] **Step 4: Run test to verify pass**

Run: `<test-command>`
Expected: Pass

---

## Chunk 2: [Integration/Next Component]

[Continue adding more tasks in the same pattern...]

---
```

---

## Multi-Subsystem Plan Template (Subsystem Document)

**Path**: `design/plans/YYYY-MM-DD-subsystem-<name>.md`

```markdown
# [Subsystem Name] Implementation Plan

> **For Agent Workers:** Required: Use executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** [One sentence describing what this subsystem builds]

**Architecture:** [2-3 sentences about the approach]

**Tech Stack:** [Key technologies/libraries]

**Outline File:** `design/plans/YYYY-MM-DD-<project>-outline.md`

**Dependency Subsystem:** [List dependent subsystems, or "None" if none]

---

## File Structure

### New Files
- `path/to/new/file.<ext>` - Responsibility description

### Modify Files
- `path/to/existing/file.<ext>` - Content to be modified

### Test Files
- `tests/path/to/test_file.<ext>` - Test responsibility

### Shared Components (For other subsystems to use)
- `path/to/shared/component.<ext>` - [Using subsystem list]

---

## Chunk 1: [Component Name]

### Task 1: [Component Name]

**Files:**
- Create: `exact/path/to/file.<ext>`
- Test: `tests/exact/path/to/test.<ext>`

- [ ] **Step 1: Write failing test**

```<language>
// Adjust to your language
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

---

[Continue adding more tasks and chunks...]
```

---

## Common Plan Pattern Templates

### Pattern 1: CRUD Module

**Applicable Scenario**: Data create, read, update, delete operations

**Reference Method**:

```markdown
### Task Group: [Entity Name] CRUD

> Reference Pattern: CRUD Module
> Entity: [EntityName]

**Files:**
- Create: `src/models/[entity].ts` - Data model definition
- Create: `src/repositories/[entity]Repository.ts` - Data access layer
- Create: `src/services/[entity]Service.ts` - Business logic layer
- Create: `src/controllers/[entity]Controller.ts` - API controller
- Create: `tests/[entity].test.ts` - Test file

[Write specific tasks based on pattern template...]
```

### Pattern 2: Authentication Module

**Applicable Scenario**: User authentication and authorization

**Reference Method**:

```markdown
### Task Group: User Authentication

> Reference Pattern: Authentication Module

**Files:**
- Create: `src/auth/jwtHandler.ts` - JWT token handling
- Create: `src/auth/middleware.ts` - Authentication middleware
- Create: `src/auth/refreshHandler.ts` - Token refresh
- Create: `src/services/userService.ts` - User service
- Create: `tests/auth.test.ts` - Authentication test

[Write specific tasks based on pattern template...]
```

### Pattern 3: API Integration

**Applicable Scenario**: Third-party service integration

**Reference Method**:

```markdown
### Task Group: [Service Name] Integration

> Reference Pattern: API Integration
> Service: [ServiceName]

**Files:**
- Create: `src/clients/[service]Client.ts` - API client
- Create: `src/adapters/[service]Adapter.ts` - Data adapter
- Create: `src/services/[service]Service.ts` - Business encapsulation
- Create: `src/mocks/[service]Mock.ts` - Mock implementation
- Create: `tests/[service].test.ts` - Integration test

[Write specific tasks based on pattern template...]
```

---

## Language Examples

### TypeScript/JavaScript (Jest)

```typescript
describe('UserService', () => {
  it('should create a new user', () => {
    const user = UserService.create({ name: 'John' });
    expect(user.name).toBe('John');
  });
});
```

Run: `npm test` or `jest tests/path/test.ts`

### Python (pytest)

```python
def test_create_user():
    user = UserService.create(name='John')
    assert user.name == 'John'
```

Run: `pytest tests/path/test.py::test_create_user -v`

### Rust

```rust
#[test]
fn test_create_user() {
    let user = UserService::create("John");
    assert_eq!(user.name, "John");
}
```

Run: `cargo test test_create_user`

### Go

```go
func TestCreateUser(t *testing.T) {
    user := UserService.Create("John")
    if user.Name != "John" {
        t.Errorf("expected John, got %s", user.Name)
    }
}
```

Run: `go test ./path/to/package -run TestCreateUser`

---

## Chunking Guide

### Chunking Granularity Standards

| Metric | Standard | Reason |
|--------|----------|--------|
| Lines | 300-500 lines | Fit AI context window |
| Tasks | 5-10 tasks | Maintain logical integrity |
| Dependencies | Self-contained within chunk | Reduce cross-chunk references |

### Chunk Boundary Identification

1. **Chunk by functional module**: Related tasks belong to one chunk
2. **Chunk by implementation phase**: Such as "infrastructure", "core features", "integration testing"
3. **Chunk by subsystem**: Each subsystem is one chunk

### Chunk Naming Suggestions

- `Chunk 1: Infrastructure` - Project initialization, dependency installation
- `Chunk 2: Data Model` - Core data structures
- `Chunk 3: Business Logic` - Main feature implementation
- `Chunk 4: API Interfaces` - External interfaces
- `Chunk 5: Integration Testing` - End-to-end testing

---

## Change Impact Analysis Template

When changes occur, use the following template to record impact analysis:

```markdown
## Change Impact Analysis

**Change Content**: [Specific change description]

**Change Type**: New feature / Modify requirements / Delete feature / Technical adjustment / Priority adjustment

**Directly Impacted Tasks**:
- Task X: [How impacted]
- Task Y: [How impacted]

**Indirectly Impacted Tasks**:
- Task Z: [How impacted]

**Impacted Subsystems**:
- Subsystem A: [How impacted]

**Documents to Update**:
- [ ] Plan Document A
- [ ] Outline File

**New Decisions** (if any):
| Decision | Rationale | Impact Scope | Decision Time |
|----------|-----------|-------------|--------------|
| [Decision content] | [Why] | [Impact] | YYYY-MM-DD |
```

---

## Notes

- Each chunk should be 300-500 lines, logically self-contained
- Each task follows TDD: test → fail → implement → pass
- Commit after each passing test
- All examples should be adjusted according to project's programming language
- Multi-subsystem projects must create outline file
- Update subsystem status in outline file after each subsystem completes
- Outline file uniformly manages session state, decision records, project information
- Key decisions must be recorded in outline file's "Decision Records" table
- Changes must be recorded in outline file's "Change History" table
- Common scenarios can reference predefined patterns to improve efficiency
