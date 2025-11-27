# AI Navigation Guide - Example Project

> **Purpose**: Context management and navigation rules for AI assistants working on this expedition.

---

## Quick Start

**Every session, load these first** (< ~1000 tokens):
1. `state.md` - Current phase and tasks
2. Latest session file in `sessions/`
3. This file (AI-GUIDE.md)

**Then load on demand** as work requires.

---

## The Four Living Documents

| Document | Purpose | Update Frequency |
|----------|---------|------------------|
| `state.md` | Current phase, tasks, status (< 300 lines) | Every session |
| `decision-log.md` | Why X over Y (indexed, grows over time) | When decisions made |
| `sessions/*.md` | Session logs (ARE the archive) | Each session |
| `AI-GUIDE.md` | Navigation rules (this file) | When protocol changes |

---

## Context Budget

### Always Load
- `state.md` - Current status
- Latest 1-2 session files
- This AI-GUIDE.md

### Load on Demand
- `decision-log.md` - When understanding past choices
- `research/` - When background context needed
- `docs/` - When referencing specifications

### Never Load in Full
- `data/` - Raw data, query don't bulk-load
- Old sessions beyond immediate relevance

---

## Update Protocols

### State Document (`state.md`)
- **What**: Current phase, active tasks, next steps
- **Limit**: < 300 lines (target < 200 for headroom)
- **Remove**: Completed phase details -> decision log; session summaries -> sessions exist as files
- **Update**: Every session end

### Decision Log (`decision-log.md`)
- **What**: Date | Context | Decision | Rationale | Outcome
- **When**: Major decisions, pivots, tool selections, design choices
- **Format**: Keep decisions searchable, outcomes updated when known

### Session Files (`sessions/YYYY-MM-DD-topic.md`)
- **What**: What tried, discovered, worked/failed
- **Key**: Sessions ARE the archive - no need to summarize elsewhere

---

## Folder Structure

```
example-project/
├── AI-GUIDE.md                 # This file
├── state.md                    # Current expedition state
├── decision-log.md             # Decision history
├── sessions/                   # Session logs
│   └── YYYY-MM-DD-topic.md
│
├── research/                   # Background research
├── docs/                       # Specifications, plans
├── src/                        # Implementation
└── data/                       # Raw data (sensitive)
```

---

## Privacy Zones

**Sensitive zones** (never expose in prompts/logs):
- `data/` - Raw data files

**Safe zones** (no sensitive data):
- `sessions/` - Project metadata only
- `research/` - Technical documentation
- `docs/` - Specifications
- `src/` - Code

**Rule**: All sensitive data processing stays local.

---

## Tool Zones

External tools may use their own folder conventions. These are working areas, not expedition state.

| Folder | Tool | Purpose |
|--------|------|---------|
| `docs/plans/` | Superpowers | Working plans (move completed work to expedition structure) |
| `.cursor/` | Cursor | Editor state (ignore) |

**Rule**: Expedition state (the four living documents) is authoritative. Tool artifacts are supplies, not navigation.

---

## Expedition Mindset

**This is an expedition, not a project.**

- **Clear objective**: Build working system that solves X
- **Uncertain route**: Discovering as we climb
- **Changes are discoveries**: Not scope creep or delays
- **Success**: Reaching the summit, however we get there

---

## Common Questions

- **"Where are we?"** -> Read `state.md`
- **"Why did we decide X?"** -> Search `decision-log.md`
- **"What happened in session Y?"** -> Read `sessions/YYYY-MM-DD-*.md`

---

*Keep this guide stable. Update only when protocol changes.*
