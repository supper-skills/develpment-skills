# Technology Selection Guide

This document provides a framework for technology selection evaluation.

---

## Evaluation Dimensions

| Dimension | Evaluation Questions |
|-----------|---------------------|
| Team Familiarity | Does the team have relevant experience? What's the learning cost? |
| Community Ecosystem | Is documentation complete? Can solutions be found for problems? |
| Long-term Maintenance | Is the project continuously maintained? How is backward compatibility? |
| Performance Characteristics | Does it meet performance requirements? Any known issues? |
| Integration Difficulty | How compatible with existing systems? What's the migration cost? |

---

## Selection Process

1. Clarify technical constraints (team skills, existing tech stack, budget/time constraints)
2. List candidate solutions (usually 2-3)
3. Comparative analysis by evaluation dimensions
4. Provide recommended solution with rationale
5. Record selection decision in specification document

---

## Decision Documentation Template

```markdown
## Technology Selection Decision

### Candidate Solutions Comparison

| Solution | Team Familiarity | Community Ecosystem | Long-term Maintenance | Performance Characteristics | Integration Difficulty |
|----------|------------------|---------------------|----------------------|----------------------------|----------------------|
| Solution A | High | High | High | Medium | Low |
| Solution B | Medium | High | High | High | Medium |

### Selection Rationale

[Why this solution was chosen]

### Trade-offs

[What was sacrificed, what was gained]
```

---

## Common Pitfalls

| Pitfall | Response Strategy |
|---------|-------------------|
| Chasing trends | Evaluate actual needs match |
| Ignoring learning costs | Reserve learning buffer |
| Lacking maintenance support | Check project activity metrics |
| Over-engineering | Follow YAGNI principle |
