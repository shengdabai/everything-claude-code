---
description: "Safely identify and remove dead code using knip, depcheck, and ts-prune, with test verification between each deletion and a categorized SAFE/CAUTION/DANGER severity report."
argument-hint: "[optional: directory or analysis tool name]"
---

# Refactor Clean

If $ARGUMENTS is empty, run all three analyzers (knip, depcheck, ts-prune) on the entire repo. If $ARGUMENTS is a path, scope the scan to that directory. If $ARGUMENTS is a tool name (knip/depcheck/ts-prune), run only that tool.

Safely identify and remove dead code with test verification:

1. Run dead code analysis tools:
   - knip: Find unused exports and files
   - depcheck: Find unused dependencies
   - ts-prune: Find unused TypeScript exports

2. Generate comprehensive report in .reports/dead-code-analysis.md

3. Categorize findings by severity:
   - SAFE: Test files, unused utilities
   - CAUTION: API routes, components
   - DANGER: Config files, main entry points

4. Propose safe deletions only

5. Before each deletion:
   - Run full test suite
   - Verify tests pass
   - Apply change
   - Re-run tests
   - Rollback if tests fail

6. Show summary of cleaned items

Never delete code without running tests first!

## Output format

```
REFACTOR-CLEAN REPORT
=====================
SAFE deletions:    X
CAUTION items:     Y  [requires manual review]
DANGER items:      Z  [skipped]
Deleted:           A items
Rolled back:       B items
Tests:             [PASS / FAIL] after each batch

Report file: .reports/dead-code-analysis.md
```

## Error handling

- If any analyzer (`knip`, `depcheck`, `ts-prune`) is not installed, list install commands and skip that analyzer.
- If a test run fails after a deletion, roll back that deletion via git and mark the item as DANGER.
- If `.reports/` directory does not exist, create it.
- Stop after 3 consecutive rollbacks and report which items were unsafe.
