# Comment Quality Checklist

This document provides a quality verification checklist for after adding comments, used to ensure comments meet specification requirements.

## Table of Contents

- [Comment Completeness Check](#comment-completeness-check)
- [Comment Content Check](#comment-content-check)
- [Comment Format Check](#comment-format-check)
- [Code Completeness Check](#code-completeness-check)

---

## Comment Completeness Check

Check if all required code elements have comments added:

### Functions/Methods

- [ ] All public functions have multi-line comments
- [ ] All private functions have comments (if complex)
- [ ] Async functions are clearly marked

### Classes/Structs

- [ ] All public classes have multi-line comments
- [ ] Abstract classes are clearly marked
- [ ] Generic type parameters have descriptions

### Properties/Fields

- [ ] All public properties have comments
- [ ] Static properties have descriptions
- [ ] Constants have purpose descriptions

### Enums

- [ ] The enum itself has comments
- [ ] All enum members have comments
- [ ] Each member's value meaning is clear

### Type Definitions

- [ ] Interfaces/types have comments
- [ ] All properties have descriptions
- [ ] Generic parameters have descriptions

---

## Comment Content Check

### Function Description

- [ ] Function description is clear and accurate
- [ ] Does not repeat information already expressed in code
- [ ] Describes "what it does" not "how it does it"

### Parameter Description

- [ ] Each parameter has a description
- [ ] Parameter types are correctly annotated
- [ ] Union type parameters have detailed descriptions for each type
- [ ] Optional parameters are clearly marked
- [ ] Parameter constraints are described

### Return Value Description

- [ ] Return value type is correct
- [ ] Return value meaning is clear
- [ ] Special cases (null, undefined) are described

### Exception Description

- [ ] All possible exceptions are described
- [ ] Exception occurrence conditions are clear
- [ ] Exception handling suggestions (if any)

### Usage Examples

- [ ] Contains at least one basic usage example
- [ ] Example code is runnable
- [ ] Complex functions have multiple examples
- [ ] Example comments use target language

---

## Comment Format Check

### Language-specific Format

- [ ] Conforms to language-specific comment style (JSDoc, Rustdoc, etc.)
- [ ] Tags are used correctly (@param, @returns, etc.)
- [ ] Tag order is reasonable

### Bilingual Format

- [ ] All comments are bilingual (English and Chinese)
- [ ] English description comes first, Chinese follows
- [ ] Blank line separates English and Chinese
- [ ] Parameter descriptions use slashes (`/`) to separate

### Line Wrapping Format

- [ ] Comment text wraps at approximately 100 characters
- [ ] List item indentation is consistent
- [ ] Code block indentation is correct

### Punctuation

- [ ] Chinese content uses Chinese punctuation
- [ ] English content uses English punctuation
- [ ] Quotes are used correctly
- [ ] No extra spaces

---

## Code Completeness Check

**This is the most critical check item**, ensuring no code was accidentally modified during comment addition:

### Code Logic

- [ ] No code logic was modified
- [ ] No new code logic was added
- [ ] No code logic was deleted

### Identifiers

- [ ] No variable names were modified
- [ ] No function names were modified
- [ ] No class names were modified
- [ ] No property names were modified

### Code Structure

- [ ] No new code lines were added
- [ ] No code lines were deleted
- [ ] No code lines were reordered
- [ ] No code order was modified

### Code Formatting

- [ ] No indentation was modified
- [ ] No line breaks were modified
- [ ] No spaces were modified
- [ ] Original code formatting is completely preserved

---

## Special Scenario Checks

### Complex Conditional Branches

If single-line comments were added for complex conditions:

- [ ] Comments clearly explain conditional logic
- [ ] Comments explain why this condition is needed

### Complex Loops

If single-line comments were added for complex loops:

- [ ] Comments clearly explain loop purpose
- [ ] Comments explain boundary conditions

### Complex Expressions

If single-line comments were added for complex expressions:

- [ ] Comments clearly explain expression meaning
- [ ] Comments explain calculation logic

---

## Verification Flow

### 1. Completeness Verification

Check the above completeness checklist item by item.

### 2. Content Review

Quickly scan comment content to ensure:

- Function descriptions are accurate
- Parameter descriptions are complete
- Example code is runnable

### 3. Format Verification

Check if all comments conform to format requirements:

- Bilingual format
- Line wrapping rules
- Punctuation

### 4. Code Comparison

Compare the modified file with the original file to ensure:

- Only comments were added or modified
- All code logic is exactly the same

### 5. Test Verification (if possible)

If the project has tests, run tests to ensure code functionality is unaffected.

---

## Common Problems

### Problem: Comments inconsistent with code

**Cause**: Code was modified after adding comments
**Solution**: Revert code modifications, keep only comments

### Problem: Too many unnecessary comments

**Cause**: Comments were added for simple code
**Solution**: Delete obviously redundant comments

### Problem: Bilingual format inconsistent

**Cause**: Some comments missed Chinese or English
**Solution**: Complete all bilingual comments

### Problem: Example code cannot run

**Cause**: Example doesn't match actual function signature
**Solution**: Fix example code or function signature
