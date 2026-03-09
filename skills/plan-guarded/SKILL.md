---
name: plan-guarded
description: Two-phase workflow with regression guards. Plan first, get approval, then implement one file at a time with type-check and test checkpoints. Use for risky multi-file changes.
---

# Guarded Plan-Then-Execute

The user will describe a task. Follow this strict two-phase workflow:

## PHASE 1 — PLAN (do not write any code yet)

1. Use Read, Grep, and Glob to thoroughly explore every file related to the task
2. Write a numbered plan with:
   - Each file to change and what changes are needed
   - Dependencies between changes (order matters)
   - Potential regression risks for each change
3. Present the plan for user approval before proceeding

## PHASE 2 — IMPLEMENT (only after user approves)

1. Implement changes **one file at a time**
2. After **each** file change, run the project's type checker (e.g., `npx tsc --noEmit`, `pyright`, etc.) — fix type errors before moving on
3. After every **3 files**, run the project's test suite to catch regressions early
4. If any test breaks:
   - **Stop immediately**
   - Analyze whether the approach is wrong (don't just patch symptoms)
   - Explain the root cause before proceeding
5. After all changes, run the full test suite and type check one final time
6. **MANDATORY: Invoke the `review-checklist` skill now.** Do not skip this. Do not summarize results until review-checklist has completed and all findings are resolved.

## Rules
- Never skip the plan phase
- Never batch multiple file changes between verification steps
- If a regression appears, consider whether the overall approach needs adjustment — not just the failing file
- Never declare done without completing the review-checklist skill — this is non-negotiable
