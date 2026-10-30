---
description: "Analyze codebase structure and regenerate token-lean codemaps under codemaps/ (architecture, backend, frontend, data), with diff gate at 30% requiring user approval."
argument-hint: "[optional: codemap area name — architecture | backend | frontend | data]"
---

# Update Codemaps

If $ARGUMENTS is empty, regenerate all four codemaps. If $ARGUMENTS is an area name, regenerate only that one.

Analyze the codebase structure and update architecture documentation:

1. Scan all source files for imports, exports, and dependencies
2. Generate token-lean codemaps in the following format:
   - codemaps/architecture.md - Overall architecture
   - codemaps/backend.md - Backend structure  
   - codemaps/frontend.md - Frontend structure
   - codemaps/data.md - Data models and schemas

3. Calculate diff percentage from previous version
4. If changes > 30%, request user approval before updating
5. Add freshness timestamp to each codemap
6. Save reports to .reports/codemap-diff.txt

Use TypeScript/Node.js for analysis. Focus on high-level structure, not implementation details.

## Output format

```
CODEMAP UPDATE
==============
Codemaps regenerated: N
Diff vs previous:     X% (threshold: 30%)
User approval:        [NOT REQUIRED / REQUESTED / GRANTED / DENIED]
Files written:        codemaps/architecture.md, codemaps/backend.md, ...
Diff report:          .reports/codemap-diff.txt
```

## Error handling

- If `tsconfig.json` is missing, fall back to plain file-tree scan and note the limitation.
- If diff exceeds 30% and the user denies the update, write the diff to `.reports/codemap-diff.txt` and exit without modifying codemaps.
- If `codemaps/` directory does not exist, create it.
