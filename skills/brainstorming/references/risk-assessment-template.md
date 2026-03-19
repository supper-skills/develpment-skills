# Risk Assessment Template

This document provides a framework for risk identification and assessment during the design phase.

---

## Risk Categories

| Category | Example Risks |
|----------|---------------|
| Technical Risk | Untested technical solutions, unstable dependencies, performance bottlenecks |
| Scope Risk | Requirement creep, vague feature boundaries, external system dependencies |
| Resource Risk | Insufficient manpower, tight schedules, skill gaps |
| Integration Risk | Third-party API changes, complex data migration, compatibility issues |
| Security Risk | Data leaks, authentication vulnerabilities, permission control flaws |

---

## Risk Assessment Matrix

```
              Impact Level
            Low      Medium    High
       ┌────────┬────────┬────────┐
  High │ Monitor│ Mitigate│ Prioritize│
Prob     ├────────┼────────┼────────┤
ability  Medium│ Accept │ Monitor│ Mitigate│
         ├────────┼────────┼────────┤
    Low  │ Accept │ Accept │ Monitor│
         └────────┴────────┴────────┘
```

---

## Risk Documentation Template

Record risk assessment in the specification document:

```markdown
## Risk Assessment

| Risk Description | Category | Impact | Probability | Mitigation Strategy |
|-----------------|----------|--------|-------------|---------------------|
| [Risk] | [Category] | High/Medium/Low | High/Medium/Low | [Response plan] |
```

---

## Mitigation Strategy Examples

| Strategy Type | Applicable Scenario | Example |
|--------------|---------------------|---------|
| Technical Validation | Uncertain technical solutions | Prototype unverified technical solutions |
| Incremental Delivery | High feature complexity | Split large features into independently deliverable smaller features |
| Backup Plan | Key dependency risks | Prepare alternatives for key dependencies |
| Monitoring and Alerting | Runtime risks | Establish monitoring mechanisms for key metrics |
