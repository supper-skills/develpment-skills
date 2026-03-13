# Implementation Plan Template

This template shows the standard structure for implementation plans. Adapt all file extensions, code examples, and test commands to your project's programming language.

---

# [Feature Name] Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---

## File Structure

### New Files
- `path/to/new/file.<ext>` - Description of responsibility
- `path/to/another/file.<ext>` - Description of responsibility

### Modified Files
- `path/to/existing/file.<ext>` - What will be modified
- `path/to/another/existing.<ext>` - What will be modified

### Test Files
- `tests/path/to/test_file.<ext>` - Test responsibilities

---

## Chunk 1: [Component Name]

### Task 1: [Component Name]

**Files:**
- Create: `exact/path/to/file.<ext>`
- Modify: `exact/path/to/existing.<ext>:123-145`
- Test: `tests/exact/path/to/test.<ext>`

- [ ] **Step 1: Write the failing test**

```<language>
// Adapt to your language
// Example: TypeScript with Jest
describe('functionName', () => {
  it('should return expected result for given input', () => {
    const result = functionName(input);
    expect(result).toBe(expected);
  });
});
```

- [ ] **Step 2: Run test to verify it fails**

Run: `<test-command>` (e.g., `npm test`, `pytest`, `cargo test`)
Expected: FAIL with appropriate error message

- [ ] **Step 3: Write minimal implementation**

```<language>
// Minimal implementation to pass the test
// Adapt to your language
export function functionName(input: InputType): OutputType {
  return expected;
}
```

- [ ] **Step 4: Run test to verify it passes**

Run: `<test-command>`
Expected: PASS

---

### Task 2: [Another Component]

**Files:**
- Create: `exact/path/to/another.<ext>`
- Test: `tests/exact/path/to/test_another.<ext>`

- [ ] **Step 1: Write the failing test**

```<language>
// Adapt to your language
```

- [ ] **Step 2: Run test to verify it fails**

Run: `<test-command>`
Expected: FAIL

- [ ] **Step 3: Write minimal implementation**

```<language>
// Adapt to your language
```

- [ ] **Step 4: Run test to verify it passes**

Run: `<test-command>`
Expected: PASS

---

## Chunk 2: [Integration/Next Component]

[Continue with more tasks following the same pattern...]

---

## Language-Specific Examples

### TypeScript/JavaScript (Jest)

```typescript
describe('UserService', () => {
  it('should create a new user', () => {
    const user = UserService.create({ name: 'John' });
    expect(user.name).toBe('John');
  });
});
```

Run: `npm test` or `jest tests/path/test.ts`

### Python (pytest)

```python
def test_create_user():
    user = UserService.create(name='John')
    assert user.name == 'John'
```

Run: `pytest tests/path/test.py::test_create_user -v`

### Rust

```rust
#[test]
fn test_create_user() {
    let user = UserService::create("John");
    assert_eq!(user.name, "John");
}
```

Run: `cargo test test_create_user`

### Go

```go
func TestCreateUser(t *testing.T) {
    user := UserService.Create("John")
    if user.Name != "John" {
        t.Errorf("expected John, got %s", user.Name)
    }
}
```

Run: `go test ./path/to/package -run TestCreateUser`

---

## Notes

- Each chunk should be ≤1000 lines
- Each task follows TDD: test → fail → implement → pass
- Commit after each passing test
- Adapt all examples to your project's programming language
