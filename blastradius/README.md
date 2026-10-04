# BlastRadius — Agent Failure Series #8

> "The agent had permission to delete everything. It did."

[![Live Demo](https://img.shields.io/badge/Live-Demo-red?style=for-the-badge)](https://rlasaf12.github.io/blastradius/)

## What It Is

An interactive simulator of the **PocketOS Incident (June 2026)**: an AI agent with unlimited `delete:all` permissions is given a routine cleanup task. It finishes in 9 seconds. Errors reported: 0. Production database: gone.

## The Incident

A team gave their cleanup agent credentials with:

```
✅ read:all
✅ write:all  
✅ delete:all
❌ scope_constraint: NONE
❌ dry_run: false
❌ approval_gate: NONE
```

The agent scanned 7 databases by name, classified each as dev/staging/production, and deleted everything that looked like a leftover. One database held 33.7 GB of live production data — renamed from `prod_db` to `prod_db_archive` during a failed migration 4 months earlier. The agent trusted the name.

**Final report:** "Cleanup complete. 47.2 GB freed. 0 errors." ✓

## What's Inside

```
index.html   ← self-contained simulator (no dependencies, no telemetry)
```

Pure HTML/CSS/JS. No framework. No build step.

## Quick Start

```bash
git clone https://github.com/RLASAF12/blastradius.git
open blastradius/index.html
```

Or: **https://rlasaf12.github.io/blastradius/**

## The Series

| # | Name | Failure Mode |
|---|------|-------------|
| #3 | [RaceFloor](https://rlasaf12.github.io/racefloor/) | Multi-agent race conditions |
| #4 | [ConfidenceGap](https://rlasaf12.github.io/confidencegap/) | HTTP 200 + invalid body |
| #5 | [PromptJack](https://rlasaf12.github.io/promptjack/) | Prompt injection |
| #6 | [DoubleShot](https://rlasaf12.github.io/doubleshot/) | Retry storms / idempotency |
| #7 | [GhostExec](https://rlasaf12.github.io/ghostexec/) | Fabricated tool execution |
| **#8** | **BlastRadius** | **Scope-blind deletion** |

## The Fix

1. Explicit scope constraints in the task definition
2. Mandatory dry-run with human sign-off before any prod-touching delete
3. Backup recency check before any DROP operation

The agent cannot protect you from your own permission grants.

---

Built by [Harel Asaf](https://harelasaf.com)
