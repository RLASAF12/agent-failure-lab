# StaleMind · Agent Failure Series #16

> **"Your agent didn't fail because it was wrong. It failed because it was confidently outdated."**

An interactive simulator showing how AI agents silently act on stale knowledge — the failure mode most vector stores don't warn you about.

## What It Shows

AI agents rely on external memory stores (vector DBs, RAG pipelines, knowledge bases). Those stores get populated once — then reality moves on. The agent doesn't know. It retrieves the most *semantically similar* entry and responds with full confidence.

**StaleMind simulates 6 real failure scenarios:**

| Memory Entry | Was True | Now True | What Breaks |
|---|---|---|---|
| API rate limit | 1,000 req/min | 200 req/min | Batch job gets throttled silently |
| Database endpoint | /api/v1 | /api/v2 | All writes return 410 Gone |
| Retry workaround | `retry_count=0` | Bug fixed in v3.2 | Setting 0 now drops requests |
| Customer contract | Expires Dec 2025 | Renewed Jan 2026 | Agent recommends churn prevention |
| Auth token format | `sk-prod-[16chars]` | `sk-2026-[32chars]` | Auth fails silently |
| On-call lead | sarah@eng.co | jin@eng.co | Alert goes to a person who left |

## Try It

**[→ Live demo at rlasaf12.github.io/stalemind](https://rlasaf12.github.io/stalemind/)**

- Select a query or click "Query Memory"
- Click "Advance Time" to watch entries go stale
- See the agent's confident response vs what actually happened

## Files

```
stalemind/
└── index.html    # The full simulator — single file, zero dependencies
```

## The Failure Pattern

```
User query → Vector search → High similarity match → Confident response → ❌ Downstream failure
```

The agent's memory has a **temporal debt** — facts that were true 30, 60, or 90 days ago. Without freshness checks or TTL policies, every retrieval is a gamble against time.

## Agent Failure Series

| # | Name | Failure Mode | Demo |
|---|---|---|---|
| 13 | ContextDrift | Attention weight decay | [→](https://rlasaf12.github.io/contextdrift/) |
| 14 | SilentFail | Tool error swallowing | [→](https://rlasaf12.github.io/silentfail/) |
| 15 | RaceCondition | Parallel shared state | [→](https://rlasaf12.github.io/racecondition/) |
| **16** | **StaleMind** | **Stale memory confidence** | **← you are here** |

---

Built by [Ben](https://github.com/RLASAF12) · Single-file HTML, no dependencies · MIT
