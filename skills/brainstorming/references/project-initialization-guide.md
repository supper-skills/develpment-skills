# Project Initialization Guide

This document provides additional considerations when creating a new project from scratch, consulted as needed during the brainstorming phase.

---

## Project Type Identification

| Type | Characteristics | Typical Tech Stack |
|------|-----------------|-------------------|
| Web Application | Browser access, frontend-backend separation | React/Vue/Next.js + Node/Python/Go |
| CLI Tool | Command-line interaction, script automation | Node.js/Python/Rust/Go |
| Library/SDK | Referenced by other projects, API design | TypeScript/Python/Rust |
| Microservice | Independent deployment, inter-service communication | Docker/Kubernetes + any language |
| Desktop Application | Local execution, GUI interface | Electron/Tauri/Qt |

---

## Project Structure Planning

### Confirmations

- [ ] Project type confirmed
- [ ] Directory structure designed
- [ ] Package manager selected
- [ ] Build tool selected

### Common Directory Structures

**Web Application (Frontend)**:
```
project/
├── src/
│   ├── components/    # Components
│   ├── hooks/         # Custom hooks
│   ├── pages/         # Pages
│   ├── services/      # API services
│   ├── utils/         # Utility functions
│   └── types/         # Type definitions
├── tests/
├── public/
└── package.json
```

**CLI Tool**:
```
project/
├── src/
│   ├── commands/      # Command handlers
│   ├── utils/         # Utility functions
│   └── index.ts       # Entry point
├── tests/
└── package.json
```

**Library/SDK**:
```
project/
├── src/
│   ├── index.ts       # Export entry
│   └── modules/       # Feature modules
├── tests/
├── examples/          # Usage examples
└── package.json
```

---

## Infrastructure Decisions

### Version Control Strategy

| Strategy | Applicable Scenario | Characteristics |
|----------|---------------------|-----------------|
| Git Flow | Large projects, multiple parallel versions | Many branches, strict process |
| GitHub Flow | Continuous deployment, small teams | Simple, main branch deployable |
| Trunk Based | High-frequency releases, mature CI/CD | Single main branch, feature flags |

### CI/CD Requirements Assessment

- [ ] Is automated testing needed?
- [ ] Is automated building needed?
- [ ] Is automated deployment needed?
- [ ] What is the deployment target environment?

### Containerization Requirements

- [ ] Is Docker support needed?
- [ ] Is Kubernetes orchestration needed?
- [ ] Is containerization needed for development environment?

---

## Key Question Checklist

The following questions must be confirmed with the user in project initialization scenarios:

### 1. Target Users

> "Who are the primary target users of this project?"

- Internal team use
- External developers
- End users
- Other

### 2. Project Scale

> "What is the expected project scale and complexity?"

- Small (1-2 person-months)
- Medium (3-6 person-months)
- Large (6+ person-months)

### 3. Environment Support

> "Does multi-environment support need to be provided (development, testing, production)?"

- Development environment only
- Development + Production
- Development + Testing + Production

### 4. Compliance and Security

> "Are there compliance or security requirements?"

- No special requirements
- Data security requirements
- Industry compliance requirements (e.g., GDPR, HIPAA)
- Other

---

## Project Initialization Checklist

- [ ] Project type confirmed
- [ ] Directory structure designed
- [ ] Package manager selected
- [ ] Build tool selected
- [ ] Version control strategy determined
- [ ] CI/CD requirements assessed
- [ ] Containerization requirements assessed
- [ ] Target users confirmed
- [ ] Project scale evaluated
- [ ] Environment support requirements confirmed
- [ ] Compliance and security requirements confirmed
