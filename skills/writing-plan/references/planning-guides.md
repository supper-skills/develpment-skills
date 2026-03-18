# Planning Guides

Detailed guides for dependency management, environment configuration, and rollback strategy.

---

## Table of Contents

- [Dependency Management Planning](#dependency-management-planning)
- [Environment Configuration Planning](#environment-configuration-planning)
- [Rollback Strategy Planning](#rollback-strategy-planning)

---

## Dependency Management Planning

Clearly specify dependency management strategy in the plan to ensure smooth implementation.

### Dependency Identification

**Types of dependencies to identify:**

| Dependency Type | Description | Example |
|---------------|-------------|---------|
| Runtime dependency | Packages required for application to run | `express`, `lodash`, `axios` |
| Dev dependency | Packages needed only in development environment | `typescript`, `jest`, `eslint` |
| Peer dependency | Packages that need to be provided by consumer | `react`, `vue` |
| Optional dependency | Non-essential but feature-enhancing packages | Performance analysis tools, debugging tools |

### Dependency Installation Plan

Include the following in the plan:

```markdown
### Pre-requisite Task: Dependency Installation

**New Dependencies:**
- `package-name@version` - Usage description
- `another-package@^1.2.0` - Usage description

**Installation Commands:**
- [ ] Install runtime dependencies
  Run: `pnpm add package-name@version`
  Expected: Dependency added to package.json and installed successfully

- [ ] Install dev dependencies
  Run: `pnpm add -D dev-package@version`
  Expected: Dependency added to devDependencies and installed successfully
```

### Version Management Strategy

**Version locking principles:**

- Use exact versions or locked ranges for production dependencies
- Can use looser ranges (`^` or `~`) for dev dependencies
- Record rationale for selecting specific versions

**Version compatibility check:**

- Check compatibility of new dependencies with existing ones
- Identify potential version conflicts
- Record solutions for resolving conflicts

---

## Environment Configuration Planning

Clearly specify configuration strategies for different environments to ensure code runs correctly in all environments.

### Environment Types

| Environment | Purpose | Configuration Characteristics |
|-----------|---------|---------------------------|
| Development | Local development and debugging | Detailed logs, hot reload, mock data |
| Testing | Automated testing | Isolated data, deterministic configuration |
| Staging | Pre-release verification | Close to production config, real data subset |
| Production | Official operation | Performance optimization, security hardening, minimal logs |

### Configuration File Planning

**Configuration file structure:**

```markdown
### Environment Configuration Files

**Create:**
- `.env.example` - Environment variable template (commit to version control)
- `.env.development` - Development environment config (don't commit)
- `.env.test` - Test environment config (optionally commit)
- `.env.production` - Production environment config (don't commit, inject via CI/CD)

**Configuration items:**
- `DATABASE_URL` - Database connection string
- `API_KEY` - Third-party service key
- `LOG_LEVEL` - Log level
- `FEATURE_FLAGS` - Feature flags
```

### Configuration Task Template

````markdown
### Task: Environment Configuration

**Files:**
- Create: `.env.example`
- Create: `src/config/index.ts`

- [ ] **Step 1: Create environment variable template**

```
# .env.example
DATABASE_URL=postgresql://localhost:5432/dbname
API_KEY=your-api-key-here
LOG_LEVEL=debug
```

- [ ] **Step 2: Create configuration loading module**

```typescript
// src/config/index.ts
export const config = {
  database: {
    url: process.env.DATABASE_URL || 'postgresql://localhost:5432/dev',
  },
  api: {
    key: process.env.API_KEY,
  },
  log: {
    level: process.env.LOG_LEVEL || 'info',
  },
};
```
````

### Sensitive Information Handling

**Security principles:**

- Never commit sensitive information (keys, passwords) to version control
- Use environment variables or secret management services
- Clearly mark which configurations need manual user setup in the plan

---

## Rollback Strategy Planning

Prepare rollback plans for implementation failures or unexpected situations to reduce risk.

### Rollback Scenario Identification

| Scenario | Trigger Condition | Rollback Strategy |
|---------|------------------|-------------------|
| Dependency installation failure | Version conflict, network issue | Restore package.json/lock file |
| Tests continuously failing | Unfixable test errors | Roll back to last passing state |
| Feature incompatible | Integration failure with existing system | Revert related code changes |
| Performance degradation | Performance metrics not meeting targets | Roll back performance-related changes |
| Security issue | Security vulnerability discovered | Immediately roll back and fix |

### Rollback Plan Template

Include rollback chapter in the plan:

````markdown
## Rollback Plan

### Checkpoints

| Checkpoint | Completed Tasks | Rollback Command |
|-----------|----------------|------------------|
| CP-1 | Dependency installation complete | `git checkout package.json pnpm-lock.yaml && pnpm install` |
| CP-2 | Authentication module complete | `git checkout src/auth/ tests/auth/` |
| CP-3 | API integration complete | `git checkout src/api/ tests/api/` |

### Rollback Steps

**If implementation fails and rollback is needed:**

1. **Stop current task**
   - Record failure reason
   - Save current progress

2. **Determine rollback point**
   - Check recent checkpoints
   - Confirm rollback scope

3. **Execute rollback**
   ```bash
   # Roll back to specified checkpoint
   git reset --hard <checkpoint-commit>

   # Or selective rollback of files
   git checkout <commit> -- path/to/files
   ```

4. **Verify rollback**
   - Run tests to ensure system works
   - Check if functionality is restored

5. **Record issue**
   - Record failure reason in design document
   - Update plan to avoid repeated issues
````

### Git Branch Strategy

**Recommended branch model:**

```
main (production)
  └── develop (development)
        └── feature/xxx (feature branch)
```

**Rollback-friendly practices:**

- Create commits after each task completes
- Use descriptive commit messages
- Tag at key checkpoints
- Keep commits atomic (one logical change per commit)
