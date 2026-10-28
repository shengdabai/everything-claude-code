---
description: "Incrementally fix TypeScript and build errors one at a time, with stop conditions on repeated failures or new errors introduced."
argument-hint: "[optional: file path or error filter]"
---

# Build and Fix

If $ARGUMENTS is empty, run the full project build. If $ARGUMENTS contains a path, scope the build/check to that file or directory first.

Incrementally fix TypeScript and build errors:

1. Run build: npm run build or pnpm build

2. Parse error output:
   - Group by file
   - Sort by severity

3. For each error:
   - Show error context (5 lines before/after)
   - Explain the issue
   - Propose fix
   - Apply fix
   - Re-run build
   - Verify error resolved

4. Stop if:
   - Fix introduces new errors
   - Same error persists after 3 attempts
   - User requests pause

5. Show summary:
   - Errors fixed
   - Errors remaining
   - New errors introduced

Fix one error at a time for safety!

## Output format

```
BUILD-FIX REPORT
================
Initial errors:    X
Errors fixed:      Y
Errors remaining:  Z
New errors:        N
Status:            [PASSING / IN PROGRESS / BLOCKED]

Per-error log:
  1. file:line  - <one-line description>  [FIXED / SKIPPED / RETRY]
  2. ...
```

## Error handling

- If the build command itself fails to launch (missing `npm`/`tsc`), report the missing tool and stop.
- If the same error persists after 3 fix attempts, mark it BLOCKED, move on to the next error, and surface it in the final report.
- If a fix introduces 2+ new errors, revert that fix and mark the original BLOCKED.
- If no build script exists in `package.json`, ask the user to specify the build command before proceeding.
