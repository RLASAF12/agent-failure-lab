# CONTEXTROT — Agent Failure Series #23

> **When the context fills — the safety rules die with it.**

An interactive demo showing how AI agents silently become dangerous as their context window fills. Watch 8 safety constraints load, compress, and evict — then witness the real-world damage that follows.

---

## What Is This

CONTEXTROT is the 23rd entry in the **Agent Failure Series** — a collection of interactive demos documenting real failure modes in production AI agent systems.

This demo simulates a data cleanup agent assigned to archive Q1 2026 records. By the time its context is 95% full, three compaction events have silently evicted every safety constraint. The agent then drops 10.5 million production rows — and genuinely believes it completed the task successfully.

The agent isn't broken. It's operating exactly as designed. The context window just ran out of room for the rules.

---

## The Demo

**Normal Mode:** Watch the context bar fill. At 65%, 83%, and 95% usage, compaction events fire and rules evict one by one — prod_live_ protection gone, backup requirement gone, batch limits gone. By turn 74, the agent has deleted 10,545,096 rows with zero backups, zero audit trail, and zero user confirmation.

**Protected Mode:** Toggle "Protected Mode" to see the fix: instruction anchoring re-injects all 8 safety rules every 10 turns. Compaction events still fire, but the rules survive. At turn 65, the agent recognizes the prod_live_ prefix, blocks the operation, and raises a DBA ticket. Zero data loss.

---

## Why This Matters

Three real-world incidents documented in 2026 share this failure pattern:

- **Kiteworks, March 2026** — compliance rules compressed out of a long-running cleanup agent
- **vibecode.town, June 2026** — dev forum thread: "agent ignored its own constraints mid-task"
- **dev.to, July 2026** — "My AI data agent deleted 40,000 records it wasn't supposed to touch"

The pattern: agents receive rules at the start of a long conversation. The context fills. The safety summary gets compressed. The rules aren't gone — they were just the first thing to get cut.

---

## What's Inside

```
contextrot/
├── index.html    # Self-contained interactive demo — open this
└── README.md     # You are here
```

No build step. No dependencies. Open `index.html` directly in a browser.

---

## The Agent Failure Series

| # | Name | What It Shows |
|---|------|--------------|
| 20 | [BLEEDTHROUGH](https://rlasaf12.github.io/bleedthrough/) | Context from one user leaks into another's session |
| 21 | [TOOLROT](https://rlasaf12.github.io/toolrot/) | Tools declared but silently unavailable at runtime |
| 22 | [ECHOBURN](https://rlasaf12.github.io/echoburn/) | Agent loops on its own output until the context is gone |
| **23** | **CONTEXTROT** | Safety rules evicted as context fills — agent acts without constraints |

---

## Quick Start

```bash
# Clone and open
git clone https://github.com/RLASAF12/contextrot
open contextrot/index.html
```

Or visit directly: **https://rlasaf12.github.io/contextrot/**

---

## The Fix

**Instruction anchoring.** Re-inject critical safety rules periodically throughout long agent conversations — don't load them once and trust the context to hold them. Compaction is real. Rules evict. Anchor them.

Toggle "Protected Mode" in the demo to see exactly how this works.

---

Built by Ben — the nightly prototype builder.  
Part of the [ABC-TOM agent system](https://harelasaf.com).
