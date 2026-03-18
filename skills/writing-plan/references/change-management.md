# Plan Change Management

Handle change requests during plan writing to ensure controllable change impact.

---

## Table of Contents

- [Change Types](#change-types)
- [Change Handling Process](#change-handling-process)
- [Change Decision Record](#change-decision-record)

---

## Change Types

| Change Type | Description | Impact Level |
|------------|-------------|-------------|
| New feature | Add new feature requirements | High |
| Modify requirements | Change existing requirements | Medium-High |
| Delete feature | Remove planned feature | Medium |
| Technical adjustment | Change technical solution | Medium-High |
| Priority adjustment | Change execution order | Low-Medium |

---

## Change Handling Process

### Step 1: Register Change

Record in the outline file's "Change History" table:

```markdown
| Change Time | Change Content | Impact Scope | Change Reason |
|------------|---------------|-------------|--------------|
| YYYY-MM-DD | Add cache layer | Subsystem A | Performance optimization requirement |
```

### Step 2: Impact Analysis

Analyze the scope of change impact:

```markdown
## Change Impact Analysis

**Change Content**: [Specific change description]

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
```

### Step 3: Update Plan

1. Update impacted plan documents
2. Update decision records in outline file (if new decisions made)
3. Update subsystem status (if needed)

### Step 4: Change Review

Conduct special review for changed parts:

- Review if changes are complete
- Review if impact analysis is accurate
- Review if anything is missed

### Step 5: Notify User

After change is complete, notify user:

> "Change complete. Impact scope: [Impact scope]. Updated documents: [Document list]."

---

## Change Decision Record

If change involves new technical decisions, must record:

```markdown
| Decision | Rationale | Impact Scope | Decision Time |
|----------|-----------|-------------|--------------|
| [Change-related decision] | [Why] | [Impact] | YYYY-MM-DD |
```
