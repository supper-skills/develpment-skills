# Execution State Record Template

This template is used to record execution state information during the process.

---

## Usage

Record execution-related content in the session state file `design/.session-state.md`.

---

## Execution State Record Format

Append the following content in the session state file:

```markdown
## Execution State

### Plan Information

- **Plan Document**: [plan file path]
- **Outline Document**: [outline file path] (if applicable)
- **Start Time**: YYYY-MM-DD HH:mm

### Task Progress

| Task | Status | Completion Time | Notes |
|------|------|----------|------|
| Task 1: [Name] | Completed | HH:mm | - |
| Task 2: [Name] | In Progress | - | Step 2/4 |
| Task 3: [Name] | Pending | - | - |

### Issues Encountered

| Issue | Solution | Resolution Time |
|------|----------|----------|
| [Issue description] | [How it was solved] | HH:mm |
```

---

## Multi-Subsystem Records

For multi-subsystem projects, append the following in the session state file:

```markdown
## Subsystem Progress

| Subsystem | Status | Plan Document |
|--------|------|----------|
| SubsystemA | Completed | plans/subsystem-a.md |
| SubsystemB | In Progress | plans/subsystem-b.md |
| SubsystemC | Pending | plans/subsystem-c.md |
```
