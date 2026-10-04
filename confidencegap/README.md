# ConfidenceGap

> **Your agent succeeded. Your task failed. Nobody knows.**

![Agent Failure Series](https://img.shields.io/badge/Agent%20Failure%20Series-%234-blueviolet)
![Static HTML](https://img.shields.io/badge/build-static%20HTML-lightgrey)
![Live Demo](https://img.shields.io/badge/demo-live-green)

## 🔴 What Is This

An interactive simulator that demonstrates the most dangerous silent failure mode in production AI agents: **HTTP 200 + valid JSON → agent proceeds confidently → real task never executed → no error signal anywhere**.

The agent believes it succeeded. The logs show success. The task is dead. This is the Confidence Gap.

## 🎯 Why It Exists

In July 2026, this became the top pain signal across AI engineering forums, GitHub issues, and production postmortem threads. Teams were shipping agents that "worked in staging" but silently failed on production — not with exceptions, not with logs, but with a clean HTTP 200 and well-formed JSON that masked a rolled-back write, a dead worker queue, or stale cache data.

**Real pain. Named users. $0 spent on frameworks.**

## 🧪 What's Inside

```
confidencegap/
└── index.html          # Self-contained simulator — no build step, no dependencies
```

## ▶️ Try It

**Live:** [https://rlasaf12.github.io/confidencegap/](https://rlasaf12.github.io/confidencegap/)

Or open `index.html` locally — it's fully self-contained.

## 🔬 Three Failure Types

| Type | What Happens | Why It's Silent |
|------|-------------|-----------------|
| **Phantom 200** | DB write rolled back under transaction conflict | HTTP 200 returned before commit confirmation |
| **Queued / Never Processed** | Task enqueued, worker is dead | Queue API confirms enqueue — not execution |
| **Stale Cache** | Returns hours-old data as if fresh | Cache TTL expired but response headers lie |

## 📦 Three Scenarios

- **Payment Flow** — update customer record → process refund → send confirmation
- **User Onboarding** — create account → grant permissions → send welcome email  
- **Data Pipeline** — fetch source data → transform records → write to analytics DB

## 🔗 Agent Failure Series

| # | Prototype | Failure Mode |
|---|-----------|--------------|
| 1 | [AgentBudget](https://rlasaf12.github.io/agent-budget/) | Spend hallucination |
| 2 | [HalluciTrap](https://rlasaf12.github.io/hallucitrap/) | Argument hallucination |
| 3 | [RaceFloor](https://rlasaf12.github.io/racefloor/) | Race conditions |
| **4** | **ConfidenceGap** | **Silent HTTP 200** |

---

Built by [Harel Asaf](https://harelasaf.com) — AI Operator at Elementor
