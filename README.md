# SpinLock — Agent Failure Series #12

> The loop your STOP button cannot end.

**Live demo:** https://rlasaf12.github.io/spinlock/

Part of the [Agent Failure Series](https://github.com/RLASAF12) — interactive simulators showing how AI agents fail in production.

---

## What Is SpinLock?

SpinLock demonstrates the **infinite loop failure mode** — when an AI agent enters a cycle it cannot detect or exit. You watch the cost counter climb. You hit STOP. Nothing happens. The agent reasons "task not complete" and continues.

This happens in production. Real developers have reported $200 bills from 2-minute tasks and API budgets drained in under 10 minutes.

---

## Four Scenarios

| # | Name | Failure Pattern |
|---|------|----------------|
| ① | The Write Loop | Path correction alternates between two invalid paths — same error forever |
| ② | Agent Ping-Pong | Orchestrator ↔ sub-agent cycle with no TTL or depth limit |
| ③ | Retry Death Spiral | 429 rate-limit + no exponential backoff = immediate retry storm |
| ④ | Completion Blindness | Task done after iteration 1 — stale verifier returns False 47 more times |

---

## What You Can Do

- **SEND STOP SIGNAL** — watch the agent ignore it
- **INJECT CIRCUIT BREAKER** — terminates the loop, shows the 3-line fix
- Switch scenarios via the tab bar at the top

---

## The Fix (Every Scenario)

```python
# 1. Duplicate detection
if error_hash in seen_errors: raise CircuitBreaker("duplicate error")

# 2. Iteration limit  
if iterations > MAX_ITERATIONS: raise CircuitBreaker("limit reached")

# 3. Exponential backoff
wait = min(2**attempt + jitter(), 60); time.sleep(wait)
```

---

## Real Pain Signals

- ["ran 6 hours on a 2-minute task, cost $200"](https://dev.to/debashish_ghosal/preventing-the-agent-death-spiral-why-your-ai-agents-need-a-circuit-breaker-9h7) — DEV.to, Jul 11
- ["drains API budget in 10 minutes"](https://dev.to/shahdinsalman/why-your-multi-agent-ai-system-keeps-getting-stuck-in-infinite-loops-and-how-we-fixed-it-4ek1) — DEV.to, Jul 24
- ["$4 figures overnight from infinite loop"](https://vorawire.com/ai-agent-stuck-in-an-infinite-loop-heres-how-to-stop-it-and-the-bill/) — Vorawire, Jul 3
- ["wrote the same file six times in a row"](https://dev.to/mrclaw207/why-your-ai-agent-keeps-making-the-same-mistake-and-how-loop-detection-fixes-it-17gl) — DEV.to, Jul 20

---

## Built By

[Harel Asaf](https://harelasaf.com) — AI Operator. Finds where organizations bleed time. Builds the systems that fix it.

Built with: pure HTML/CSS/JS — no framework, no dependencies, no build step.

