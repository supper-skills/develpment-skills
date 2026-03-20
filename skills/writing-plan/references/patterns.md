# Common Plan Pattern Library

Pre-defined task templates that can be quickly reused for common scenarios.

---

## Usage

When the following common patterns are identified, directly reference the corresponding template.

---

## Pattern 1: CRUD Module

**Applicable Scenario**: Data create, read, update, delete operations

**Typical File Structure**:

| File | Responsibility |
|------|------|
| `src/models/<entity>.ts` | Data model definition |
| `src/repositories/<entity>Repository.ts` | Data access layer |
| `src/services/<entity>Service.ts` | Business logic layer |
| `src/controllers/<entity>Controller.ts` | API controller |
| `tests/<entity>.test.ts` | Test file |

**Typical Task Sequence**:
1. Define data model
2. Implement Repository (CRUD operations)
3. Implement Service (business logic)
4. Implement Controller (API endpoints)
5. Integration tests

---

## Pattern 2: Authentication Module

**Applicable Scenario**: User authentication and authorization

**Typical File Structure**:

| File | Responsibility |
|------|------|
| `src/auth/jwtHandler.ts` | JWT token handling |
| `src/auth/middleware.ts` | Authentication middleware |
| `src/auth/refreshHandler.ts` | Token refresh |
| `src/services/userService.ts` | User service |
| `tests/auth.test.ts` | Authentication tests |

**Typical Task Sequence**:
1. Implement JWT generation and verification
2. Implement authentication middleware
3. Implement login/logout logic
4. Implement token refresh mechanism
5. Permission verification

---

## Pattern 3: API Integration

**Applicable Scenario**: Third-party service integration

**Typical File Structure**:

| File | Responsibility |
|------|------|
| `src/clients/<service>Client.ts` | API client |
| `src/adapters/<service>Adapter.ts` | Data adapter |
| `src/services/<service>Service.ts` | Business encapsulation |
| `src/mocks/<service>Mock.ts` | Mock implementation |
| `tests/<service>.test.ts` | Integration tests |

**Typical Task Sequence**:
1. Define API client interface
2. Implement request/response handling
3. Implement data adapter layer
4. Implement error handling and retry
5. Create mock implementation for testing

---

## Pattern 4: Middleware/Plugin

**Applicable Scenario**: Request processing pipeline, plugin system

**Typical File Structure**:

| File | Responsibility |
|------|------|
| `src/middleware/<name>.ts` | Middleware implementation |
| `src/types/middleware.ts` | Type definitions |
| `tests/middleware/<name>.test.ts` | Test file |

**Typical Task Sequence**:
1. Define middleware interface
2. Implement core logic
3. Implement configuration options
4. Error handling
5. Integration tests

---

## Pattern Reference Method

Reference patterns in plans:

```markdown
### Task Group: User Management CRUD

> Reference Pattern: CRUD Module
> Entity: User

[Write specific tasks based on pattern template...]
```
