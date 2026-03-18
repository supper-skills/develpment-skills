# Specification Document Reviewer Prompt

This document provides guidance for reviewing design specification documents.

## Review Purpose

Ensure every specification document meets quality standards before entering the implementation planning phase. The reviewer verifies completeness, consistency, and adherence to design principles.

## When to Deploy

After specification documents are written to the `design/specs/` directory.

---

## Review Checklist

### 1. Completeness

- [ ] No TODO markers or placeholder text
- [ ] No "TBD" or "to be defined" sections
- [ ] No statements like "will spec after X is completed"
- [ ] All sections have appropriate level of detail
- [ ] No sections noticeably more brief than others

### 2. Coverage

- [ ] Error handling covered
- [ ] Edge cases considered
- [ ] Integration points defined
- [ ] Data flow recorded
- [ ] Security considerations (if applicable)

### 3. Consistency

- [ ] No internal contradictions
- [ ] No conflicting requirements
- [ ] Consistent terminology usage
- [ ] External system references clear

### 4. Clarity

- [ ] No vague requirements
- [ ] Technical terms defined or self-evident
- [ ] Requirements testable/verifiable
- [ ] Acceptance criteria clear

### 5. YAGNI (You Aren't Gonna Need It)

- [ ] No unrequested features
- [ ] No over-engineering
- [ ] No speculative future预留
- [ ] Scope focused on declared requirements

### 6. Scope Validation

- [ ] Focused enough to produce a single implementation plan
- [ ] Not covering multiple independent subsystems
- [ ] If multiple subsystems exist, split already suggested
- [ ] Each subsystem can produce runnable, testable artifacts

### 7. Architecture Quality

- [ ] Units have clear boundaries
- [ ] Interface definitions clear
- [ ] Each unit independently understandable
- [ ] Each unit independently testable
- [ ] Each unit's function understandable without reading internal implementation
- [ ] Internal implementation can change without affecting consumers

---

## Issues Requiring Special Attention

### Placeholder Content

❌ Incorrect:
```
## Error Handling
TODO: Define error handling strategy
```

✅ Correct:
```
## Error Handling
- Network errors: Exponential backoff retry (max 3 times)
- Validation errors: Return 400 with detailed error messages
- Authentication errors: Return 401 and redirect to login page
```

### Vague Requirements

❌ Incorrect:
```
The system should be fast and secure.
```

✅ Correct:
```
The system should respond to API requests within 200ms (p95).
All API endpoints require JWT token authentication.
```

### Missing Boundaries

❌ Incorrect:
```
UserService handles user registration, authentication,
profile management, notifications, and analytics.
```

✅ Correct:
```
UserService handles user registration and authentication.
- ProfileService: Handles profile management
- NotificationService: Handles notifications
- AnalyticsService: Handles analytics
```

### Over-Engineering

❌ Incorrect:
```
We will implement a plugin system to allow future expansion
of features we may need in 2-3 years.
```

✅ Correct:
```
We will implement the specifically requested features.
Expansion points can be added when actual requirements arise.
```

---

## Review Output Format

After review, provide output in the following format:

```markdown
## Specification Review

**Status:** ✅ Approved | ❌ Issues Found

**Issues Found (if any):**
1. [Section Name]: [Specific Issue]
   - Why Important: [Explain]
   - Suggestion: [How to Fix]

**Strengths:**
- [What's done well]

**Suggestions (For Reference Only):**
- [Non-blocking suggestions]
```

---

## Review Guidance

1. **Thorough but Fair** - Focus on issues that would block implementation
2. **Explain Why** - When marking issues, explain why they matter
3. **Constructive** - Provide specific suggestions
4. **Consider Context** - Specifications are for engineers who will create implementation plans
5. **Value Clarity** - Vague specs lead to implementation failures
6. **Enforce Boundaries** - Unclear boundaries lead to code entanglement

---

## Escalation

If the same specification review loop exceeds 5 iterations:

1. Summarize all issues found across iterations
2. Document attempted solutions
3. Identify specific points of disagreement
4. Submit to human for guidance with complete context

---

## Review Example

### Input Specification

```markdown
# User Authentication Design

## Overview
Add user authentication functionality to the application.

## Requirements
- Users can log in
- Users can log out
- Sessions are secure

## Architecture
AuthService will handle everything related to authentication.
```

### Review Output

```markdown
## Specification Review

**Status:** ❌ Issues Found

**Issues Found:**
1. **Overview**: Too vague - Missing context of current system state
   - Why Important: Implementation approach depends on existing architecture
   - Suggestion: Add section describing current authentication state (none? legacy system?)

2. **Requirements**: Missing key details
   - Why Important: "Login" could mean multiple methods - password, SSO, OAuth?
   - Suggestion: Clarify authentication method (password+email, OAuth providers, etc.)

3. **Requirements**: "Sessions are secure" is not testable
   - Why Important: Cannot verify if requirement is met
   - Suggestion: Define specific security measures (HTTPS, token expiration, CSRF protection)

4. **Architecture**: AuthService boundaries unclear
   - Why Important: "Everything related to authentication" scope is too broad
   - Suggestion: Split into focused services (TokenService, SessionService, PasswordService)

**Strengths:**
- Goals clear in overview

**Suggestions (For Reference Only):**
- Consider adding error handling section
- Consider adding testing strategy section
```
