---
description: "Sync documentation from source-of-truth files (package.json scripts, .env.example), regenerate docs/CONTRIB.md and docs/RUNBOOK.md, and flag obsolete docs over 90 days old."
argument-hint: "[optional: doc file to regenerate — CONTRIB | RUNBOOK | all]"
---

# Update Documentation

If $ARGUMENTS is empty, regenerate both `CONTRIB.md` and `RUNBOOK.md`. If $ARGUMENTS names one, regenerate only that file.

Sync documentation from source-of-truth:

1. Read package.json scripts section
   - Generate scripts reference table
   - Include descriptions from comments

2. Read .env.example
   - Extract all environment variables
   - Document purpose and format

3. Generate docs/CONTRIB.md with:
   - Development workflow
   - Available scripts
   - Environment setup
   - Testing procedures

4. Generate docs/RUNBOOK.md with:
   - Deployment procedures
   - Monitoring and alerts
   - Common issues and fixes
   - Rollback procedures

5. Identify obsolete documentation:
   - Find docs not modified in 90+ days
   - List for manual review

6. Show diff summary

Single source of truth: package.json and .env.example

## Output format

```
DOCS UPDATE REPORT
==================
Files regenerated:    docs/CONTRIB.md, docs/RUNBOOK.md
Scripts documented:   N
Env vars documented:  M
Obsolete docs (>90d): K  (listed below)
Diff summary:         +A lines / -B lines
```

## Error handling

- If `.env.example` is missing, skip the env vars section and note the omission.
- If `package.json` has no `scripts` block, skip the scripts table and note the omission.
- If `docs/` does not exist, create it before writing.
