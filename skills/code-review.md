Review the selected code (or recent changes) for simplicity, clarity, and correctness.
Inspired by Rob Pike's philosophy: "Simplicity is the key to good software."

## Usage
```
/code-review [file-or-path]
```
Examples: `/code-review src/auth.ts`, `/code-review` (reviews staged changes)

## Steps

1. Determine the review target:
   - If a file/path is given, read that file.
   - If no argument, run `git diff --cached` (staged changes). If nothing staged, use `git diff` (unstaged).
   - If the user has selected code in the IDE, review that selection.

2. Analyze the code on these axes:
   - **Simplicity** — Can anything be removed or simplified without losing functionality?
   - **Clarity** — Is the intent obvious? Are names descriptive?
   - **Correctness** — Any bugs, edge cases, or off-by-one errors?
   - **Security** — Any injection, XSS, or credential exposure risks?

3. Output a structured review:
```
## Code Review

### Summary
One-line overall assessment.

### Issues
- [severity] file:line — description and suggested fix

### Suggestions
- Improvement ideas that aren't bugs but would help

### Verdict
LGTM / Needs changes (with priority items)
```

## Notes

- Keep feedback actionable — every issue should have a concrete suggestion
- Don't nitpick style if a linter/formatter handles it
- Focus on logic and architecture, not cosmetics
