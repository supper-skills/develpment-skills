# Spec Document Reviewer Prompt

This document provides instructions for reviewing design specification documents.

## Review Purpose

Ensure each spec document meets quality standards before implementation planning. The reviewer validates completeness, consistency, and adherence to design principles.

## When to Dispatch

After writing spec document to `design/specs/` directory.

---

## Review Checklist

### 1. Completeness

- [ ] No TODO markers or placeholder text
- [ ] No "TBD" or "to be defined later" sections
- [ ] No "will spec when X is done" statements
- [ ] All sections have appropriate level of detail
- [ ] No sections noticeably less detailed than others

### 2. Coverage

- [ ] Error handling is addressed
- [ ] Edge cases are considered
- [ ] Integration points are defined
- [ ] Data flow is documented
- [ ] Security considerations (if applicable)

### 3. Consistency

- [ ] No internal contradictions
- [ ] No conflicting requirements
- [ ] Terminology is used consistently
- [ ] References to external systems are clear

### 4. Clarity

- [ ] No ambiguous requirements
- [ ] Technical terms are defined or self-explanatory
- [ ] Requirements are testable/verifiable
- [ ] Acceptance criteria are clear

### 5. YAGNI (You Aren't Gonna Need It)

- [ ] No unrequested features
- [ ] No over-engineering
- [ ] No speculative future-proofing
- [ ] Scope is focused on stated requirements

### 6. Scope Validation

- [ ] Focused enough for a single implementation plan
- [ ] Not covering multiple independent subsystems
- [ ] If multiple subsystems, recommendation to split was made
- [ ] Each subsystem can produce runnable, testable files

### 7. Architecture Quality

- [ ] Units have clear boundaries
- [ ] Interfaces are well-defined
- [ ] Each unit is independently understandable
- [ ] Each unit is independently testable
- [ ] Can understand what each unit does without reading internals
- [ ] Internal implementation can change without affecting users

---

## Critical Issues to Watch For

### Placeholder Content

❌ Bad:
```
## Error Handling
TODO: Define error handling strategy
```

✅ Good:
```
## Error Handling
- Network errors: Retry with exponential backoff (max 3 retries)
- Validation errors: Return 400 with detailed error messages
- Authentication errors: Return 401 and redirect to login
```

### Vague Requirements

❌ Bad:
```
The system should be fast and secure.
```

✅ Good:
```
The system should respond to API requests within 200ms (p95).
All API endpoints require authentication via JWT tokens.
```

### Missing Boundaries

❌ Bad:
```
The UserService handles user registration, authentication,
profile management, notifications, and analytics.
```

✅ Good:
```
The UserService handles user registration and authentication.
- ProfileService: handles profile management
- NotificationService: handles notifications
- AnalyticsService: handles analytics
```

### Over-Engineering

❌ Bad:
```
We'll implement a plugin system to allow future extensions
for features we might need in 2-3 years.
```

✅ Good:
```
We'll implement the specific features requested.
Extension points can be added when actual requirements emerge.
```

---

## Review Output Format

After reviewing, provide output in this format:

```markdown
## Spec Review

**Status:** ✅ Approved | ❌ Issues Found

**Issues Found (if any):**
1. [Section name]: [specific issue]
   - Why it matters: [explanation]
   - Recommendation: [how to fix]

**Strengths:**
- [What was done well]

**Recommendations (advisory):**
- [Suggestions that don't block approval]
```

---

## Review Guidelines

1. **Be thorough but fair** - Focus on issues that would block implementation
2. **Explain the why** - When flagging issues, explain why it matters
3. **Be constructive** - Provide specific recommendations
4. **Consider context** - The spec is for engineers who will create implementation plans
5. **Value clarity** - Ambiguous specs lead to failed implementations
6. **Enforce boundaries** - Unclear boundaries lead to tangled code

---

## Escalation

If review loop exceeds 5 iterations for the same spec:

1. Summarize all issues found across iterations
2. Document attempts made to resolve
3. Identify specific areas of disagreement
4. Submit to human for guidance with full context

---

## Example Review

### Input Spec

```markdown
# User Authentication Design

## Overview
Add user authentication to the application.

## Requirements
- Users can log in
- Users can log out
- Sessions are secure

## Architecture
The AuthService will handle everything related to auth.
```

### Review Output

```markdown
## Spec Review

**Status:** ❌ Issues Found

**Issues Found:**
1. **Overview**: Too vague - missing context about current system state
   - Why it matters: Implementation approach depends on existing architecture
   - Recommendation: Add section describing current authentication state (none? legacy system?)

2. **Requirements**: Missing critical details
   - Why it matters: "Log in" could mean many things - password, SSO, OAuth?
   - Recommendation: Specify authentication methods (password + email, OAuth providers, etc.)

3. **Requirements**: "Sessions are secure" is not testable
   - Why it matters: Cannot verify if requirement is met
   - Recommendation: Define specific security measures (HTTPS, token expiration, CSRF protection)

4. **Architecture**: AuthService has unclear boundaries
   - Why it matters: "Everything related to auth" is too broad
   - Recommendation: Split into focused services (TokenService, SessionService, PasswordService)

**Strengths:**
- Clear goal stated in overview

**Recommendations (advisory):**
- Consider adding error handling section
- Consider adding testing strategy section
```
