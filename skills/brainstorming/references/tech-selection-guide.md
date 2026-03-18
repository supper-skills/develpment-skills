# Technology Selection Guide

This document provides a systematic technology selection evaluation framework, consulted as needed during the brainstorming phase.

---

## Evaluation Dimensions

| Dimension | Key Considerations | Evaluation Questions |
|-----------|-------------------|---------------------|
| Team Familiarity | Team experience, learning curve | Does the team have relevant experience? What's the learning cost? |
| Community Ecosystem | Documentation quality, community activity | Is documentation complete? Can solutions be found for problems? |
| Long-term Maintenance | Project activity, version updates | Is the project continuously maintained? How is backward compatibility? |
| Performance Characteristics | Performance, known bottlenecks | Does it meet performance requirements? Any known issues? |
| Integration Difficulty | Compatibility, migration cost | How compatible with existing systems? What's the migration cost? |

---

## Selection Process

```
1. Clarify technical constraints
   ├── Team skill inventory
   ├── Existing tech stack
   └── Budget/time constraints

2. List candidate technical solutions (usually 2-3)

3. Comparative analysis by evaluation dimensions

4. Provide recommended solution with rationale

5. Document selection decision and trade-offs
```

---

## Decision Documentation Template

Document technology selection decisions in the specification:

```markdown
## Technology Selection Decision

### Candidate Solutions
| Solution | Team Familiarity | Community Ecosystem | Long-term Maintenance | Performance | Integration Difficulty |
|----------|-----------------|--------------------|-----------------------|-------------|----------------------|
| Solution A | High | High | High | Medium | Low |
| Solution B | Medium | High | High | High | Medium |
| Solution C | Low | Medium | Medium | High | High |

### Rationale for Selecting Solution A
- Team already has experience, low learning cost
- Good compatibility with existing systems
- Active community, problems easy to solve

### Trade-offs
- Performance slightly lower than Solution B, but meets requirements
- Sacrificed some performance for development efficiency
```

---

## Common Pitfalls

| Pitfall | Manifestation | Response Strategy |
|---------|---------------|-------------------|
| Chasing trends | Choosing new technology just because it's "popular" | Evaluate actual needs match |
| Ignoring learning costs | Underestimating team learning time | Reserve learning buffer |
| Lacking maintenance support | Selecting abandoned projects | Check project activity metrics |
| Over-engineering | Choosing overly complex solutions | Follow YAGNI principle |

---

## Technology Stack Evaluation Checklist

- [ ] Does the team have relevant experience?
- [ ] Is documentation complete?
- [ ] Is the community active (GitHub stars, issues, update frequency)?
- [ ] Does it meet performance requirements?
- [ ] How is compatibility with existing systems?
- [ ] Is migration cost acceptable?
- [ ] Is there long-term maintenance support?
- [ ] Are there known major issues?
