---
name: project-context
description: Project context management skill for managing user profiles and project context. This skill is invoked by brainstorming and executing-plans skills, not triggered independently. Called when brainstorming activates to get user profile, and automatically updates project context when executing-plans completes.
license: MIT
metadata:
  version: "3.0.1"
---

# Project Context Skill

This skill manages user profiles and project context, providing context information to other skills.

---

## Core Responsibilities

| Responsibility | Description | Maintenance Method |
|----------------|-------------|-------------------|
| User Profile Read | Load user profile, provide user information to brainstorming | Agent automatic |
| User Profile Update | Identify user preferences during conversation, automatically update profile | Agent automatic |
| Project Context Management | Record project current status, provide background for future planning | Agent automatic (when executing-plans completes) |

---

## File Locations

| File | Path | Purpose |
|------|------|---------|
| User Profile | `design/context/user-profile.md` | Cross-session user preferences |
| Project Context | `design/context/project-context.md` | Project ongoing status records |

---

## User Profile

### Basic Information

| Field | Content | Update Date |
|-------|---------|-------------|
| User Positioning | [Senior Developer/Mid-level Developer/Product Manager/Other] | - |
| Technical Background | [Main languages, frameworks, tech stack used] | - |
| First Record | YYYY-MM-DD | - |
| Last Update | YYYY-MM-DD | - |

### Technical Preferences

| Type | Preference | Notes |
|------|------------|-------|
| Frontend Framework | [React/Vue/Angular/Other] | - |
| Backend Language | [Node.js/Python/Go/Rust/Other] | - |
| Code Style | [Specific standards or style description] | - |

### Decision Tendencies

| Scenario | Tendency | Performance |
|----------|----------|-------------|
| Routine Development | [Quality First/Efficiency First/Balanced] | [Specific performance] |
| Urgent Situations | [Quality First/Efficiency First/Balanced] | [Specific performance] |
| Refactoring Scenarios | [Quality First/Efficiency First/Balanced] | [Specific performance] |

### Risk Preferences

- **Technology Selection**: [Conservative/Moderate/Aggressive]
- **Refactoring Decisions**: [Small Steps/Medium Iterations/Big Refactoring]
- **Dependency Introduction**: [Minimal Dependencies/Moderate Dependencies/Willing to Try New]

---

## Interaction Style

| Aspect | Preference | Description |
|--------|------------|-------------|
| Detail Level | [Detailed/Concise/Moderate] | - |
| Feedback Frequency | [Every Step/Key Milestones/After Completion] | - |
| Explanation Depth | [Deep Explanation/Summary/No Explanation Needed] | - |
| Question Format | [Multiple Choice/Open-ended/Both] | - |

---

## Capability Assessment

| Capability Area | Self-assessment Level | Notes |
|-----------------|----------------------|-------|
| Frontend Development | [Junior/Intermediate/Senior] | - |
| Backend Development | [Junior/Intermediate/Senior] | - |
| Architecture Design | [Junior/Intermediate/Senior] | - |
| Performance Optimization | [Junior/Intermediate/Senior] | - |

---

## Update History

| Date | Update Content | Trigger Scenario |
|------|---------------|------------------|
| YYYY-MM-DD | [Initial creation] | First conversation |
| YYYY-MM-DD | [Update content] | [Trigger scenario] |
