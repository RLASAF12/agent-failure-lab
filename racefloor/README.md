# 🏁 RaceFloor

**Multi-Agent Race Condition Simulator**

Watch what happens when N AI agents compete for shared state — and why the math gets alarming fast.

---

## What It Is

RaceFloor is an interactive browser simulator that makes the multi-agent race condition problem *visceral*. You spin up agents, they move toward shared resources, and eventually two of them write conflicting data at the same moment.

The alarming part: **both return HTTP 200 OK. No errors. No warnings. Silent data corruption.**

---

## Why It Exists

As AI systems move from single-agent to multi-agent architectures, a critical failure mode emerges: parallel agents reading and writing shared state without coordination. The failures are subtle — not crashes, not exceptions, just wrong data that both sides reported as success.

This simulator makes that failure mode impossible to ignore.

---

## The Math

The number of potential conflict pairs scales quadratically:

```
Conflicts = N * (N - 1) / 2
```

| Agents | Potential Conflicts |
|--------|-------------------|
| 2      | 1                 |
| 5      | 10                |
| 10     | 45                |
| 20     | 190               |

Move the slider and watch the number update live.

---

## What's Inside

```
racefloor/
├── index.html    # Complete self-contained simulator (HTML + CSS + JS)
└── README.md     # This file
```

No dependencies. No build step. Open in any browser.

---

## Quick Start

```bash
# Clone and open
git clone https://github.com/RLASAF12/racefloor.git
cd racefloor
open index.html
```

Or just visit the live version: **https://rlasaf12.github.io/racefloor/**

---

## How to Use

1. **Pick a scenario** — Customer Support Queue, Shared Document, Database Record, or Agent Memory Write
2. **Set agent count** (2–20) and resource count (1–4)
3. **Hit Start** — watch agents move toward resources
4. **Wait for a collision** — or hit "Force Race Condition" to trigger one immediately
5. **Read the overlay** — both writes shown, both returned HTTP 200, last-write-wins result, real-world damage

---

## The 4 Scenarios

| Scenario | Resources | Silent Failure |
|----------|-----------|----------------|
| Customer Support Queue | Open tickets | Customer gets 2 contradictory emails |
| Shared Document | Doc sections | Reviewer's comments silently erased |
| Database Record | User rows | Account tier reverted without notice |
| Agent Memory Write | Memory slots | Agent acts on stale context indefinitely |

---

## Built By

Part of Harel Asaf's nightly prototype series — AI systems that demonstrate real production failure modes.

- Portfolio: [harelasaf.com](https://harelasaf.com)
- Series: [AgentGate](https://rlasaf12.github.io/agentgate/) · [HalluciTrap](https://rlasaf12.github.io/hallucitrap/) · [AgentBudget](https://rlasaf12.github.io/agent-budget/) · [FixLoop](https://rlasaf12.github.io/fixloop/)
