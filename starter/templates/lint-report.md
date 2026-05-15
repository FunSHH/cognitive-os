---
type: synthesis-lint
date: YYYY-MM-DD
scope: [knowledge-only | cognition-only | both]
trigger: [scheduled-weekly | manual]
---

# Lint Report · YYYY-MM-DD

> Weekly health check across the vault.
> Run by the agent. Reviewed by the user in ~30 minutes.

---

## Layer 1 · System consistency

> Is the schema being followed? Are the indices current?

- [ ] `03_knowledge/index.md` current with all Knowledge pages
- [ ] `04_cognition/index.md` current with all judgment nodes
- [ ] All judgment nodes have required schema fields (type/domain/layer/confidence/evidence/falsifiers)
- [ ] All Domain/Meta layer nodes have `methodology` field filled
- [ ] No orphan files (pages with no inbound link)

**Issues found:**
- [List any]

---

## Layer 2 · Knowledge Wiki health

### Stale pages
> No update in 6+ months. May or may not be a problem.

- [[Page A]] — last updated YYYY-MM-DD

### Contradictions across pages
> Different pages making opposite claims.

- [[Page X]] says "..." but [[Page Y]] says "...". Recommend: reconciliation or explicit comparison page.

### Missing entities / concepts
> Mentioned across multiple pages but no dedicated page exists yet.

- "X" — mentioned in 5+ pages, no entity page

### Broken evidence links
> Knowledge pages referenced in Cognition `evidence:` fields that have moved/deleted.

- [...]

---

## Layer 3 · Cognition Wiki health

### Stale judgments
> No new evidence in N+ months. Possible failure modes: not relevant anymore / system not noticing relevant signals / domain inactive.

- [[Judgment A]] — last evidence YYYY-MM-DD (X months ago)

### Approaching falsifiers — not yet acknowledged
> Falsifiers in `⚠️ approaching trigger` state for >2 weeks without user review.

- [[Judgment B]] · F2 — approaching since YYYY-MM-DD. **User action recommended.**

### Triggered falsifiers — not yet acted upon
> Falsifiers fully triggered (`❌`) without confidence downgrade or judgment revision.

- [[Judgment C]] · F4 — triggered YYYY-MM-DD. **Confidence should be reviewed urgently.**

### Contradictory judgments
> Two judgments making opposite claims.

- [[Judgment X]] and [[Judgment Y]] appear to contradict. Recommend: resolve, merge, or explicitly note the disagreement.

### Missing methodology fields
> Domain/Meta layer nodes that should have `methodology` link but don't.

- [...]

### Escalation candidates
> Observations with 5+ evidence entries that should be promoted to thesis.

- [[Observation O1]] — N evidence entries; promote?

---

## Layer 4 · Methodology Library health

### Methodologies referenced but missing
> `methodology:` field points to non-existent file.

- [...]

### Methodologies updated recently — reverse-update audit
> When methodology X was updated, did the reverse-update fire?

- [[Methodology M]] updated YYYY-MM-DD. Linked judgments: N. Evidence appended: should be N.

### Stale methodologies
> No update in 12+ months. Likely fine, but worth a glance.

- [...]

---

## Layer 5 · Coverage gaps

### Topics referenced but undefined
> Topics mentioned in judgments / workbench but no topic workspace exists.

- "..." — mentioned 3+ times, no `05_topics/<name>/` exists

### Domains where activity is high but judgment density is low
> Lots of ingestions, few judgments. Possibly: lots of inputs without forming opinions. Worth reflection.

- Domain X: N ingestions, only M judgments

---

## Action items

> User to acknowledge or address:

- [ ] Review approaching falsifiers (see above)
- [ ] Confirm or override escalation candidates
- [ ] Resolve contradictory judgment pair
- [ ] Fill missing methodology links

---

## Summary stats

- Knowledge pages: N
- Cognition nodes: M (🔴 X / 🟡 Y / 🟢 Z)
- Active topics: K
- Falsifiers approaching trigger: W
- Stale judgments: Q
- Days since last Lint: D

---

*Lint is the anti-entropy operation. Without it, the wiki silently rots. With it, the wiki stays alive.*
