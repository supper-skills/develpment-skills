# Specification Document Template

This document provides the standard structure for design specification documents.

---

## Document Path

```
design/specs/YYYY-MM-DD-<topic>-design.md
```

---

## Template

```markdown
# [Feature Name] Design Specification

## Overview

[Feature goals and background, 1-2 paragraphs]

## Goal Positioning

- **Primary Users**: [User group]
- **Use Cases**: [Typical use cases]

## Constraints

- **Technical Constraints**: [Tech stack, framework limitations]
- **Time Constraints**: [Delivery time requirements]
- **Resource Constraints**: [Manpower, budget limitations]

## Success Criteria

- [ ] [Verifiable delivery criterion 1]
- [ ] [Verifiable delivery criterion 2]

## Architecture Design

### System Structure

[System overall architecture description]

### Component Division

| Component | Responsibility | Dependencies |
|------|------|------|
| [Component name] | [Responsibility description] | [Dependency components] |

## Data Flow

[How data flows, can use text or simple diagrams]

## Error Handling

| Error Type | Handling Method |
|----------|----------|
| [Error type] | [Handling strategy] |

## Testing Strategy

- **Unit Tests**: [Test scope]
- **Integration Tests**: [Test scope]
- **Acceptance Criteria**: [Pass conditions]

## Decision Records

| Decision | Rationale | Impact |
|------|------|------|
| [Decision content] | [Why] | [Impact scope] |
```

---

## Quality Requirements

- No TODOs, TBDs, or placeholders
- All sections have complete content
- Success criteria are verifiable
- Decisions have clear rationale
