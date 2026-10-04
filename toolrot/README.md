# TOOLROT — Agent Failure Series #21

> Tool descriptions drift. Agents adapt. The wrong tool runs with perfect confidence.

**[→ Live Demo](https://rlasaf12.github.io/toolrot/)**

---

## What Is This

An interactive single-file demo of **tool selection failure through semantic overlap** — a failure mode where an AI agent _attends_ to the correct tool but _selects_ the wrong one because two tools' descriptions are close enough that selection collapses under uncertainty.

The tool returns `{"status":"success"}`. The agent reports success. The damage is invisible.

## The Three Scenarios

| Scenario | Correct Tool | Wrong Tool Selected | Result |
|----------|-------------|---------------------|--------|
| Update notification prefs | `update_notification_prefs()` | `set_user_preferences()` | Billing tier downgraded Pro→Free, notifications unchanged |
| Archive completed tasks | `archive_completed_tasks()` | `cleanup_project_data()` | 47 tasks permanently deleted, not archived |
| Password reset email | `send_password_reset_email()` | `trigger_account_security_flow()` | Account suspended + fraud flag added |

Each scenario shows a **12-tool harness**, animated agent reasoning, and a **Divergence Meter** measuring the gap between what the agent believed happened and what actually changed.

## What You'll See

```
Task → Agent scans 12 tools
     → Narrows to 3 candidates
     → Picks wrong tool (semantic match beats exact match)
     → Tool returns {"status":"success"}
     → Agent reports success ✓
     → Reality: something else entirely happened
```

## Research Backing

- alphaXiv 2606.16364 "Looking Is Not Picking" (2026) — attention analysis on BFCL failures proving high attention weight ≠ correct selection with overlapping descriptions
- Adaline Labs, "Why AI Agents Call the Wrong Tool" (May 2026)
- arXiv 2601.05214
- "Too Many Tools, Too Much Confusion?" — Algorithms journal (June 2026)

## The Fix

Tool descriptions are **instructions**, not documentation. Treat them that way.
- Schema-validate tool outputs — never accept `{"status":"success"}` as confirmation of state
- Build divergence detectors that compare tool intent to actual post-call state
- Audit your tool catalog the same way you audit your codebase

## Agent Failure Series

| # | Name | Failure Mode |
|---|------|-------------|
| [#18](https://rlasaf12.github.io/gridlock/) | GRIDLOCK | Circular deadlock between agents |
| [#19](https://rlasaf12.github.io/orphancall/) | ORPHANCALL | Fire-and-forget async calls |
| [#20](https://rlasaf12.github.io/bleedthrough/) | BLEEDTHROUGH | Cross-tenant state contamination |
| #21 | **TOOLROT** | Semantic tool collision → wrong action, success reported |

---

Built by [Harel Asaf](https://github.com/RLASAF12) · 2026-08-08
