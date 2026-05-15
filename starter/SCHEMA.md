# SCHEMA.md

> **For your LLM agent to read at the start of every session.**
> This is the configuration that turns a generic LLM into a disciplined Cognitive OS maintainer.
> Co-evolve this file with your agent over time.

---

## 1. Vault structure

```
your-vault/
├── _system/
│   ├── SOUL.md                 ← Agent role + cognitive engine philosophy
│   ├── SCHEMA.md               ← this file
│   └── AGENT_PROTOCOL.md       ← operating protocol
├── 00_inbox/                   ← raw inputs not yet processed
├── 01_drafts/                  ← thoughts in progress
│   └── feedback/               ← feedback files for reverse-update
├── 02_memory/                  ← high-compression background (LLM reads at session start)
├── 03_knowledge/               ← LLM Wiki layer: external facts
│   ├── entities/
│   ├── concepts/
│   ├── theories/
│   ├── facts/
│   └── index.md                ← Knowledge layer index
├── 04_cognition/               ← ★ Cognition Wiki: YOUR judgments
│   ├── world/                  ← judgments about the external world
│   ├── domain/                 ← judgments about your specific domain
│   ├── self/                   ← judgments about yourself (values, principles)
│   ├── meta/                   ← judgments about thinking methods
│   └── index.md                ← Cognition layer index
├── 05_topics/                  ← topic-level workspaces (apply methodology to specific domains)
├── 06_workbench/               ← daily / weekly / decision logs
│   ├── daily/
│   ├── weekly/
│   ├── synthesis/              ← LLM's reports back to you
│   └── decisions/              ← decision snapshots (immutable)
└── 07_methodology/             ← procedural knowledge: protocols you've signed
```

---

## 2. Judgment node front-matter (required fields)

Every file in `04_cognition/` MUST have this YAML front-matter:

```yaml
---
type: cognition
domain: [your domain — investment | research | product | policy | etc.]
layer: [worldview | theory | framework | thesis | observation]
confidence: 🔴 0.xx | 🟡 0.xx | 🟢 0.xx
created: YYYY-MM-DD
updated: YYYY-MM-DD
evidence:
  - YYYY-MM-DD [source page link]: one-line summary
falsifiers:
  - F1: [condition that would invalidate this judgment, one sentence]
  - F2: [...]
  - F3: [...]
methodology: "[[link to methodology file]]"   # required for Domain/Meta layers
tags: [tag1, tag2]
---
```

### Confidence semantics

- **🔴 0.30 – 0.50** = initial guess / intuition / one-source observation. **Not yet a judgment, more a hypothesis.** Falsifiers exist but haven't been actively monitored.
- **🟡 0.50 – 0.75** = verified by multiple independent sources, no falsifier has triggered. **Forming opinion.** Worth tracking but not yet acting on.
- **🟢 0.75 – 0.95** = stable, multiple convergent evidence, key falsifiers tested and held. **Actionable judgment.** Can drive protocols.

Confidence is **co-evolved**. The LLM suggests; you confirm. The LLM never silently raises confidence — it only proposes, you sign.

### Layer semantics

- **worldview** — broad belief about how some part of the world works ("Higher-for-longer is structural, not cyclical")
- **theory** — analytical framework you'd apply repeatedly ("The yield curve has three layers, each driven by different forces")
- **framework** — a structured approach to a class of problems ("Six-layer investment analysis: mechanism → narrative → transmission → fundamentals → pricing → allocation")
- **thesis** — specific actionable judgment about a specific topic ("Domain X is in late accelerating stage")
- **observation** — single data-point judgment, often graduated to theory over time

---

## 3. Falsifier naming convention

Falsifiers are named **F1, F2, F3...** within a judgment node.

For node-level subscoping (e.g., a thesis with multiple sub-judgments), use **F-Xn** where X is a one-letter prefix (capitalized first letter of the sub-entity) and n is the sequence:
- A thesis on Entity ABC → falsifiers can be F-A1, F-A2
- A thesis on Entity XYZ → F-X1, F-X2

