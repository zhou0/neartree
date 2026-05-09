```markdown
# neartree Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches the core development patterns and conventions used in the `neartree` TypeScript codebase. You'll learn about file organization, import/export styles, commit message conventions, and how to write and run tests. This guide is ideal for contributors aiming to maintain consistency and quality in the project.

## Coding Conventions

### File Naming
- Use **snake_case** for all file names.
  - Example:  
    ```
    nearest_neighbor.ts
    distance_calculator.ts
    ```

### Import Style
- Use **relative imports** for referencing other modules within the project.
  - Example:
    ```typescript
    import { calculateDistance } from './distance_calculator';
    ```

### Export Style
- Use **named exports** instead of default exports.
  - Example:
    ```typescript
    // In distance_calculator.ts
    export function calculateDistance(a: Point, b: Point): number { ... }
    ```

### Commit Messages
- Follow the **Conventional Commits** specification.
- Use the `feat` prefix for new features.
- Keep commit messages concise (average ~37 characters).
  - Example:
    ```
    feat: add nearest neighbor search algorithm
    ```

## Workflows

### Adding a New Feature
**Trigger:** When implementing a new feature or module  
**Command:** `/add-feature`

1. Create a new file using snake_case naming.
2. Implement the feature using TypeScript.
3. Use relative imports for dependencies.
4. Export functions or classes using named exports.
5. Write corresponding test files (see Testing Patterns).
6. Commit your changes with a `feat:` prefix and a concise message.

### Writing Tests
**Trigger:** When adding or updating functionality  
**Command:** `/write-test`

1. Create a test file with the pattern `*.test.*` (e.g., `nearest_neighbor.test.ts`).
2. Write tests for all exported functions and classes.
3. Use the project's preferred (unknown) testing framework.
4. Run tests to ensure correctness.

### Making a Commit
**Trigger:** When saving progress or submitting a pull request  
**Command:** `/commit`

1. Stage your changes.
2. Write a commit message following the conventional format (e.g., `feat: ...`).
3. Keep the message concise and descriptive.

## Testing Patterns

- Test files follow the pattern: `*.test.*` (e.g., `distance_calculator.test.ts`).
- Each exported function or class should have corresponding tests.
- The specific testing framework is not detected, but tests should be written in TypeScript and placed alongside or near the modules they test.
- Example test file:
  ```typescript
  // distance_calculator.test.ts
  import { calculateDistance } from './distance_calculator';

  describe('calculateDistance', () => {
    it('returns 0 for identical points', () => {
      expect(calculateDistance([0, 0], [0, 0])).toBe(0);
    });
  });
  ```

## Commands
| Command        | Purpose                                      |
|----------------|----------------------------------------------|
| /add-feature   | Start the workflow for adding a new feature  |
| /write-test    | Begin writing tests for a module or feature  |
| /commit        | Make a commit following project conventions  |
```
