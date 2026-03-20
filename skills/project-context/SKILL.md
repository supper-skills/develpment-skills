---
name: project-context
description: Project context management skill for managing user profiles and project context. This skill is invoked by brainstorming and executing-plans skills, not triggered independently. Invoked to get user profile when brainstorming is activated, automatically updates project context when executing-plans completes.
license: MIT
metadata:
  version: "3.0.1"
---

# Project Context Skill

This skill manages user profiles and project context, providing context information to other skills.

---

## Core Responsibilities

| Responsibility | Description | Maintenance Method |
|------|------|---------|
| User Profile Reading | Load user profile, provide user information for brainstorming | Agent automatic |
| User Profile Updating | Identify user preferences during dialogue, automatically update profile | Agent automatic + proactive trigger |
| Project Context Management | Record current project state, provide background for future planning | Agent automatic (when executing-plans completes) |

---

## Proactive Update Mechanism

### User Profile Proactive Update Triggers

⚠️ **Must proactively update user profile in the following situations**:

**Technical Preference Identification**:

- User explicitly expresses preference for a certain framework/library
- User shows tendencies in technical selection
- User demonstrates new tech stack usage experience

**Decision Tendency Identification**:

- User shows consistent tendencies across multiple decisions (quality first/efficiency first)
- User's attitude toward risk (conservative/aggressive)
- User's attitude toward refactoring (small frequent changes/big refactoring)

**Interaction Style Identification**:

- User preference for detailed explanations or concise descriptions
- User preference for multiple choice questions or open-ended questions
- User wants confirmation at each step or at key milestones

**Capability Assessment Updates**:

- User demonstrates capabilities beyond expectations in certain areas
- User needs more guidance in certain areas

### Project Context Proactive Update Triggers

⚠️ **Must proactively update project context in the following situations**:

**On Feature Completion**:

- Each feature implementation must be recorded to project context upon completion
- Record technical decisions and reasoning
- Record encountered problems and solutions

**On Architecture Changes**:

- Major changes in project structure
- Introduction of new dependencies or tech stacks
- Modifications to core design patterns

**On Test Status Updates**:

- Test coverage changes
- Test strategy adjustments
- Test framework changes

---

## File Locations

| File | Path | Purpose |
|------|------|------|
| User Profile | `design/context/user-profile.md` | Cross-session user preferences |
| Project Context | `design/context/project-context.md` | Project persistent state record |

---

## User Profile

### Basic Information

| Field | Content | Update Date |
|------|------|---------|
| User Positioning | [Senior Developer/Mid-level Developer/Product Manager/Other] | - |
| Technical Background | [Main languages, frameworks, tech stacks used] | - |
| First Recorded | YYYY-MM-DD | - |
| Last Updated | YYYY-MM-DD | - |

### Technical Preferences

| Type | Preference | Notes |
|------|------|------|
| Frontend Framework | [React/Vue/Angular/Other] | - |
| Backend Language | [Node.js/Python/Go/Rust/Other] | - |
| Code Style | [Specific standards or style description] | - |

### Decision Tendencies

| Scenario | Tendency | Manifestation |
|------|------|------|
| Regular Development | [Quality First/Efficiency First/Balance] | [Specific manifestation] |
| Emergency Situations | [Quality First/Efficiency First/Balance] | [Specific manifestation] |
| Refactoring Scenarios | [Quality First/Efficiency First/Balance] | [Specific manifestation] |

### Risk Appetite

- **Technical Selection**: [Conservative/Moderate/Aggressive]
- **Refactoring Decisions**: [Small frequent changes/Medium iterations/Big refactoring]
- **Dependency Introduction**: [Minimal dependencies/Moderate dependencies/Willing to try new things]

---

## Interaction Style

| Aspect | Preference | Description |
|------|------|------|
| Detail Level | [Detailed/Concise/Moderate] | - |
| Feedback Frequency | [Each step/Key milestones/After completion] | - |
| Explanation Depth | [In-depth explanation/Summary/No explanation needed] | - |
| Question Format | [Multiple choice/Open-ended/Both acceptable] | - |

---

## Capability Assessment

| Capability Area | Self-assessed Level | Notes |
|---------|---------|------|
| Frontend Development | [Junior/Mid-level/Senior] | - |
| Backend Development | [Junior/Mid-level/Senior] | - |
| Architecture Design | [Junior/Mid-level/Senior] | - |
| Performance Optimization | [Junior/Mid-level/Senior] | - |

---

## Update History

| Date | Update Content | Trigger Scenario |
|------|---------|---------|
| YYYY-MM-DD | [Initial creation] | First dialogue |
| YYYY-MM-DD | [Update content] | [Trigger scenario] |
