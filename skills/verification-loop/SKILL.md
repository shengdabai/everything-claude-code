---
name: verification-loop
description: Run the build/type/lint/test/security/diff gate after any feature change, refactor, or before opening a PR. Use when the user says "verify", "run the verification loop", "check before PR", "make sure it's green", "run quality gates", or when a change needs systematic sign-off across all 6 phases. Trigger phrases include "verification loop", "pre-PR check", "quality gates", "ready for PR".
---

# Verification Loop Skill

A comprehensive verification system for Claude Code sessions.

## Examples

<example>
Context: User just finished implementing a new API endpoint.
user: "Run the verification loop before I open a PR."
assistant: "Executing the 6-phase loop in order: build → type check → lint → tests with coverage → secret/console.log scan → diff review. I'll report PASS/FAIL per phase and produce the consolidated verification report at the end."
</example>

<example>
Context: Long refactor session, user wants a mid-session checkpoint.
user: "Quick gate check — am I still green?"
assistant: "Running the verification loop in continuous mode: build + type + lint + test pass count + diff stat. Skipping the full security scan since this is mid-session, not pre-PR. Reporting in 30 seconds."
</example>

## When to Use

Invoke this skill:
- After completing a feature or significant code change
- Before creating a PR
- When you want to ensure quality gates pass
- After refactoring

## Verification Phases

### Phase 1: Build Verification
```bash
# Check if project builds
npm run build 2>&1 | tail -20
# OR
pnpm build 2>&1 | tail -20
```

If build fails, STOP and fix before continuing.

### Phase 2: Type Check
```bash
# TypeScript projects
npx tsc --noEmit 2>&1 | head -30

# Python projects
pyright . 2>&1 | head -30
```

Report all type errors. Fix critical ones before continuing.

### Phase 3: Lint Check
```bash
# JavaScript/TypeScript
npm run lint 2>&1 | head -30

# Python
ruff check . 2>&1 | head -30
```

### Phase 4: Test Suite
```bash
# Run tests with coverage
npm run test -- --coverage 2>&1 | tail -50

# Check coverage threshold
# Target: 80% minimum
```

Report:
- Total tests: X
- Passed: X
- Failed: X
- Coverage: X%

### Phase 5: Security Scan
```bash
# Check for secrets
grep -rn "sk-" --include="*.ts" --include="*.js" . 2>/dev/null | head -10
grep -rn "api_key" --include="*.ts" --include="*.js" . 2>/dev/null | head -10

# Check for console.log
grep -rn "console.log" --include="*.ts" --include="*.tsx" src/ 2>/dev/null | head -10
```

### Phase 6: Diff Review
```bash
# Show what changed
git diff --stat
git diff HEAD~1 --name-only
```

Review each changed file for:
- Unintended changes
- Missing error handling
- Potential edge cases

## Output Format

After running all phases, produce a verification report:

```
VERIFICATION REPORT
==================

Build:     [PASS/FAIL]
Types:     [PASS/FAIL] (X errors)
Lint:      [PASS/FAIL] (X warnings)
Tests:     [PASS/FAIL] (X/Y passed, Z% coverage)
Security:  [PASS/FAIL] (X issues)
Diff:      [X files changed]

Overall:   [READY/NOT READY] for PR

Issues to Fix:
1. ...
2. ...
```

## Continuous Mode

For long sessions, run verification every 15 minutes or after major changes:

```markdown
Set a mental checkpoint:
- After completing each function
- After finishing a component
- Before moving to next task

Run: /verify
```

## Integration with Hooks

This skill complements PostToolUse hooks but provides deeper verification.
Hooks catch issues immediately; this skill provides comprehensive review.
