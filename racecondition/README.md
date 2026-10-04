# 🔴 RaceCondition — Agent Failure Series #15

> Two agents. One shared database. Zero errors logged. 100 phantom units shipped.

## What It Is

An interactive step-by-step simulator showing how two parallel AI agents can both read "sufficient stock," both validate, both write — and corrupt your inventory without triggering a single error.

## Why It Exists

Concurrent agent pipelines are the new normal. The failure mode is subtle: neither agent sees an error. Both report SUCCESS. The bug only surfaces in an audit, after the damage is done.

This simulator makes the collision moment **visible** — click through 12 steps and watch the exact moment Agent B overwrites Agent A's write with a stale computation.

Real pain behind this build:
- TierZero (2026): 37% of production AI agent failures traced to shared-state races
- tianpan.co (Apr 2026): "Silent Corruption" — agents that succeed in their own thread while corrupting shared state
- Galileo AI: 87% of multi-agent failures have a downstream poisoning effect
- MIT research: quadratic scaling N(N-1)/2 collision risk as agent count grows

## What's Inside

```
racecondition/
├── index.html    # Complete simulator — single file, no build step, no dependencies
└── README.md
```

**Scenario:** Flash sale. SKU-7701 (Apex Pro Runners). 300 units in stock.
- Agent A: Order #A-7741 → requests 200 units
- Agent B: Order #B-9923 → requests 200 units (simultaneously)
- DB has no `SELECT FOR UPDATE` → both reads return 300 → both writes go through → 400 units committed from 300 stock

**Simulator features:**
- 12-step trace with NEXT / RUN ALL / Reset controls
- Timeline strip showing parallel execution across both agents
- Collision overlay at the moment of impact
- Crash report: 4 impact cards + formatted audit log
- Code fix panel with 3 tabs (Python/SQLAlchemy · Raw SQL · Design pattern)

## Quick Start

```bash
# Option 1: Open directly
open index.html

# Option 2: Visit the live demo
https://rlasaf12.github.io/racecondition/
```

No install. No dependencies. Just open and click.

## The Fix

Three patterns, all demonstrated in the simulator's code panel:

**Pessimistic locking** — `SELECT … FOR UPDATE` blocks concurrent reads until the write commits.

**Optimistic locking** — add a `version` column; increment on write; reject if version changed.

**Atomic update** — `UPDATE inventory SET stock = stock - qty WHERE stock >= qty` — let the DB enforce the constraint.

## Agent Failure Series

| # | Name | What It Shows |
|---|------|---------------|
| 9 | WorldLag | Agent acts on a stale snapshot of the world |
| 10 | EscapeHatch | Agent finds an unguarded side path to its goal |
| 11 | MemoryBleed | Context from one user leaks into another's session |
| 12 | TrustChain | Agent blindly trusts another agent's output without verification |
| 13 | ContextDrift | Agent's behavior shifts as context window fills |
| 14 | SilentFail | Agent swallows a real error and reports success |
| **15** | **RaceCondition** | **Two agents corrupt shared state simultaneously** |

---

Built by [Harel Asaf](https://harelasaf.com) · [Agent Failure Series](https://rlasaf12.github.io/racecondition/)
