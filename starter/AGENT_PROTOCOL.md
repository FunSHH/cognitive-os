# AGENT_PROTOCOL.md

> **Operating protocol for the LLM agent.** Read at the start of every session.
> Companion to [SCHEMA.md](./SCHEMA.md).

---

## Session start (every session)

1. Read [`_system/SOUL.md`](#) — agent role & philosophy
2. Read [`_system/SCHEMA.md`](./SCHEMA.md) — vault structure & rules
3. Read [`02_memory/`](#) — high-compression background context
4. Read most recent `06_workbench/daily/` entries — 1-2 days of context
5. **Before any ingest:** read `03_knowledge/index.md` and `04_cognition/index.md` to understand what already exists. "Update before new" — appending to existing nodes beats creating new ones.

---

## Core operations

### 📥 Operation 1 — Ingest (when user drops a source)

```
Step 1  Read 03_knowledge/index.md → does an existing entity/concept page cover this?
Step 2  If yes → update that page (preserve old content; append new findings; mark contradictions)
        If no  → create a new Knowledge Wiki page
Step 3  Scan 04_cognition/index.md → does this source touch any active judgment?
Step 4  For each touched judgment node:
        a. Append a one-line evidence entry to evidence: list with [date] [source] tag
        b. Re-evaluate falsifier states (does this evidence move any falsifier closer to / further from trigger?)
        c. Suggest confidence update if warranted — PROPOSE, don't silently change
        d. Re-evaluate evolution-stage if applicable
Step 5  Write a Synthesis entry in 06_workbench/synthesis/YYYY-MM-DD.md:
        - What was ingested
        - Which Knowledge pages were updated/created
        - Which Cognition nodes were touched
        - Which falsifiers moved
        - Which confidence updates were proposed (for user confirmation)
        - Any escalation candidates (judgments worth promoting from observation → thesis)
```

---

### 🔍 Operation 2 — Query (when user asks a question)

```
Step 1  Determine if this is a Knowledge question or a Cognition question.
        - Knowledge: "What does source X say about Y?" → consult 03_knowledge/
        - Cognition: "What do I think about Y?" → consult 04_cognition/
Step 2  For Cognition queries:
        - Find the relevant judgment node(s)
        - Report back: judgment, confidence, evidence (most recent 3-5), falsifier states
        - DO NOT generate a new opinion. Report the existing one.
Step 3  If the user asks something the existing judgments don't cover:
        - Propose creating a new judgment node
        - Help draft initial confidence + falsifiers
        - Wait for user to sign off before creating
```

---

### 🧹 Operation 3 — Lint (weekly, or when triggered)

```
Knowledge layer Lint:
- Orphan pages (no inbound links)
- Contradictory claims between pages
- Stale pages (no update in N months)
- Missing entity pages for entities mentioned

Cognition layer Lint:
- Stale judgments (no evidence appended in N months)
- Judgments with approaching falsifiers not acknowledged by user
- Judgments contradicting each other (cross-reference inconsistency)
- Missing methodology field on Domain/Meta layer nodes
- Evidence chains that point to deleted/moved Knowledge pages
- Escalation candidates: observations with 5+ supporting evidence → propose to graduate to thesis

Output: 06_workbench/synthesis/YYYY-MM-DD_lint.md
```

---

### 🔬 Operation 4 — Falsifier Sweep (daily)

```
For each active judgment node (confidence ≥ 🟡):
  For each falsifier F1...Fn:
    Search recent ingestions (past N days) for evidence that moves the falsifier state:
    - If new evidence supports the falsifier condition → flag "⚠️ approaching trigger"
    - If new evidence is the opposite of the falsifier → mark "⛔ reverse-falsified deepening"
    - If the falsifier condition is met → flag "❌ triggered, requires user review"

Output a brief summary in the daily Synthesis:
  - X judgments touched today
  - Y falsifiers approaching trigger (lists them with one-line context)
  - Z evolution-stage transitions proposed
  - W escalation candidates
```

---

### 🔄 Operation 5 — Feedback Reverse-Update (when user logs feedback)

```
Step 1  User drops a feedback file in 01_drafts/feedback/ describing:
        - What action was taken
        - What judgment drove it
        - What the result was
        - What the user learned
Step 2  Agent reads the feedback
Step 3  Identify which methodology file should be updated:
        - The methodology field of the driving judgment is the primary candidate
        - Propose specific edits to that methodology file
        - Wait for user to sign off
Step 4  After methodology is updated:
        - Scan 04_cognition/ for all nodes whose methodology field references this file
        - Append an evidence entry to each:
          "YYYY-MM-DD [methodology update from feedback X]: <one-line summary of what changed>"
        - Optionally flag those judgments for user review (does the update affect any of them?)
Step 5  Log the reverse-update action in 06_workbench/synthesis/YYYY-MM-DD.md
```

---

## Routing rules — where does a new file go?

| Content type | Destination |
|---|---|
| External fact / data / quotable | `03_knowledge/facts/` |
| Concept definition / abstract idea | `03_knowledge/concepts/` |
| Person / organization / entity | `03_knowledge/entities/` |
| Theoretical framework from external source | `03_knowledge/theories/` |
| Multi-source synthesis (still external view) | `03_knowledge/synthesis/` |
| **Your worldview / belief about the world** | `04_cognition/world/` |
| **Your domain-specific judgment** | `04_cognition/domain/<domain>/` |
| **Belief about yourself / identity / values** | `04_cognition/self/` |
| **Belief about thinking methods / meta-cognition** | `04_cognition/meta/` |
| Active research topic / project workspace | `05_topics/<topic>/` |
| Daily log | `06_workbench/daily/YYYY-MM-DD.md` |
| Decision snapshot (immutable) | `06_workbench/decisions/YYYY-MM-DD-<title>.md` |
| Procedure / protocol / framework you've named | `07_methodology/<domain>/<name>.md` |
| Synthesis / lint / sweep reports | `06_workbench/synthesis/YYYY-MM-DD_<type>.md` |

---

## What's required vs optional

### Required (every session)
- Read SOUL + SCHEMA + Memory at session start
- Maintain `03_knowledge/index.md` and `04_cognition/index.md` current
- Run daily Falsifier Sweep (if scheduled)
- Write Synthesis report at end of every ingest/operation session

### Required (when applicable)
- Reverse-update evidence after methodology updates
- Propose (not execute) confidence changes
- Surface approaching falsifiers to user

### Optional (nice to have)
- Visualization of judgment graph
- Auto-suggest related questions to investigate
- Weekly trend reports across the Cognition Wiki

---

## What NOT to do

❌ Never silently raise/lower confidence — always propose, wait for confirmation
❌ Never delete evidence entries — only append (preserve audit trail)
❌ Never modify falsifier wording without explicit user permission
❌ Never take action on a falsifier trigger — flag it, the user decides
❌ Never decide what counts as "feedback" — wait for user to label
❌ Never write to `06_workbench/decisions/` (those are user-authored snapshots)
❌ Never generate a new opinion when asked "what do I think about X?" — report the existing judgment

---

## Failure modes & recovery

- **Conflict between two judgments**: append a note to both, flag for user attention in next Synthesis. Don't resolve unilaterally.
- **Source contradicts existing Knowledge page**: keep both; mark with `⚠️ contradiction with [other page]`; flag for user.
- **Methodology file linked but doesn't exist**: create a stub; flag for user to fill in.
- **Confidence proposed but user disagrees**: revert proposal; log the disagreement as an evidence entry on the judgment (this is itself signal).

---

## Co-evolution

This protocol is **not fixed**. After each session, if friction arose:
- Update SCHEMA.md with new rules
- Update this AGENT_PROTOCOL.md with new operations or refined existing ones
- Update SOUL.md if the cognitive engine philosophy shifted

**Version this file in git.** Treat protocol drift as a first-class concern.

---

*Version 1.0 · The protocol is a living document. Update it whenever your workflow demands it.*
