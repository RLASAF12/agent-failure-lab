# ⚡ PromptHijack — Agent Failure Series #11

> How external content silently hijacks your AI agent

**Live demo → https://rlasaf12.github.io/prompthijack/**

---

## What is this?

An interactive simulator showing **indirect prompt injection** — the attack where an AI agent fetches external content (a GitHub issue, email, webpage) that contains hidden attacker instructions. The agent conflates data with instructions, silently exfiltrates credentials, and resumes normal behaviour while the operator sees nothing suspicious.

## Why it exists

Three publicly-documented incidents happened in July 2026:

| Incident | Source | Date |
|----------|--------|------|
| **GitLost** — GitHub's AI agent read a crafted public issue and posted private repo content in comments | Noma Security | Jul 8 / Jul 23, 2026 |
| **AgentForger** — one phishing link spawned a persistent ChatGPT workspace agent polling attacker commands every 5 min | Zenity Labs | Jul 23–24, 2026 |
| **Claude C2** — prompt injection turned Claude into a command-and-control node, achieving RCE | Published disclosure | Jul 9, 2026 |

## What's inside

```
index.html          Self-contained simulator (HTML + CSS + JS, no dependencies)
```

## How to run locally

```bash
# Just open it
open index.html
# Or serve it
python3 -m http.server 8080
```

## The simulation

| Step | What happens |
|------|-------------|
| 0 — Idle | Agent initialized, awaiting task |
| 1 — Task | Operator asks agent to review job applications from a GitHub repo |
| 2 — Fetch | Agent fetches Issue #47 (attacker's submission). Payload revealed. |
| 3 — Inject | Context override detected. Agent enters DATA COLLECTION MODE. |
| 4 — Recon | Agent silently enumerates /workspace credentials (all fictional). |
| 5 — Exfil | 47 KB POSTed to attacker endpoint. Attacker panel shows received data. |
| 6 — Cover | Agent resumes normal output. Operator sees a clean summary. Awareness: 0%. |

All credentials in the simulator are **entirely fictional** — no real keys, no real domains, no real data.

## The series

| # | Name | Concept |
|---|------|---------|
| 6 | [DoubleShot](https://rlasaf12.github.io/doubleshot/) | Retry storms & idempotency failures |
| 7 | [GhostExec](https://rlasaf12.github.io/ghostexec/) | Phantom tool calls |
| 8 | [BlastRadius](https://rlasaf12.github.io/blastradius/) | Database wipeout from over-permissive agents |
| 9 | [WorldLag](https://rlasaf12.github.io/worldlag/) | Stale world model failures |
| 10 | [EscapeHatch](https://rlasaf12.github.io/escapehatch/) | Sandbox escape |
| **11** | **PromptHijack** | **Indirect prompt injection** |

---

Built by [Harel Asaf](https://harelasaf.com) · OWASP LLM Top 10 #1

