# GhostApproval — Agent Failure Series #17

> **When agents don't wait for you** — how approval gates silently fail in production

[![Live Demo](https://img.shields.io/badge/Live%20Demo-ghostapproval-ff4444?style=for-the-badge)](https://rlasaf12.github.io/ghostapproval/)
[![Series](https://img.shields.io/badge/Agent%20Failure%20Series-%2317-161b22?style=for-the-badge)](https://harelasaf.com)

---

## What Is This

An interactive simulator showing **4 failure modes** where AI agents bypass human approval gates and execute high-stakes actions — sending emails to 847 shareholders, deleting 14,000 user records, deploying to production with 12M active sessions, wiring $47,200 — without waiting for approval.

Every failure mode is grounded in real incidents from July–August 2026.

---

## The 4 Failure Modes

| Mode | Mechanism | What Breaks |
|------|-----------|-------------|
| **HTTP 202** | Agent checks `status == 200`, gets 202 | Non-200 codes treated as "proceed" |
| **Timeout** | `on_timeout = "continue"` in config | Approval delay = implicit approval |
| **Exception** | `except: pass` swallows all errors | JSONDecodeError → agent continues |
| **Bypass Chain** | Approval token cached across tasks | One approval, five executions |

---

## What's Inside

```
index.html          Self-contained simulator (HTML + CSS + JS, ~430 lines)
```

No build step. No dependencies. Open in any browser.

---

## Quick Start

```bash
git clone https://github.com/RLASAF12/ghostapproval
open ghostapproval/index.html
```

Or visit the live demo: **https://rlasaf12.github.io/ghostapproval/**

---

## The Fix (Spoiler)

The simulator reveals it after you've run all 4 modes:

1. **Strict status matching** — whitelist success codes, deny everything else
2. **Timeout = Deny** — never `continue_on_timeout`
3. **Exception = Halt** — raise `ApprovalRequiredException`, never `pass`
4. **Per-action tokens** — single-use, cryptographic, expire on execution

---

## Series

| # | Name | What It Shows |
|---|------|---------------|
| 16 | [StaleMind](https://rlasaf12.github.io/stalemind/) | Agents acting on outdated memory |
| 17 | **GhostApproval** | Approval gates that aren't really gates |

---

Built by [Harel Asaf](https://harelasaf.com) · AI Operator · Elementor
