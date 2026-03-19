# Comment Quality Checklist

This document provides a quality verification checklist after adding comments to ensure comments meet specification requirements.

## Table of Contents

- [Comment Completeness Check](#comment-completeness-check)
- [Comment Content Check](#comment-content-check)
- [Comment Format Check](#comment-format-check)
- [Code Integrity Check](#code-integrity-check)

---

## Comment Completeness Check

Check if all required code elements have comments added:

### Functions/Methods

- [ ] All public functions have multi-line comments
- [ ] All private functions have comments (if complex)
- [ ] Async functions clearly marked

### Classes/Structs

- [ ] All public classes have multi-line comments
- [ ] Abstract classes clearly marked
- [ ] Generic type parameters explained

### Properties/Fields

- [ ] All public properties have comments
- [ ] Static properties explained
- [ ] Constants have purpose explanation

### Enums

- [ ] Enum itself has comments
- [ ] All enum members have comments
- [ ] Each member's value meaning is clear

### Type Definitions

- [ ] Interfaces/types have comments
- [ ] All properties explained
- [ ] Generic parameters explained

---

## Comment Content Check

### Function Description

- [ ] Function description is clear and accurate
- [ ] Does not repeat information already expressed by code
- [ ] Describes "what it does" not "how it does it"

### Parameter Description

- [ ] Each parameter has explanation
- [ ] Parameter types correctly annotated
- [ ] Union type parameters have detailed explanation for each type
- [ ] Optional parameters clearly marked
- [ ] Parameter constraints explained

### Return Value Description

- [ ] Return value type is correct
- [ ] Return value meaning is clear
- [ ] Special cases (null, undefined) explained

### Exception Description

- [ ] All possible exceptions explained
- [ ] Exception conditions clear
- [ ] Exception handling suggestions (if any)

### Usage Examples

- [ ] At least one basic usage example included
- [ ] Example code is runnable
- [ ] Complex functions have multiple examples
- [ ] Examples use target language

---

## Comment Format Check

### Language-specific Format

- [ ] Conforms to language-specific comment style (JSDoc, Rustdoc, etc.)
- [ ] Tags used correctly (@param, @returns, etc.)
- [ ] Tag order is reasonable

### Bilingual Format

- [ ] All comments are bilingual (English and Chinese)
- [ ] English description first, Chinese description after
- [ ] Empty line between English and Chinese
- [ ] Parameter descriptions use slash separation (`/`)

### Line Wrapping Format

- [ ] Comment text wraps at around 100 characters
- [ ] List item indentation consistent
- [ ] Code block indentation correct

### Punctuation

- [ ] Chinese content uses Chinese punctuation
- [ ] English content uses English punctuation
- [ ] Quotation marks used correctly
- [ ] No extra spaces

---

## Code Integrity Check

**This is the most critical check item**, ensuring no accidental code modifications during comment addition:

### Code Logic

- [ ] No code logic modified
- [ ] No new code logic added
- [ ] No code logic deleted

### Identifiers

- [ ] No variable names modified
- [ ] No function names modified
- [ ] No class names modified
- [ ] No property names modified

### Code Structure

- [ ] No new code lines added
- [ ] No code lines deleted
- [ ] No code lines rearranged
- [ ] No code order modified

### Code Format

- [ ] No indentation modified
- [ ] No line breaks modified
- [ ] No spaces modified
- [ ] Original code format completely preserved

---

## Special Scenario Checks

### Complex Conditional Branches

If single-line comments were added for complex conditions:

- [ ] Comment clearly explains conditional logic
- [ ] Comment explains why this condition is needed

### Complex Loops

If single-line comments were added for complex loops:

- [ ] Comment clearly explains loop purpose
- [ ] Comment explains boundary conditions

### Complex Expressions

If single-line comments were added for complex expressions:

- [ ] Comment clearly explains expression meaning
- [ ] Comment explains calculation logic

---

## Verification Process

### 1. Completeness Verification

Check the completeness checklist above item by item.

### 2. Content Review

Quickly browse comment content to ensure:

- Function descriptions are accurate
- Parameter descriptions are complete
- Example code is runnable

### 3. Format Verification

Check if all comments meet format requirements:

- Bilingual format
- Line wrapping rules
- Punctuation

### 4. Code Comparison

Compare modified file with original file to ensure:

- Only comments were added or modified
- All code logic is exactly the same

### 5. Test Verification (if possible)

If the project has tests, run tests to ensure code functionality is not affected.

---

## Common Issues

### Issue: Comment Inconsistent with Code

**Cause**: Code was modified after comments were added
**Solution**: Revert code changes, keep only comments

### Issue: Too Many Unnecessary Comments

**Cause**: Comments added for simple code
**Solution**: Remove obviously redundant comments

### Issue: Inconsistent Bilingual Format

**Cause**: Some comments missing Chinese or English
**Solution**: Complete all bilingual comments

### Issue: Example Code Not Runnable

**Cause**: Example doesn't match actual function signature
**Solution**: Fix example code or function signature
