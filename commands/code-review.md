---
description: "Comprehensive security and quality review of uncommitted changes, organized by severity (CRITICAL/HIGH/MEDIUM/LOW), with explicit block-on-critical policy."
argument-hint: "[optional: file path or git ref to limit scope]"
---

# Code Review

If $ARGUMENTS is empty, review all uncommitted changes (`git diff HEAD`). If $ARGUMENTS is a path or git ref, scope the review to those files only.

Comprehensive security and quality review of uncommitted changes:

1. Get changed files: git diff --name-only HEAD

2. For each changed file, check for:

**Security Issues (CRITICAL):**
- Hardcoded credentials, API keys, tokens
- SQL injection vulnerabilities
- XSS vulnerabilities  
- Missing input validation
- Insecure dependencies
- Path traversal risks

**Code Quality (HIGH):**
- Functions > 50 lines
- Files > 800 lines
- Nesting depth > 4 levels
- Missing error handling
- console.log statements
- TODO/FIXME comments
- Missing JSDoc for public APIs

**Best Practices (MEDIUM):**
- Mutation patterns (use immutable instead)
- Emoji usage in code/comments
- Missing tests for new code
- Accessibility issues (a11y)

3. Generate report with:
   - Severity: CRITICAL, HIGH, MEDIUM, LOW
   - File location and line numbers
   - Issue description
   - Suggested fix

4. Block commit if CRITICAL or HIGH issues found

Never approve code with security vulnerabilities!

## Output format

```
CODE REVIEW REPORT
==================
Files reviewed:  X
CRITICAL:        N issues  [BLOCKS COMMIT]
HIGH:            N issues  [BLOCKS COMMIT]
MEDIUM:          N issues
LOW:             N issues
Verdict:         [APPROVE / WARNING / BLOCK]

Findings (sorted by severity):
  [CRITICAL] file.ts:42 — <issue> → <suggested fix>
  [HIGH]     file.ts:88 — <issue> → <suggested fix>
  ...
```

## Error handling

- If `git diff` returns nothing, report "No uncommitted changes to review" and exit cleanly.
- If the repository is not a git checkout, report that and ask the user for a path scope.
- If a file referenced by the diff has been deleted on disk, skip it and note "file deleted" in the report.
