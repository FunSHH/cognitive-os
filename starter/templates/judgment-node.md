---
type: cognition
domain: [your-domain]                    # investment / research / product / policy / ...
layer: [worldview|theory|framework|thesis|observation]
confidence: 🔴 0.40                       # 🔴 0.30-0.50 | 🟡 0.50-0.75 | 🟢 0.75-0.95
created: YYYY-MM-DD
updated: YYYY-MM-DD
evolution-stage: [optional — 萌芽 E / 加速 A / 制度化 S- / 拥挤 S+ / 退潮 B-]
evidence:
  - YYYY-MM-DD [[link to 03_knowledge/page]]: one-line summary
falsifiers:
  - F1: [condition that would invalidate this judgment, one sentence]
  - F2: [...]
  - F3: [...]
methodology: "[[link to 07_methodology/relevant-file]]"   # required for Domain/Meta layers
tags: [tag1, tag2]
related:
  - "[[link to other judgment node]]"
---

# [Judgment Title — one short, declarative sentence]

> **Core claim:** [State the judgment in one sentence. Make it falsifiable.]

---

## Why this is the judgment

[2-3 paragraphs explaining what you believe and why. Cite Knowledge Wiki pages.]

[Be specific about what you're claiming and what you're NOT claiming. The boundary matters.]

---

## What would change my mind

The `falsifiers` field above lists the conditions that, if observed, would invalidate this judgment. Expanded:

- **F1**: [Brief expansion — what data would I need to see, in what magnitude, to acknowledge this?]
- **F2**: [Same]
- **F3**: [Same]

These are not vague concerns. They are **specific, observable, named conditions**. When new evidence comes in, the LLM checks whether it moves any falsifier closer to trigger.

---

## Current state

- **Confidence**: 🔴 0.40 — initial guess based on N sources
- **Evolution stage**: [if applicable — where in the lifecycle is the underlying phenomenon?]
- **Last reviewed**: YYYY-MM-DD

---

## Methodology

This judgment relies on / will be tested by procedures in:
- [[link to methodology file 1]]
- [[link to methodology file 2]]

If those methodology files are updated (due to feedback), this judgment's evidence list should be reverse-updated automatically.

---

## Related judgments

- [[neighbor judgment 1]] — relationship: [supporting / conflicting / parallel]
- [[neighbor judgment 2]] — relationship: [...]

---

## History

> Append-only log of significant changes. Do not edit existing entries.

- **YYYY-MM-DD** — node created. Initial confidence 🔴 0.40. Falsifiers F1/F2/F3 defined.

---

*Edit confidence ONLY after the agent proposes it. Edit falsifiers ONLY with deliberate intention. Append evidence freely.*
