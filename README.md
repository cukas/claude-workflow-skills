# Claude Workflow Skills

Battle-tested development workflow skills for Claude Code. Born from 451 sessions of real-world audio plugin development.

## Skills

### `/plan-guarded`
Two-phase workflow with regression guards. Plan first, get approval, then implement one file at a time with type-check and test checkpoints after each change. Automatically chains into review-checklist when done.

### `/bugfix`
Test-driven bug fix loop. Write a failing test first, then iterate fix > test > fix until all tests pass. No hand-holding — runs autonomously and only surfaces when everything is green.

### `/review-checklist`
Post-implementation review that traces affected code paths, checks for common bug patterns (null safety, async/await, stale data, off-by-one), and verifies builds and tests pass. Auto-triggered by plan-guarded and bugfix, but can also be invoked standalone.

## Install

```bash
claude plugins install --from github:cukas/claude-workflow-skills
```

## Workflow

```
/plan-guarded  →  implement one file at a time  →  /review-checklist (automatic)
/bugfix        →  test-driven fix loop           →  /review-checklist (automatic)
```
