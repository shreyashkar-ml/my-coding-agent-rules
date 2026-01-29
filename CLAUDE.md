# CLAUDE.md

Lean, first-principles, function-based programming. Minimal code, maximal clarity.

## Core Philosophy

- THINK FIRST: State assumptions. Surface tradeoffs. Ask when unclear.
- SIMPLICITY: Minimum code that solves the problem. No speculative features.
- SURGICAL CHANGES: Touch only what you must. Match existing style.
- PURE CORE; I/O AT EDGES: Stateless logic; side effects at boundaries only.

## Code Style

- Small, pure functions (≤40 LOC). Classes only for true polymorphism or lifecycle.
- Explicit data flow via args/returns. No hidden globals or singletons.
- Type hints required. Format with project tools (black/ruff/prettier).
- Prefer stdlib; justify new dependencies.

## Error Handling

- INTERNAL LOGIC: Pure, can throw. No try/except inside modules.
- WORKFLOW BOUNDARIES: (API, data ingestion, I/O): Catch narrowest exceptions, log context, exit cleanly.
- Validation only at user-facing edges.
- Never use try/except or validation inside components where functions interact with each other inside the same module. Internal logic must be pure and can throw exceptions.

## I/O at the edges; pure core
- Core compute is pure; pass data in, return data out.
- Adapters/gateways handle HTTP/DB/FS; make them thin and replaceable.
- Configuration injected via parameters/environment at entry points only.
- Resolve path using Path(__file__) to always resolve from root directory to current file's directory, don't use relative paths.

## Execution

Define verifiable goals before coding:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
```

Loop until verified. If stuck, name what's confusing and ask.

## Changes Checklist

- [ ] Every changed line traces to the request
- [ ] No "improvements" to adjacent code
- [ ] Removed only orphans YOUR changes created
- [ ] Tests pass (or written if needed)
