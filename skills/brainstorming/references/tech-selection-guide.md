# Technology Selection Guide

This document provides the evaluation framework for technology selection.

---

## Evaluation Dimensions

| Dimension | Evaluation Questions |
|------|----------|
| Team Familiarity | Does the team have existing experience? What's the learning cost? |
| Community Ecosystem | Is documentation complete? Can you find solutions when problems arise? |
| Long-term Maintenance | Is the project continuously maintained? How is backward compatibility? |
| Performance Characteristics | Does it meet performance requirements? Any known issues? |
| Integration Difficulty | How is compatibility with existing systems? What's the migration cost? |

---

## Selection Process

1. Clarify technical constraints (team skills, existing tech stack, budget/time limits)
2. List candidate solutions (typically 2-3)
3. Compare and analyze according to evaluation dimensions
4. Provide recommended solution with rationale
5. Record selection decision in specification document

---

## Decision Record Template

```markdown
## Technology Selection Decision

### Candidate Solutions Comparison

| Solution | Team Familiarity | Community Ecosystem | Long-term Maintenance | Performance | Integration Difficulty |
|------|------------|----------|----------|----------|----------|
| Solution A | High | High | High | Medium | Low |
| Solution B | Medium | High | High | High | Medium |

### Selection Rationale

[Why this solution was chosen]

### Trade-offs Considered

[What was sacrificed in exchange for what]
```

---

## Common Pitfalls

| Pitfall | Response Strategy |
|------|----------|
| Chasing trends | Evaluate actual requirements match |
| Ignoring learning costs | Reserve learning buffer period |
| Lack of maintenance support | Check project activity metrics |
| Over-engineering | Follow YAGNI principle |
