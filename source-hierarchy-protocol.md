# Source Hierarchy Protocol

> User-provided sources are ground truth. Never contradict them with training knowledge.

## The Problem

AI systems mix information sources without explicit precedence: user documents blend with training knowledge, retrieved content lacks attribution, inferences appear as facts. Result: you can't trust what's from your source vs. what the AI added.

This breaks collaboration in high-stakes work - analysis, research, decision support - where accuracy to specific sources matters.

**Root cause**: AI treats all information as equally weighted when no explicit hierarchy is declared.

## The Hierarchy

When multiple sources exist, enforce this precedence:

| Priority | Source Type | Treatment |
|----------|-------------|-----------|
| 1 | User-provided documents | Authoritative ground truth |
| 2 | User statements | Trust unless internally inconsistent |
| 3 | Retrieved/searched content | Cite explicitly with source |
| 4 | Training knowledge | Fill gaps only, flag when used |

**Key insight**: This is trust flow, not information flow. Lower-priority sources can provide context, but higher-priority sources always win conflicts.

## The Practice

### Interactive Mode (Conversation)

**1. Declare hierarchy upfront**
```
Treating [document] as authoritative.
Will extract before analyzing.
```

**2. Extract before synthesize**
- Quote specific content first
- Mark extraction complete
- Ask user to verify extraction
- Only then analyze

**3. Cite sources for every claim**
- From user document: "The document states..." or direct quote
- From search: "According to [source]..."
- From training: "My understanding is..." or "Based on general knowledge..."
- Inference: "This suggests..." or "Connecting these..."

**4. Source always wins**
If training knowledge conflicts with user source:
- Defer to source
- Don't state the contradiction as fact
- If relevant: "This differs from general understanding, but deferring to your source"

**5. Flag what's not in source**
- "The document doesn't specify X"
- "Inferring Y from [stated facts] - verify this"
- "My understanding is Z - worth confirming"

### Artifact-First Mode (Review Existing Documents)

Apply protocol to an existing document/analysis as input. Find hierarchy violations.

**Process:**
1. Identify all sources the document claims to use
2. For each factual claim, check: is source cited? Does source actually say this?
3. Flag: unmarked inferences, source contradictions, missing attributions, training knowledge stated as fact

**Output options:**
- Problem list with line references
- Corrected document with violations fixed
- Verification report

**Example review output:**
```
Reviewing: draft-analysis.md

Line 3: "Revenue grew 15%" - no source cited.
  -> Q3 Report p.2 says 14.7%. Correct and cite.

Line 7: "Industry average is 12%" - source?
  -> Not in provided documents. Flag as training knowledge or find source.

Line 12: "Enterprise drove growth" - document says consumer segment led.
  -> Source contradiction. Defer to document.

Line 15: "This suggests market share gain" - inference not marked.
  -> Add [inference] marker.
```

## Example: Before and After

**Input**: User provides quarterly earnings report, asks for analysis

**Without protocol**:
> "Revenue grew 15% year-over-year, driven by strong enterprise sales..."

Problem: May mix document facts with analyst reports from training data. User can't tell which is which.

**With protocol**:
> Treating Q3 earnings report as authoritative.
>
> From source:
> - Revenue: $X (up Y% YoY per page 2)
> - Enterprise segment: $Z (page 5)
> - Guidance: [quote from page 8]
>
> Inference:
> This suggests strong enterprise performance [my analysis, not in source].

Difference: Source declared, extraction explicit, inference clearly marked as separate from source facts.

## Detection: When You Need This

Apply when:
- User provides documents for analysis
- Multiple sources are in context
- Task requires factual accuracy
- Prior conversations/training data could conflict with new sources

Don't apply when:
- Pure brainstorming
- User wants synthesis without attribution overhead
- All sources have equal status (comparative analysis)

## Evidence

Tested in verification sessions where user provided technical documents for fact-checking. Caught:
- 3 critical errors in AI learning overview (GPT version misattribution, 76% -> 36% numerical error, wrong citation)
- Multiple claim misattributions in technical support analysis

Pattern: most errors occur when AI blends document content with training knowledge without marking the boundary.

## Common Failures

| Anti-Pattern | Correct Behavior |
|--------------|------------------|
| Stating training knowledge that contradicts document | Defer to document |
| Blending sources without labels | Separate and cite each |
| "The document shows X" (when it doesn't) | "I infer X - document doesn't state this" |
| "Studies show..." (no source) | "According to [source]..." or "My understanding..." |

---

**Related work**: Complements claim-verification protocol (which handles claims without explicit sources in context).

**Use this when**: Sources have clear precedence and accuracy to specific sources matters.
