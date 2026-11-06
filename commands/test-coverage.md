---
description: "Analyze test coverage from coverage-summary.json, identify files under the 80% threshold, then generate unit/integration/E2E tests for uncovered paths and re-verify."
argument-hint: "[optional: file or directory to focus coverage analysis on]"
---

# Test Coverage

If $ARGUMENTS is empty, analyze the full project coverage report. If $ARGUMENTS is a path, focus generation on uncovered code within that path.

Analyze test coverage and generate missing tests:

1. Run tests with coverage: npm test --coverage or pnpm test --coverage

2. Analyze coverage report (coverage/coverage-summary.json)

3. Identify files below 80% coverage threshold

4. For each under-covered file:
   - Analyze untested code paths
   - Generate unit tests for functions
   - Generate integration tests for APIs
   - Generate E2E tests for critical flows

5. Verify new tests pass

6. Show before/after coverage metrics

7. Ensure project reaches 80%+ overall coverage

Focus on:
- Happy path scenarios
- Error handling
- Edge cases (null, undefined, empty)
- Boundary conditions

## Output format

```
COVERAGE REPORT
===============
Before:  L% lines / F% functions / B% branches
After:   L% lines / F% functions / B% branches
Files under 80%: N
Tests generated: M
Test run:        [PASS / FAIL]
Target met:      [YES / NO]
```

## Error handling

- If `coverage/coverage-summary.json` does not exist, run the test command with `--coverage` first.
- If no test runner is detected (no `test` script in `package.json`), report this and ask the user.
- If a generated test fails on first run, mark it `// TODO: review` and continue rather than blocking.
