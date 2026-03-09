# Claude Workflow Skills

Guarded development workflows for Claude Code. Investigation before fixes. Orchestration before implementation. Verification before completion.

## Skills

### `/build-guard`
Orchestrated multi-file implementation. Plans in plan mode (read-only), then implements with subagent dispatch for larger changes. Type-check after every file, test gate every 3 files, stop-on-failure analysis. For big plans that consume context, hands off and resumes with full budget.

### `/trace-fix`
Investigation-first bug fixing. Traces the full call chain to root cause before touching code. Then TDD loop: failing test, minimal fix, verify. Escapes after 5 failed iterations instead of spinning forever.

### `/review-gate`
Structured post-implementation review with pass/fail output. Traces code paths, scans for bug patterns, runs build/type/test verification, checks architectural consistency. Both build-guard and trace-fix auto-invoke this — nothing ships without passing the gate.

## Install

```bash
claude plugins install --from github:cukas/claude-workflow-skills
```

## Workflow

```
/build-guard  →  plan mode → subagent dispatch → checkpoints  →  /review-gate (automatic)
/trace-fix    →  trace root cause → TDD loop                  →  /review-gate (automatic)
```

## Works With

- **[patrol](https://github.com/cukas/patrol)** — If installed, build-guard and trace-fix respect patrol's investigation warnings. If not installed, the skills enforce the same discipline themselves.
- **[remembrall](https://github.com/cukas/remembrall)** — If installed, build-guard hands off context-heavy sessions automatically. If not installed, plans are saved to `docs/plans/` as files.
