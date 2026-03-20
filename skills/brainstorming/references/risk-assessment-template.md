# Risk Assessment Template

This document provides the framework for risk identification and assessment during the design phase.

---

## Risk Categories

| Category | Example Risks |
|------|----------|
| Technical Risks | Unvalidated technical solutions, unstable dependencies, performance bottlenecks |
| Scope Risks | Requirement creep, fuzzy feature boundaries, external system dependencies |
| Resource Risks | Insufficient manpower, tight deadlines, skill gaps |
| Integration Risks | Third-party API changes, complex data migration, compatibility issues |
| Security Risks | Data leakage, authentication vulnerabilities, permission control flaws |

---

## Risk Assessment Matrix

```
              Impact Level
            Low      Medium     High
       ┌────────┬────────┬────────┐
 High  │ Monitor│ Mitigate│ Prioritize│
Proba  ├────────┼────────┼────────┤
bility Medium │ Accept │ Monitor│ Mitigate│
       ├────────┼────────┼────────┤
 Low   │ Accept │ Accept │ Monitor│
       └────────┴────────┴────────┘
```

---

## Risk Record Template

Record risk assessment in the specification document:

```markdown
## Risk Assessment

| Risk Description | Category | Impact | Probability | Mitigation Strategy |
|----------|------|------|------|----------|
| [Risk] | [Category] | High/Medium/Low | High/Medium/Low | [Response plan] |
```

---

## Mitigation Strategy Examples

| Strategy Type | Applicable Scenario | Example |
|----------|----------|------|
| Technical Validation | Uncertain technical solutions | Prototype validate uncertain technical solutions |
| Incremental Delivery | High feature complexity | Split large features into independently deliverable small features |
| Backup Plans | Key dependency risks | Prepare alternatives for key dependencies |
| Monitoring Alerts | Runtime risks | Establish monitoring mechanisms for key metrics |
