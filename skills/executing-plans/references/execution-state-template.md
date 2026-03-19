# Execution State File Template

This template is used to record state information during execution.

---

## Usage

Record execution-related content in the session state file `design/.session-state.md`.

---

## Execution State Recording Format

Append the following content to the session state file:

```markdown
## Execution State

### Plan Information

- **Plan Document**: [Plan file path]
- **Outline File**: [Outline file path] (if applicable)
- **Start Time**: YYYY-MM-DD HH:mm

### Task Progress

| Task | Status | Completion Time | Notes |
|------|--------|-----------------|-------|
| Task 1: [Name] | Complete | HH:mm | - |
| Task 2: [Name] | In Progress | - | Step 2/4 |
| Task 3: [Name] | Pending | - | - |

### Issues Encountered

| Issue | Solution | Resolved Time |
|-------|----------|---------------|
| [Issue description] | [How resolved] | HH:mm |
```

---

## Multi-Subsystem Recording

For multi-subsystem projects, append to the session state file:

```markdown
## Subsystem Progress

| Subsystem | Status | Plan Document |
|-----------|--------|---------------|
| Subsystem A | Complete | plans/subsystem-a.md |
| Subsystem B | In Progress | plans/subsystem-b.md |
| Subsystem C | Pending | plans/subsystem-c.md |
```
