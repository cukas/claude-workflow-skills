---
name: bugfix
description: Test-driven bug fix loop. Write a failing test first, then iterate fix > test > fix until all tests pass. Use when reporting a bug to fix.
---

# Test-Driven Bug Fix

The user will describe a bug. Follow this loop autonomously:

1. **Write a failing test** that reproduces the exact bug behavior
2. **Run the test** to confirm it fails
3. **Implement the minimal fix** — smallest change that makes the test pass
4. **Run the full test suite**
5. **If any test fails**, analyze the failure, adjust the fix, and go back to step 4
6. **Repeat until all tests pass**

## Rules
- Do not ask clarifying questions — make reasonable assumptions and document them
- Do not show intermediate results — only present the final diff and test results when everything is green
- After all tests pass, run the project's type checker to verify types
- **MANDATORY: Invoke the `review-checklist` skill before declaring done.** Do not skip this step.
