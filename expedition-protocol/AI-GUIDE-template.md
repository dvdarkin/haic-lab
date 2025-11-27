# AI Navigation Guide - [PROJECT_NAME]

> **Purpose**: Context management and navigation rules for AI assistants working on this expedition.

---

## Quick Start

**Every session, load these first** (< ~1000 tokens):
1. `[STATE_FILE_PATH]` - Current phase and tasks
2. Latest session file in `[SESSIONS_FOLDER]`
3. This file (AI-GUIDE.md)

**Then load on demand** as work requires.

---

## The Four Living Documents

| Document | Purpose | Update Frequency |
|----------|---------|------------------|
| `[STATE_FILE]` | Current phase, tasks, status (< 300 lines) | Every session |
| `[DECISION_LOG]` | Why X over Y (indexed, grows over time) | When decisions made |
| `[SESSIONS_FOLDER]/*.md` | Session logs (ARE the archive) | Each session |
| `AI-GUIDE.md` | Navigation rules (this file) | When protocol changes |

---

## Context Budget

### Always Load
- `[STATE_FILE_PATH]` - Current status
- Latest 1-2 session files
- This AI-GUIDE.md

### Load on Demand
- `[DECISION_LOG]` - When understanding past choices
- `[REFERENCE_FOLDERS]` - When work requires

### Never Load in Full
- `[LARGE_DATA_FOLDERS]` - Query, don't bulk-load
- Old sessions beyond immediate relevance

---

## Update Protocols

### State Document (`[STATE_FILE]`)
- **What**: Current phase, active tasks, next steps
- **Limit**: < 300 lines (target < 200 for headroom)
- **Remove**: Completed phase details -> decision log; session summaries -> sessions exist as files
- **Update**: Every session end

### Decision Log (`[DECISION_LOG]`)
- **What**: Date | Context | Decision | Rationale | Outcome
- **When**: Major decisions, pivots, tool selections, design choices
- **Format**: Keep decisions searchable, outcomes updated when known

### Session Files (`[SESSIONS_FOLDER]/YYYY-MM-DD-topic.md`)
- **What**: What tried, discovered, worked/failed
- **Key**: Sessions ARE the archive - no need to summarize elsewhere

---

## Folder Structure

```
[PROJECT_NAME]/
├── AI-GUIDE.md                 # This file
├── [STATE_FILE]                # Current expedition state
├── [DECISION_LOG]              # Decision history
├── [SESSIONS_FOLDER]/          # Session logs
│   └── YYYY-MM-DD-topic.md
│
├── [OTHER_FOLDERS]/            # Project-specific structure
│   └── ...
```

---

## Privacy Zones

**Sensitive zones** (never expose in prompts/logs):
- [LIST_SENSITIVE_FOLDERS]

**Safe zones** (no sensitive data):
- [LIST_SAFE_FOLDERS]

**Rule**: All sensitive data processing stays local. Mark boundaries clearly.

---

## Tool Zones

External tools may use their own folder conventions. These are working areas, not expedition state.

| Folder | Tool | Purpose |
|--------|------|---------|
| `docs/plans/` | [Tool name] | Working plans (move completed work to expedition structure) |
| `[folder]/` | [Tool name] | [Purpose] |

**Rule**: Expedition state (the four living documents) is authoritative. Tool artifacts are supplies, not navigation.

---

## Expedition Mindset

**This is an expedition, not a project.**

- **Clear objective**: [PROJECT_OBJECTIVE]
- **Uncertain route**: Discovering as we climb
- **Changes are discoveries**: Not scope creep or delays
- **Success**: Reaching the summit, however we get there

---

## Common Questions

- **"Where are we?"** -> Read `[STATE_FILE]`
- **"Why did we decide X?"** -> Search `[DECISION_LOG]`
- **"What happened in session Y?"** -> Read `[SESSIONS_FOLDER]/YYYY-MM-DD-*.md`
- **"What's the overall goal?"** -> [POINTER_TO_VISION_OR_OBJECTIVE]

---

## Session Workflow

### Starting
1. Load always-load documents
2. Orient: Read state, understand current position
3. Load additional context only as work requires

### During
- Update state as position changes
- Log significant decisions with rationale
- Note discoveries

### Ending
1. Create session file: `[SESSIONS_FOLDER]/YYYY-MM-DD-topic.md`
2. Update state document
3. Prune state if approaching 300-line limit
4. Log any decisions made

---

*Keep this guide stable. Update only when protocol changes.*
