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

- **Primary Users**: [User groups]
- **Use Cases**: [Typical use cases]

## Constraints

- **Technical Limitations**: [Tech stack, framework limitations]
- **Time Limitations**: [Delivery time requirements]
- **Resource Limitations**: [Manpower, budget limitations]

## Success Criteria

- [ ] [Verifiable delivery criterion 1]
- [ ] [Verifiable delivery criterion 2]

## Architecture Design

### System Structure

[Overall system architecture description]

### Component Division

| Component | Responsibility | Dependencies |
|-----------|---------------|--------------|
| [Component Name] | [Responsibility Description] | [Dependent Components] |

## Data Flow

[How data flows, can use text or simple diagrams]

## Error Handling

| Error Type | Handling Method |
|------------|-----------------|
| [Error Type] | [Handling Strategy] |

## Testing Strategy

- **Unit Tests**: [Test scope]
- **Integration Tests**: [Test scope]
- **Acceptance Criteria**: [Pass conditions]

## Decision Record

| Decision | Rationale | Impact |
|----------|-----------|--------|
| [Decision Content] | [Why] | [Impact Scope] |
```

---

## Quality Requirements

- No TODO, TBD, or placeholder content
- All sections have complete content
- Success criteria are verifiable
- Decisions have clear rationale
