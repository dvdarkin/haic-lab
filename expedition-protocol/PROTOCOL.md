# The Expedition Protocol

> Context management for long-running human-AI collaboration under uncertainty.

---

## The Metaphor

This is an expedition, not a project.

**Projects** assume known routes, predictable timelines, scope that can be managed. They optimize for efficiency along a planned path.

**Expeditions** assume uncertain terrain, limited supplies, and discoveries that reshape the route. They optimize for navigation under constraint.

The distinction matters because AI collaboration has hard constraints that project thinking ignores:

| Expedition Reality | AI Collaboration Reality |
|--------------------|--------------------------|
| Limited supplies | Context window is finite |
| Unknown terrain | Requirements emerge through work |
| Can't carry everything | Must choose what context to load |
| Field notes matter | Sessions are primary record |
| Base camp as anchor | State document grounds each session |
| Summit is clear, route isn't | Objective known, path discovered |

The metaphor isn't decoration - it's a **reasoning scaffold**. An AI reading "expedition" activates concepts like resource constraints, navigation vs. map-following, base camps, and field notes. These become available for analogical reasoning without explicit enumeration.

---

## The Problem

Long-running AI collaboration fails in predictable ways:

**Context loss**: New sessions forget hard-won insights. You re-explain the same context repeatedly. Setup time compounds.

**Context bloat**: Trying to preserve everything, you load too much. Signal drowns in noise. The AI loses focus.

**Drift**: Without anchoring documents, each session drifts slightly. Small divergences compound into misalignment.

**Archaeology**: Finding "why did we decide X?" requires excavating conversation history. Decisions aren't indexed.

These are symptoms of missing infrastructure - no base camp, no supply management, no field notes protocol.

---

## Core Mechanics

### The Four Living Documents

Every expedition maintains four document types:

| Document | Metaphor | Purpose | Update Frequency |
|----------|----------|---------|------------------|
| **State** | Base camp | Current position, active tasks, next steps | Every session |
| **Decisions** | Route markers | Why X over Y, indexed for retrieval | When decisions made |
| **Sessions** | Field notes | What happened, what we learned | Each session |
| **Guide** | Expedition rules | Navigation protocol, context budget | When protocol changes |

**Key insight**: Sessions ARE the archive. Don't summarize sessions into state - that creates drift between summary and reality. Sessions are the primary record; state is working memory.

### Context Budget

Context is a finite resource. Manage it like expedition supplies.

**Always load** (~1000 tokens, adjust to your context window):
- State document (current position)
- Latest session file (recent work)
- Guide document (navigation rules)

**Load on demand** (when work requires):
- Decision log (when understanding past choices)
- Older sessions (when specific history matters)
- Domain documents (when entering that territory)

**Never bulk-load**:
- Raw data files
- Complete archives
- "Just in case" context

**The discipline**: Resist the urge to load everything. More context != better results. Focused context = better results.

### State Document Constraints

The state document is working memory, not archive. Keep it tight:

- **Hard limit**: ~300 lines (target 200 for headroom)
- **Contains**: Current phase, active tasks, immediate next steps, key artifact locations
- **Excludes**: Completed work details (that's in sessions), decision rationale (that's in decision log), historical context (load on demand)

When state document grows past limit, prune:
1. Move completed phase details -> decision log
2. Remove session summaries -> sessions exist as files
3. Archive resolved blockers -> they're resolved

### Privacy Zones

Some expedition territory contains sensitive material. Demarcate explicitly:

**Sensitive zones** (never expose in prompts, logs, or outputs):
- Personal data, credentials, private content
- Raw extractions from private sources

**Safe zones** (can reference freely):
- Project metadata, technical documentation
- Code, configuration, public content

**Rule**: Mark zones in your guide. AI respects boundaries it knows about.

### Operating Principles

**Usefulness First**: Every session should deliver value, not just preparation. Avoid "base camp optimization" that never reaches the summit.

**Validate Before Commit**: Test tools and approaches before building on them. Failed expeditions often trace to untested equipment.

**Changes Are Discoveries**: Route adjustments are navigation, not failure. A pivot based on new information is the protocol working, not breaking.

### External Tool Integration

AI tools and plugins often assume folder conventions (`docs/plans/`, `.cursor/`, etc.). These can coexist with the expedition protocol:

**Expedition state is authoritative**: The four living documents define where we are. Tool-generated artifacts are supplies, not navigation.

**Isolate tool artifacts**: Let tools use their conventions, but don't mix with expedition folders. If a tool creates `docs/plans/`, that's a working area - completed work moves to expedition structure.

**Document tool zones in your guide**: List which folders belong to which tools. This prevents the AI from treating tool artifacts as expedition state.

**When conventions conflict**: Expedition protocol wins. Adapt tool usage, not navigation structure.

---

## Session Protocol

### Starting a Session

1. Load always-load documents (state, latest session, guide)
2. Orient: "Where are we?" (state document answers this)
3. Load on-demand context only as work requires
4. Begin work

### During a Session

- Update state document as position changes
- Log decisions to decision log with rationale
- Note discoveries - they may reshape the route

### Ending a Session

1. Create session file: `YYYY-MM-DD-topic.md`
2. Record: What tried, what discovered, what worked/failed
3. Update state document: Current position, next steps
4. Prune state if approaching limit

---

## When to Use This Protocol

**Good fit**:
- Multi-session work with continuity requirements
- Complex domains where context accumulates
- Projects where "why did we decide X?" matters later
- Work with sensitive data requiring privacy discipline
- Collaboration that will span weeks or months

**Poor fit**:
- Single-session tasks
- Simple Q&A interactions
- Work where context resets are acceptable
- Highly structured workflows with existing state management

**Signs you need this**:
- You're re-explaining context every session
- You can't find past decisions or their rationale
- Sessions feel disconnected from each other
- Context window fills with "just in case" content

---

## What This Protocol Doesn't Solve

**Infrastructure requirements**:

- Requires file system or document storage AI can reference
- Requires session continuity (same AI instance or context transfer)
- Requires discipline - the protocol only works if followed

**Not automatic**:

This protocol provides structure, not magic. You still need to:
- Actually prune state documents
- Actually write session files
- Actually log decisions
- Actually respect context budget

The first 3 issues can be resovled by giving explicit command to the AI agent inside the current session, after a major finding, course correction or decision: "Update expedition log".
The last one is an existing issue that may or may not affect your use case. 

---

## Emergent Extensions

The expedition metaphor enables reasoning about patterns not explicitly defined:

- **Acclimatization**: Gradual context loading for complex domains
- **Supply caching**: Pre-positioned context for anticipated needs
- **Weather windows**: Recognizing when conditions favor certain work
- **Route marking**: Breadcrumbs for decision backtracking
- **Sherpa pattern**: AI carrying context load human doesn't need to hold

These may emerge through use. The metaphor provides vocabulary for discussing them.

---

## Getting Started

1. Copy `AI-GUIDE-template.md` into your project
2. Fill in project-specific sections (folder structure, privacy zones)
3. Create initial state document
4. Point your AI at the guide
5. Start your expedition

---

*The summit is clear. The route reveals itself through climbing.*
