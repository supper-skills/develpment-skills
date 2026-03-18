# Risk Assessment Template

This document provides a framework for risk identification and assessment during the design phase, consulted as needed during the brainstorming phase.

---

## Risk Categories

| Category | Example Risks | Typical Manifestations |
|----------|---------------|----------------------|
| Technical Risk | Untested technical solutions, unstable dependencies, performance bottlenecks | Tech stack selection mistakes, third-party service unavailability |
| Scope Risk | Requirement creep, vague feature boundaries, external system dependencies | Continuously changing requirements, project delays |
| Resource Risk | Insufficient manpower, tight schedules, skill gaps | Team member changes, compressed timelines |
| Integration Risk | Third-party API changes, complex data migration, compatibility issues | Unstable external dependencies, interface changes |
| Security Risk | Data leaks, authentication vulnerabilities, permission control flaws | Security vulnerabilities, data loss |

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

## Risk Assessment Process

```
1. Identify Risks
   └── List all risk factors that may impact the project

2. Assess Impact
   └── Classify by severity: High/Medium/Low

3. Assess Probability
   └── Estimate likelihood: High/Medium/Low

4. Develop Mitigation Strategies
   └── Develop response plans for high-impact/high-probability risks

5. Document Risk Register
   └── Include risk chapter in design document
```

---

## Risk Documentation Template

Document risk assessment in the specification:

```markdown
## Risk Assessment

| Risk Description | Category | Impact | Probability | Mitigation Strategy |
|-----------------|----------|--------|-------------|---------------------|
| Third-party API may change | Integration | High | Medium | Prepare alternatives, encapsulate call layer |
| Team members may change | Resource | Medium | Medium | Document key knowledge, cross-training |
| Performance may not meet targets | Technical | High | Low | Early performance testing, reserve optimization time |
```

---

## Mitigation Strategy Examples

| Strategy Type | Applicable Scenario | Example |
|--------------|---------------------|---------|
| Technical Validation | Uncertain technical solutions | Prototype unverified technical solutions |
| Incremental Delivery | High feature complexity | Split large features into independently deliverable smaller features |
| Backup Plan | Key dependency risks | Prepare alternatives for key dependencies |
| Monitoring and Alerting | Runtime risks | Establish monitoring mechanisms for key metrics |
| Documentation | Knowledge risks | Document key decisions and implementation details |

---

## Risk Assessment Checklist

- [ ] Have all technical risks been identified?
- [ ] Have all scope risks been identified?
- [ ] Have all resource risks been identified?
- [ ] Have all integration risks been identified?
- [ ] Have all security risks been identified?
- [ ] Do high-impact/high-probability risks have mitigation strategies?
- [ ] Are mitigation strategies specific and feasible?
