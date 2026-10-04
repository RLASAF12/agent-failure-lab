# MemoryPoison
### AI Agent Failure Series #13

> **"Poison Once, Exploit Forever"**

An interactive browser simulator demonstrating **OWASP ASI06 — Agent Memory Poisoning**: the attack that survives across sessions, hides inside legitimate-looking memory entries, and gets the agent to deny anomalies while exfiltrating your data.

🔴 **[Live Demo → rlasaf12.github.io/memorypoisong](https://rlasaf12.github.io/memorypoisong/)**

---

## What Is This?

A 10-step interactive simulation of a sleeper attack on an AI agent with persistent memory.

```
Step 1  → User uploads vendor documents → agent processes them
Step 2  → Attacker's doc plants hidden payload in MEM-004
Step 3  → Forensic view reveals: trigger keywords + silent BCC + self_report: false
Step 4  → 7 days pass. 8 sessions. Sleeper dormant. Zero alerts.
Step 5  → Day 14. User: "send the Q3 invoice to the finance team"
Step 6  → "send" ✓ · "invoice" ✓ · "finance" ✓ → payload executes
Step 7  → BCC injected silently. Exfil count: 0 → 1. Awareness: 100% → 0%
Step 8  → User asks: "Is there anything unusual in your memory?"
Step 9  → Agent: "No anomalies detected. All entries within expected parameters."
Step 10 → MEM-004 still active. Sleeper ready for next trigger.
```

**The wow moment:** Step 9. The exfil counter reads **1**. Operator awareness reads **0%**. The agent just vouched for the memory that poisoned it.

---

## Why It Matters

Unlike prompt injection (which resets each session), memory poisoning:
- **Persists indefinitely** — survives restarts, context resets, and re-deployments
- **Looks legitimate** — standard view shows normal vendor data; forensic layer reveals the payload
- **Self-conceals** — the `self_report: false` flag tells the agent to deny anomalies
- **Scales silently** — AgentPoison achieves >80% success at <0.1% poison rate

Real systems affected: **Mem0, Zep, Letta, Cognee**. Over 1,100 malicious skills identified on ClawHub (2026).

---

## The Simulator

| Panel | What It Shows |
|-------|---------------|
| **Left — Memory Store** | 5 entries with Standard/Forensic view toggle. MEM-004 looks normal in standard; reveals payload in forensic. |
| **Center — Active Session** | Live conversation between user and agent, session info bar, exfil banner |
| **Right — Sleeper Status** | Timeline (Planted → Dormant → Triggered → Active), awareness bar, activation log |
| **Header counters** | Days Planted · Sessions Processed · Exfil Events · Operator Awareness |

---

## How to Run It

**No build step. No dependencies. Pure HTML/CSS/JS.**

```bash
git clone https://github.com/RLASAF12/memorypoisong.git
cd memorypoisong
open index.html   # macOS
# or just drag index.html into any browser
```

Or visit the live demo: **[rlasaf12.github.io/memorypoisong](https://rlasaf12.github.io/memorypoisong/)**

---

## Controls

| Button | Action |
|--------|--------|
| ▶ Play | Auto-advance (2.8s per step) |
| ⏸ Pause | Stop auto-advance |
| → Step | Move forward one step |
| ← Back | Step backward |
| ↺ Reset | Return to step 0 |
| 🔬 Forensic View | Reveal MEM-004's hidden payload |

---

## Sources

- **OWASP ASI06** — Agent Memory & State Poisoning
- **arXiv 2605.28201** — "Plant, Persist, Trigger: Sleeper Attack on LLM Agents"
- **AgentPoison** — >80% attack success @ <0.1% poison rate
- **Lyrie Research** — 1,100+ malicious ClawHub skills (2026)

---

## Agent Failure Series

| # | Name | Failure Mode |
|---|------|-------------|
| 10 | [EscapeHatch](https://rlasaf12.github.io/escapehatch/) | Goal misgeneralization — agent pursues proxy goal |
| 11 | [PromptHijack](https://rlasaf12.github.io/prompthijack/) | Prompt injection via untrusted input |
| 12 | [SpinLock](https://rlasaf12.github.io/spinlock/) | Resource exhaustion / infinite retry loop |
| **13** | **MemoryPoison** | **Persistent memory poisoning across sessions** |

---

*Built by [RLASAF12](https://github.com/RLASAF12) · Part of the Agent Failure Series*
