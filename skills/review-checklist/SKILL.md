---
name: review-checklist
description: TRIGGER automatically after completing any code implementation, bug fix, or refactor — do NOT wait for the user to invoke this. Post-implementation review checklist that traces affected code paths, checks for common bug patterns, and verifies builds.
---

# Review Checklist

Run this checklist after implementing changes, before declaring done.

## 1. Explore affected code paths
Use a code-explorer agent to trace the full data flow through all affected files. Do not skip this step for changes that touch multiple files or cross process/API boundaries.

## 2. Common bug patterns
Check for these recurring issues:
- **Null safety:** NonNullable casts without guards, optional chaining gaps
- **Missing async/await:** Especially on async operations, IPC calls, API requests
- **Stale data:** Old values in caches, persisted state, or UI that survive restarts
- **Off-by-one errors:** Index validation, array boundary logic
- **Import errors:** Missing imports, circular dependencies, wrong paths

## 3. Build verification
- Run the project's build command and confirm it succeeds
- If the project has separate build targets (e.g., plugin, shared types), rebuild those too

## 4. Type and test verification
- Run the project's type checker (e.g., `npx tsc --noEmit`)
- Run the project's test suite (e.g., `npx vitest run`, `pytest`, `npm test`)
- Fix all failures before reporting completion

## 5. Architectural check
- Does the change follow existing patterns in the codebase?
- Are there simpler approaches already used elsewhere?
- Does it introduce unnecessary abstractions or over-engineering?
