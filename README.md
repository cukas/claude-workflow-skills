# Claude Workflow Skills

Guarded development workflows for Claude Code. Investigation before fixes. Orchestration before implementation. Verification before completion.

> **Pure discipline, zero infrastructure.** No databases, no MCP servers, no build tools. Just markdown skills that teach Claude to work methodically — read before edit, test before ship, verify before done. Works standalone. Layers with [patrol](https://github.com/cukas/patrol) and [remembrall](https://github.com/cukas/remembrall) if installed.

## Skills

### `/build-guard`

Orchestrated multi-file implementation with regression checkpoints.

1. **Plan** — enters plan mode (read-only), explores the codebase, writes a numbered plan with risks
2. **Implement** — dispatches subagents for larger changes (one per file or logical chunk), type-checks after every file, runs tests every 3 files
3. **Verify** — auto-invokes `/review-gate` before declaring done

Auto-scales: small changes (1-2 files) run inline, larger changes use subagents to keep context clean. For big plans that consume context, hands off via remembrall and resumes with full budget.

```
/build-guard  →  plan mode  →  approval  →  subagent dispatch  →  checkpoints  →  /review-gate
```

### `/trace-fix`

Investigation-first bug fixing with TDD loop.

1. **Trace** — reads every file in the call chain, documents the root cause before touching code
2. **Fix** — writes a failing test, implements the minimal fix, runs full test suite
3. **Verify** — auto-invokes `/review-gate` when green

Escapes after 5 failed iterations instead of spinning forever. Falls back gracefully when no test framework or type checker exists.

```
/trace-fix  →  trace root cause  →  failing test  →  minimal fix  →  verify  →  /review-gate
```

### `/review-gate`

Structured post-implementation review with pass/fail output.

Traces affected code paths, scans for bug patterns (null safety, async errors, security, stale data), runs build/type/test verification, checks architectural consistency. Outputs a structured report:

```
| Check            | Status | Notes                      |
|------------------|--------|----------------------------|
| Code path trace  | PASS   | 3 callers, 2 dependents    |
| Bug pattern scan | PASS   | No issues found            |
| Build            | PASS   | npm run build              |
| Type check       | PASS   | npx tsc --noEmit           |
| Tests            | PASS   | 47 passed, 0 failed        |
| Architecture     | PASS   | Consistent with src/utils  |
```

Both `/build-guard` and `/trace-fix` auto-invoke this — nothing ships without passing the gate.

## Install

```bash
claude plugin marketplace add cukas/claude-workflow-skills
claude plugin install workflow-skills@cukas
```

## Works With

These skills are **self-contained** — they enforce discipline on their own. But they integrate smoothly with:

- **[patrol](https://github.com/cukas/patrol)** — If installed, build-guard and trace-fix respect patrol's investigation warnings and escalation. If not, the skills enforce the same read-before-edit discipline themselves.
- **[remembrall](https://github.com/cukas/remembrall)** — If installed, build-guard hands off context-heavy sessions automatically for clean context on resume. If not, plans are saved to `docs/plans/` as files.

## License

MIT