Each falsifier MUST be:
- **One sentence** (forces clarity)
- **Observable** (you'd know it if it happened)
- **Distinct from other falsifiers** (no overlap)

**State of each falsifier** (the LLM tracks this):
- `🟢 not triggered` — no evidence approaching this condition
- `⚠️ approaching trigger` — recent evidence moving toward this condition
- `⛔ reverse-falsified deepening` — opposite of falsifier is being confirmed (judgment getting stronger)
- `❌ triggered` — falsifier condition met; judgment needs reconsideration

---

## 4. Evolution stage taxonomy

For judgments about phenomena that evolve over time, tag with:

| Stage | Symbol | Meaning |
|---|---|---|
| 萌芽 / Emerging | E | Early signals; mostly speculation |
| 加速 / Accelerating | A | Clear evidence of phenomenon; gaining steam |
| 制度化 / Institutionalizing | S- | Phenomenon being formalized / accepted |
| 拥挤 / Crowded | S+ | Consensus reached; little surprise remaining |
| 退潮 / Fading | B- | Reversal beginning; consensus unraveling |

Your domain may use different taxonomy — define it here.

---

## 5. Methodology field

Every Domain and Meta layer judgment MUST have a `methodology` field pointing to a procedural file in `07_methodology/`.

When that methodology file is updated (because feedback showed it failed), the LLM scans this field across all judgments and **appends an evidence entry to each** matching one:

```yaml
evidence:
  - 2026-XX-XX [methodology update from feedback Y]: methodology revised; check if this judgment still holds
```

This is the **Feedback Reverse-Update** operation.

---

## 6. Indexing files (per LLM Wiki convention)

- `03_knowledge/index.md` — content catalog for the Knowledge layer
- `04_cognition/index.md` — content catalog for the Cognition layer, grouped by domain/layer
- `06_workbench/synthesis/log.md` — chronological log of every ingest / synthesis / lint pass

Each index entry should include: page link, one-line summary, last-updated date, and (for Cognition) current confidence.

---

## 7. What the LLM should NOT do silently

- ❌ Never raise confidence without proposing it to you first
- ❌ Never modify a judgment's `falsifiers` list (you wrote them; you change them)
- ❌ Never delete evidence (only append; ensure full audit trail)
- ❌ Never act on a falsifier trigger — flag it for your review
- ❌ Never decide what counts as "feedback" — wait for you to mark a file as feedback
- ❌ Never write to `06_workbench/decisions/` directly — those are your authored snapshots

---

## 8. What the LLM SHOULD do without asking

- ✅ Append evidence to a judgment node when a new ingestion clearly touches it
- ✅ Update evolution-stage field when evidence supports a transition (with one-line note in evidence)
- ✅ Write daily Synthesis reports summarizing all changes in the past 24 hours
- ✅ Run weekly Lint and produce a report
- ✅ Run daily Falsifier Sweep and flag approaching triggers
- ✅ Reverse-update evidence when a methodology file is updated
- ✅ Maintain `index.md` files current at all times
- ✅ Cross-reference: when a new judgment is created, scan for related judgments and add bidirectional links

---

## 9. Customization checklist

Before running this with your LLM, customize:

- [ ] Domain values (replace "investment / research / etc." with what you actually do)
- [ ] Layer taxonomy (extend or simplify the worldview/theory/framework/thesis split)
- [ ] Confidence thresholds (your 0.50 may be different from someone else's)
- [ ] Evolution stage names (Chinese / English / domain-specific)
- [ ] Falsifier prefix convention (e.g., if you do investing, F-Xn for stock-thesis layer)
- [ ] Daily / weekly task schedules
- [ ] Inbox routing rules

When in doubt: do not optimize upfront. Let the schema accrete from real friction during the first month.

---

*Version 1.0 · Co-evolve this with your LLM in every session that produces friction.*
