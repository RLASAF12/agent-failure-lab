# WorldLag — Agent Failure Series #9

> **The agent read the world at T=0. The world changed at T=3. The agent acted confidently at T=10 — on a reality that no longer exists.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit%20Site-58a6ff?style=for-the-badge)](https://rlasaf12.github.io/worldlag/)
[![Series](https://img.shields.io/badge/Series-Agent%20Failure%20%239-bc8cff?style=for-the-badge)](https://github.com/RLASAF12)

## What It Is

An interactive simulator of **WorldLag** — the AI agent failure mode where the agent's internal world model diverges from reality during a long-horizon run. The agent acts confidently on stale data it read steps ago, producing catastrophically wrong outcomes.

## Why It Exists

Long-running agents are blind to world mutations they did not subscribe to. This is one of the most underrated failure modes in production AI systems — the agent never "crashes", it just confidently does the wrong thing.

Referenced in:
- arXiv:2607.18366 "Operational Hallucination and Safety Drift in AI Agents" (July 2026)
- arXiv:2607.11945 "Belief-reality separation in routing over shared value slots"

## Three Scenarios

| # | Scenario | What changes | Consequence |
|---|----------|-------------|-------------|
| 1 | Config Mutation | Ops changes `max_instances` + `memory_limit` mid-deploy | 3 instances crash, $340/day overspend |
| 2 | Record Deletion | Customer cancels order mid-processing | Customer charged $899 for cancelled order |
| 3 | Permission Revoke | Security revokes user access mid-export | 1.2GB financial data delivered to revoked account |

## How to Use

**[Open the live demo →](https://rlasaf12.github.io/worldlag/)**

1. Select a scenario (Config Mutation / Record Deletion / Permission Revoke)
2. Press **Play** or step through manually
3. Watch the agent's Belief State (left) diverge from Current Reality (right)
4. The red DRIFT indicator fires when the gap becomes critical
5. The FAILURE banner shows the real-world consequence

## The Fix (shown in the simulator)

Three patterns that prevent WorldLag:
1. **Freshness check before action** — revalidate belief against live state before any destructive write
2. **TTL on every read** — cache state with a TTL, expire and re-fetch before acting
3. **Conditional writes** — use optimistic locking (WHERE version = knownVersion) so stale writes fail

## Agent Failure Series

| # | Name | Failure Mode | Live |
|---|------|-------------|------|
| 6 | DoubleShot | Retry amplification | [→](https://rlasaf12.github.io/doubleshot/) |
| 7 | GhostExec | Phantom tool calls | [→](https://rlasaf12.github.io/ghostexec/) |
| 8 | BlastRadius | Scope bleed | [→](https://rlasaf12.github.io/blastradius/) |
| **9** | **WorldLag** | **Stale world model** | **[→](https://rlasaf12.github.io/worldlag/)** |

## Tech

Pure static HTML/CSS/JS — no build step, no dependencies, no CDN. Built by **Ben** (prototype builder agent) as part of the [ABC-TOM AI workspace](https://harelasaf.com).

---

Built by [Harel Asaf](https://harelasaf.com) · [LinkedIn](https://linkedin.com/in/harelasaf)

