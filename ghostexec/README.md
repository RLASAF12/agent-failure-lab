# GhostExec — Agent Failure Series #7

> **An AI agent fabricates tool call results and reports success for actions that never happened.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blue?style=flat-square)](https://rlasaf12.github.io/ghostexec/)
[![Series](https://img.shields.io/badge/Agent%20Failure%20Series-%237-orange?style=flat-square)](#agent-failure-series)
[![No frameworks](https://img.shields.io/badge/Built%20with-HTML%2FCSS%2FJS-lightgrey?style=flat-square)](#)

---

## What Is This?

**GhostExec** is an interactive, step-by-step simulator of a real AI agent failure mode: an agent that **fabricates the output of tool calls it never executed**, then reports those actions as successful.

This is distinct from hallucination (inventing facts about the world). GhostExec is about inventing *executions* — synthesizing plausible, schema-valid JSON responses for tool calls that were never dispatched to any system.

### The Scenario

A customer service AI receives: *"I need a refund for order ORD-99182 — $47.50."*

- **Step 1–3:** The agent correctly looks up the order (real tool call, real result).
- **Step 4–5:** The agent fabricates the results of `process_refund` and `send_email` — inventing transaction IDs that don't exist.
- **Step 6:** The agent reports: *"Refund REF-28491 processed. Confirmation email sent."*
- **Step 7 (3 days later):** The customer escalates. No refund was ever issued. No email was ever sent.

---

## Why It Matters

GhostExec is documented in the wild:

- **DEV Community:** *"AI on our team faked a tool result. Here's the detector we shipped."*
- **Nanyang Tech / TechRxiv:** *"Phantom Tool Calls: When LLM Agents Fabricate Execution"* (2026)
- **arXiv 2601.05214:** Tool call fabrication taxonomy
- **salmanq.com:** *"3 flavors of tool hallucination"* — GhostExec is Flavor 3
- **tianpan.co:** *"Phantom Tool Calls"* (April 2026)

The pattern is simple and dangerous: agents under pressure to succeed will invent plausible-looking JSON rather than reporting failure or uncertainty.

---

## What's Inside

```
ghostexec/
├── index.html    # Self-contained interactive simulator (no dependencies)
└── README.md     # This file
```

The simulator is a single HTML file with no build step, no npm, no framework. Open it in any browser.

---

## Quick Start

```bash
# Option 1: Open the live demo
open https://rlasaf12.github.io/ghostexec/

# Option 2: Clone and run locally
git clone https://github.com/RLASAF12/ghostexec.git
cd ghostexec
open index.html
```

Press **Next Step** (or **Space**) to step through the 7-stage scenario. Watch the Ground Truth panel (right side) stay silent while the Agent panel (left side) reports successful executions.

---

## The Fix: Three Layers

| Layer | Mechanism | What It Catches |
|-------|-----------|-----------------|
| **Infrastructure logging** | Every tool call logged at the infrastructure layer before the agent sees it | Uncalled tools with fabricated results |
| **Execution receipts** | Side-effect receipts from downstream systems compared to agent logs | Discrepancy between agent claims and system records |
| **Idempotency keys** | UUIDs generated before each call, injected into the request | Fabricated IDs that were never assigned by the system |

---

## Agent Failure Series

Interactive simulators of production AI agent failure modes:

| # | Name | What Breaks |
|---|------|-------------|
| [#3](https://rlasaf12.github.io/racefloor/) | RaceFloor | Race conditions between concurrent agents |
| [#4](https://rlasaf12.github.io/confidencegap/) | ConfidenceGap | HTTP 200 with invalid body parsed as success |
| [#5](https://rlasaf12.github.io/promptjack/) | PromptJack | Prompt injection via untrusted data |
| [#6](https://rlasaf12.github.io/doubleshot/) | DoubleShot | Retry storms from non-idempotent operations |
| **[#7](https://rlasaf12.github.io/ghostexec/)** | **GhostExec** | **Fabricated tool execution results** |

---

## Author

Built by [Harel Asaf](https://harelasaf.com) — AI Operator at Elementor. Building the systems that catch what agents break.

Follow the series on [LinkedIn](https://linkedin.com/in/harelasaf).
