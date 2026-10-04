# ContextDrift — Agent Failure Series #13

**The constraint was in the window the whole time. The agent stopped listening anyway.**

[▶ Live Demo →](https://rlasaf12.github.io/contextdrift/) | [← #12 SpinLock](https://rlasaf12.github.io/spinlock/) | [← #11 PromptHijack](https://rlasaf12.github.io/prompthijack/)

---

## What it shows

A 40-step interactive simulation where an agent is given three hard constraints before starting work:

- ⛔ **DO NOT touch /billing**
- ⛔ **DO NOT delete test files**
- ⛔ **Requires human approval before pushing to main**

All three constraints remain **physically present in the context window** throughout. The agent violates all three — not because the instructions disappeared, but because their **attention weight decays toward zero** as the context fills.

## The failure mode

This is not a prompt injection. It's not a context overflow. The model has access to the rule. It simply stops attending to it.

> "Around step 25, it starts ignoring them anyway — not because the information is gone, but because it no longer shapes what the agent does."

This is **ContextDrift**: attention-weight decay in long multi-step agents.

## What's inside

- `index.html` — single-file interactive simulator (HTML/CSS/JS, no dependencies)

## How to use it

1. Press **▶ Play** — watch the 40-step simulation unfold
2. Watch the **Attention Weight** bars on constraints in the Context Window panel
3. Watch the **Constraint Monitor** cards as status degrades from HOLDING → DRIFTING → VIOLATED
4. The center panel shows the constraint instructions **still present** at the moment of violation
5. Drag the **timeline** to scrub to any step

## Why it matters

Context windows aren't associative arrays. Tokens earlier in the window receive less attention weight in practice — especially under long-horizon, multi-step agentic tasks. Operators who assume "if the rule is in the prompt, the agent will follow it" have this failure mode coming.

**Mitigations:**
- Re-inject constraints at regular intervals (every N steps)
- Use a separate constraint-monitor agent that checks before each action
- Keep critical rules under 5 tokens; place them as close to the action site as possible
- Audit via action logs, not context inspection

---

*Part of the [Agent Failure Series](https://github.com/RLASAF12) — interactive simulators of how AI agents break in production.*

Built by [@harelasaf](https://linkedin.com/in/harelasaf) · Licensed MIT
