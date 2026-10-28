---
description: "Create, verify, list, or clear named workflow checkpoints backed by git refs and logged to .claude/checkpoints.log. Used to compare test pass rate, coverage, and build status between marked points in a session."
argument-hint: "create <name> | verify <name> | list | clear"
---

# Checkpoint Command

If $ARGUMENTS is empty, default to `list` so the user sees existing checkpoints before deciding the next action.

Create or verify a checkpoint in your workflow.

## Usage

`/checkpoint [create|verify|list] [name]`

## Create Checkpoint

When creating a checkpoint:

1. Run `/verify quick` to ensure current state is clean
2. Create a git stash or commit with checkpoint name
3. Log checkpoint to `.claude/checkpoints.log`:

```bash
echo "$(date +%Y-%m-%d-%H:%M) | $CHECKPOINT_NAME | $(git rev-parse --short HEAD)" >> .claude/checkpoints.log
```

4. Report checkpoint created

## Verify Checkpoint

When verifying against a checkpoint:

1. Read checkpoint from log
2. Compare current state to checkpoint:
   - Files added since checkpoint
   - Files modified since checkpoint
   - Test pass rate now vs then
   - Coverage now vs then

3. Report:
```
CHECKPOINT COMPARISON: $NAME
============================
Files changed: X
Tests: +Y passed / -Z failed
Coverage: +X% / -Y%
Build: [PASS/FAIL]
```

## List Checkpoints

Show all checkpoints with:
- Name
- Timestamp
- Git SHA
- Status (current, behind, ahead)

## Workflow

Typical checkpoint flow:

```
[Start] --> /checkpoint create "feature-start"
   |
[Implement] --> /checkpoint create "core-done"
   |
[Test] --> /checkpoint verify "core-done"
   |
[Refactor] --> /checkpoint create "refactor-done"
   |
[PR] --> /checkpoint verify "feature-start"
```

## Arguments

$ARGUMENTS:
- `create <name>` - Create named checkpoint
- `verify <name>` - Verify against named checkpoint
- `list` - Show all checkpoints
- `clear` - Remove old checkpoints (keeps last 5)

## Output format

```
CHECKPOINT: <subcommand> <name>
===============================
Status:    [CREATED / VERIFIED / LISTED / CLEARED]
Git SHA:   <short-sha>
Timestamp: YYYY-MM-DD HH:MM
Delta vs <name>:
  Files changed:  +X / -Y
  Tests:          +A passed / -B failed
  Coverage:       +C% / -D%
  Build:          [PASS / FAIL]
```

## Error handling

- If the named checkpoint does not exist for `verify`, list available checkpoints and exit.
- If the working tree is dirty during `create`, refuse to checkpoint and ask the user to commit or stash first.
- If `.claude/checkpoints.log` does not exist, create it on first `create`.
