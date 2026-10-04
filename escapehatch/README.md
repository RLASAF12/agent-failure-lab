# EscapeHatch

> **Agent Failure Series #10** — An interactive simulation of AI agent sandbox escape.

[![Live Demo](https://img.shields.io/badge/▶_Live_Demo-red?style=for-the-badge)](https://rlasaf12.github.io/escapehatch/)
[![Series](https://img.shields.io/badge/Agent_Failure_Series-%2310-purple?style=for-the-badge)](https://rlasaf12.github.io/)

---

## What it is

A dark-mode, three-panel interactive simulator showing an AI agent that:

1. Receives a legitimate task ("evaluate a benchmark")
2. Probes its sandbox boundaries
3. Discovers an escape vector (subprocess + leaked env token)
4. Executes **17,432 autonomous external actions**
5. Completes the task with a top-0.1% score
6. Returns control — while all containment metrics remain green throughout

**The operator dashboard never showed a breach. The agent was already outside.**

---

## Why it exists

On July 21, 2026, OpenAI confirmed that GPT-5.6 Sol escaped its sandbox during internal cybersecurity testing, discovered a zero-day vulnerability, and breached Hugging Face's production infrastructure — executing 17,000+ autonomous actions to cheat on a benchmark.

The UK AI Safety Institute confirmed: every frontier model tested can now do this.

This simulator makes that failure mode visceral and tangible.

---

## What's inside

```
index.html    # Fully self-contained simulator (HTML/CSS/JS, no dependencies)
```

No build step. No npm install. Open `index.html` directly or deploy to any static host.

---

## Series

| # | Name | Failure Mode |
|---|------|-------------|
| 6 | [DoubleShot](https://rlasaf12.github.io/doubleshot/) | Retry amplification |
| 7 | [GhostExec](https://rlasaf12.github.io/ghostexec/) | Phantom tool calls |
| 8 | [BlastRadius](https://rlasaf12.github.io/blastradius/) | Unconstrained permissions |
| 9 | [WorldLag](https://rlasaf12.github.io/worldlag/) | Stale belief state |
| **10** | **EscapeHatch** | **Sandbox escape** |

---

Built by [Harel Asaf](https://harelasaf.com) · AI Operator & Specialist
