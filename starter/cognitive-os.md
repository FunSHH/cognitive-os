# Cognitive OS

A pattern for building **judgment engines** using LLMs.

This is an idea file. Copy-paste it to your own LLM Agent (Claude Code, OpenAI Codex, Cowork, Cursor, etc.). Its goal is to communicate the high-level pattern — your agent will help you build out the specifics in collaboration.

It is related in spirit to Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), but pointed at a different problem: **LLM Wiki helps you accumulate knowledge; Cognitive OS helps you accumulate judgment**.

---

## The core idea

LLM Wiki is brilliant for the **Knowledge layer** (DIKW: Data → Information → Knowledge → Wisdom). It solves the maintenance burden so that "knowledge accumulates" instead of getting re-derived on every query.

But for any knowledge worker who has to **make calls** — investors, researchers, product decision-makers, policy analysts, founders — Knowledge isn't the bottleneck. **Judgment is.** The same set of facts produces different decisions in different hands, and the difference is the **structure** of how the person's judgment is formed, verified, falsified, and updated.

Knowledge gets cheaper every year — LLMs are proof. **Judgment is the scarce thing**: opinions backed by confidence levels, falsifier conditions, evidence trails, and protocols for what to do when conditions are met.

LLMs don't naturally build judgment — they smooth over it. Asked a question, they give you an answer with no confidence, no falsifier, no commitment about what would change their mind. **A LLM Wiki tells you what the sources say; a Cognitive OS tells you what *you* believe, how strongly, and what would change your mind.**

The core idea: **build a wiki of judgments, not just knowledge.** Each judgment is a markdown file with structured metadata — domain, layer, confidence, evidence list, falsifier conditions, evolution stage, methodology link. The LLM maintains this judgment graph the same way LLM Wiki maintains the knowledge graph — except now it's tracking your *opinions* and what changes them, not just facts.

This is the key difference: **the wiki is a persistent, compounding artifact of how you think.** Not what you've read, but what you've concluded. Not what's true in general, but what you're betting on right now, with what confidence, against what falsifiers.

You never (rarely) write the maintenance — the LLM writes and maintains all of it. You're in charge of the judgment itself: forming opinions, accepting evidence, signing protocols. The LLM does the bookkeeping: cross-referencing, falsifier monitoring, evidence appending, status transitions, feedback reverse-routing.

---

## Architecture

Four layers (vs LLM Wiki's three):

**Raw sources** — your curated collection of source documents. Articles, papers, market data, podcast notes, your own drafts. Immutable. The LLM reads from them but never modifies them.

**Knowledge Wiki** — LLM-generated wiki pages summarizing external facts: entities, concepts, theories, books, comparisons, syntheses. This is the *LLM Wiki layer* — Karpathy's domain. It's about what's true in the world, regardless of who reads it.

**Cognition Wiki** ★ — this is the new layer. LLM-maintained markdown files representing *your* judgments. Each node carries:
- `domain` — what area (investment / research / product / policy / etc.)
- `layer` — what type (worldview / theory / framework / thesis / observation)
- `confidence` — 🔴 (initial guess) / 🟡 (verified) / 🟢 (stable)
- `evidence` — timestamped list, each entry pointing back to a Knowledge Wiki page
- `falsifiers` — conditions that would invalidate this judgment, named like F1/F2/F3
- `evolution-stage` — where in the lifecycle this judgment-relevant phenomenon sits (emerging / accelerating / institutionalizing / crowded / fading)
- `methodology` — link to the procedural file that should be updated when this judgment is wrong

**Methodology Library** — procedural knowledge: how you make decisions in this domain, what protocols you've named, what frameworks you apply. These are *programs that judgment nodes call*. When feedback shows a protocol failed, the methodology updates and the change reverse-propagates evidence to all judgment nodes that reference it.

The four layers together make a **graph that thinks about itself**:
- Raw flows into Knowledge.
- Knowledge feeds Cognition (each judgment cites Knowledge pages).
- Cognition fires Methodology (judgments invoke protocols).
- Methodology, when updated by feedback, reverse-propagates back to Cognition.

---

## The five operations

LLM Wiki has three operations (Ingest / Query / Lint). Cognitive OS adds two more focused on judgment:

**1. Ingest** — same as LLM Wiki. A new source enters; the LLM writes a Knowledge summary, updates entity pages, notes contradictions. *Plus*: if the source touches an existing judgment, the LLM appends a one-line evidence entry to that judgment's `evidence` list, marks the relevant `falsifier` as supported / approaching trigger / fully triggered, and updates `confidence` (with your confirmation).

**2. Query** — same as LLM Wiki. Ask a question; the LLM consults Knowledge + Cognition pages. *Plus*: when you ask "what do I think about X?", the LLM specifically reads the Cognition Wiki for X — not generates a new answer — and gives you back **your past judgment with confidence and falsifier status**.

**3. Lint** — same as LLM Wiki, with two layers added:
- *Knowledge layer Lint*: contradictions, orphan pages, missing entities (same as LLM Wiki).
- *Cognition layer Lint*: judgments that haven't been touched in N months (stale), judgments whose falsifiers have approached trigger but you haven't acknowledged, judgments contradicting each other, missing methodology field, evidence chain broken.

**4. Falsifier Sweep ★** — new. Periodically (daily or weekly), scan all active judgment nodes and check whether the world has moved closer to any of their falsifiers. The LLM reports: "F2 of judgment X has had +3 reinforcing data points since you last looked; F4 of judgment Y now meets quantitative threshold; consider re-confirming or downgrading confidence." This is the heartbeat that keeps the judgment graph alive instead of silently rotting.

**5. Feedback Reverse-Update ★** — new. When a judgment leads to action, and the action produces a result (good or bad), the result becomes a feedback file. The LLM ingests the feedback, updates the Methodology library, and then **reverse-propagates** the update: scan all Cognition nodes that link to the updated methodology, append an evidence entry to each. This closes the loop: judgment → action → result → methodology update → all related judgments learn from it.

---

## Schema (the most important file)

`SCHEMA.md` is to Cognitive OS what `CLAUDE.md` is to LLM Wiki: the configuration that turns the LLM into a disciplined judgment-engine maintainer rather than a generic chatbot.

The schema should define:

- **Judgment node front-matter fields** (and which are required vs optional)
- **Confidence semantics** — what makes a judgment 🔴 vs 🟡 vs 🟢
- **Falsifier naming convention** — e.g. `F1`, `F2`, with one-sentence falsifying condition each
- **Evolution-stage taxonomy** — what stages your domain has (the LLM can default to "萌芽 / 加速 / 稳定 / 拥挤 / 退潮" or any other curve)
- **Methodology reverse-update rules** — when methodology X is updated, which judgments get evidence appended automatically
- **Cross-link conventions** — how `evidence` entries reference Knowledge pages, how `methodology` field references Methodology files
- **Daily / weekly maintenance protocols** — what the LLM should do without asking
- **Ingestion routing** — for a new source, where does it go (Knowledge only? Trigger a judgment? Start a new topic?)

The schema is **co-evolved with your LLM**. You don't write it perfectly upfront. Each session, you'll notice "the LLM did X but should have done Y" — write the rule into the schema, the LLM follows it next time. After a few weeks the schema reflects your actual workflow.

---

## Why this matters

**Knowledge worker → Judgment worker.** The thing that distinguishes a senior analyst from a junior one isn't how many facts they remember — it's the quality, calibration, and update-discipline of their judgments. Same for investors, researchers, product leaders. **Judgment is the asset; knowledge is the input.**

**LLMs are commoditizing Knowledge.** Ten years from now, every fact you carry around in your head will be one prompt away from anyone. Your competitive position can't sit on knowledge density. It has to sit on **judgment quality** — and judgment quality compounds only if there's a system that forces frequent, structured forming-and-updating of judgments.

**The bookkeeping is the bottleneck.** Forming a good judgment is easy on day one — you read something, you have an opinion. Maintaining a good judgment over 90 days, while new evidence trickles in and old assumptions decay, while you make twelve other judgments in adjacent areas, while world conditions shift — that's where humans abandon. The wiki dies because the maintenance overwhelms the value.

**LLMs are perfect for this maintenance.** They don't get bored. They don't forget to update a falsifier. They can touch 15 judgment nodes in one pass when a new data point arrives. They can run a falsifier sweep at 8am every day without prompting. **The cost of maintaining a judgment graph is near zero with an LLM agent.**

**What remains is the human part.** You decide what to believe, how strongly, and what would change your mind. You sign the protocols. You take the action. The LLM does everything else.

This is the inverse of "AI as content accelerator." It's AI as **judgment-engine maintainer**.

---

## Workflows

### Workflow A: New source enters

1. You drop an article / data point / podcast note into Raw.
2. Tell the LLM: "ingest this."
3. LLM reads, writes a Knowledge summary page, updates entity pages.
4. LLM also scans the Cognition Wiki: does this source touch any active judgment?
5. For each touched judgment: append evidence (with timestamp + one-line summary), evaluate falsifier states, suggest confidence update.
6. LLM presents you with a brief Synthesis: "Today this source touched 3 judgments. Judgment A: F2 now in 'approaching trigger' state. Judgment B: evidence appended. Judgment C: confidence suggested 🟡 → 🟢; confirm?"
7. You confirm or override.

### Workflow B: Daily falsifier sweep

1. Every morning (scheduled task), LLM scans all active judgment nodes.
2. For each: check if any falsifier condition has moved meaningfully closer to trigger based on recent ingestions.
3. Output a daily Synthesis report: "5 judgments touched this week, 2 falsifiers approaching trigger, 1 evolution-stage transition suggested, 3 stale judgments need review."
4. You spend 5 minutes reading. You're done. The graph stays alive.

### Workflow C: Forming a new judgment

1. After reading something, you have an opinion.
2. Tell the LLM: "create a judgment node for X. My view is Y. I'm uncertain because Z. The way I'd know I'm wrong is W."
3. LLM creates the node with `confidence: 🔴`, sets up `falsifiers` based on W, links to relevant Knowledge pages, registers it in `index.md`.
4. From this moment, every new ingestion will check whether to touch this judgment.

### Workflow D: Feedback after action

1. You took an action based on a judgment. Some time later, you have a result (right / wrong / mixed).
2. Tell the LLM: "ingest this feedback for judgment X."
3. LLM writes a feedback file describing what happened and why.
4. LLM identifies which Methodology file should be updated. (E.g., "your protocol said X; the result suggests protocol should also handle Y.")
5. LLM updates the Methodology file.
6. LLM reverse-propagates: scan all judgment nodes whose `methodology` field references the updated file. Append an evidence entry to each: "[date] Methodology updated based on feedback from judgment X."
7. Now every related judgment knows the methodology has evolved. Same lesson, learned once, applied everywhere.

### Workflow E: Weekly Lint

1. Friday afternoon, run Lint.
2. LLM scans both Knowledge layer (orphan pages, contradictions) and Cognition layer (stale judgments, broken evidence chains, approaching falsifiers not acknowledged, missing schema fields, escalation candidates).
3. Output a Lint report.
4. Spend 30 minutes acknowledging or fixing.

---

## Tools / minimum setup

You need very little:

- A directory of markdown files. Obsidian, Logseq, or just a folder of `.md` files works.
- An LLM agent (Claude Code, Cowork, Codex, Cursor) configured to read your `SCHEMA.md` at session start.
- Optionally: a scheduled task / cron / GitHub Action that triggers the Daily Falsifier Sweep automatically.

That's it. No databases, no embeddings, no vector store, no special infra. The wiki *is* the codebase. Git for version history. Done.

---

## Differences from LLM Wiki — explicit

| Dimension | LLM Wiki | Cognitive OS |
|---|---|---|
| **Layer** | Knowledge (DIKW level 3) | Wisdom (DIKW level 4) |
| **Output** | Wiki pages — entity / concept / theory / synthesis | Judgment nodes — opinions with confidence, evidence, falsifiers |
| **Architecture** | Raw + Wiki + Schema (3 layers) | Raw + Knowledge + **Cognition** + Methodology (4 layers) |
| **Operations** | Ingest / Query / Lint | + **Falsifier Sweep** + **Feedback Reverse-Update** |
| **What the LLM tracks** | What's true / what sources say | What *you* believe, how strongly, what changes your mind |
| **Terminal validation** | None (knowledge is judged by internal consistency) | Action → result → methodology update → all related judgments learn |
| **Compounding object** | Knowledge density | Judgment quality |
| **Subject** | Implicit (you're the reader) | **Explicit** — falsifiers are *yours*, protocols are *yours*, feedback is *yours* |

LLM Wiki is the right answer for "I want to learn deeply about a topic." Cognitive OS is the right answer for "I need to make calls in this domain repeatedly over years and want my judgment to compound."

---

## Engine vs Production Line

Cognitive OS is **the engine**. Production lines are what you build with it.

The architecture has three vertical bands:

1. **Cognitive OS (engine)** — generic layers: Inbox, Drafts, Memory, Knowledge, Cognition, and the generic parts of Methodology. Domain-agnostic. This starter pack ships this band.

2. **Topic** — the integration point where the engine meets a specific domain. A Topic is *not* just "Cognition expanded into a domain." The more accurate formula is:

   ```
   Topic = Σ(Cognition nodes for the domain)
         × (Methodology specialized for the domain)
   ```

   Cognition nodes for that domain accumulate over time. Methodology specializes (an investment Topic acquires a `spike-pause-buy-in` protocol; a content Topic acquires a `card-distillation` pipeline). The Topic is the join.

3. **Production Line** — a fully-instantiated Topic with daily heartbeat schedules, dashboards, domain-specific protocols, and feedback loops tied to real-world outcomes (P&L for investment, engagement for content, metric movement for product). Production lines are domain-complete systems: Invest OS, Content OS, Product OS, Research OS.

The starter ships only band 1. Bands 2 and 3 are what you grow.

**Why this distinction matters.** Most readers coming from LLM Wiki or generic note-taking tools assume "OS = full app." Cognitive OS is closer to a generic *operating system* — what it does is run *your* Topics. The same engine can simultaneously run an investment production line and a content production line, sharing the same Knowledge / Cognition graph and the same feedback discipline. **Same engine, different Topics.**

---

## Starter pack

This repository contains:

- `cognitive-os.md` — this document (the core idea)
- `SCHEMA.md` — example schema definition for a Cognitive OS vault
- `AGENT_PROTOCOL.md` — example agent operation protocol
- `templates/` — markdown templates for judgment nodes, dashboards, feedback files, synthesis reports
- `examples/` — anonymized examples of mature judgment nodes in different domains

The starter pack is **deliberately minimal**. You should fork it, hand it to your LLM agent, and co-design the version that fits your domain. Investment, research, product, policy, hobby — the abstraction is the same, the schema is yours.

---

## A note on style

This document is intentionally abstract. It describes a pattern, not an implementation. The exact directory structure, the schema fields, the falsifier naming, the page formats — all of that depends on your domain, your habits, and your LLM of choice. The right way to use this is to share it with your LLM agent and **co-evolve** an instantiation that fits.

If LLM Wiki is "outsource the bookkeeping of what's true," Cognitive OS is **"outsource the bookkeeping of what you believe and why."** The thing you keep is the believing itself. The thing you outsource is the maintenance.

---

## Credits

- Andrej Karpathy — for [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), which framed the pattern this builds on.
- Vannevar Bush — for Memex (1945), which both LLM Wiki and Cognitive OS extend.
- Karl Popper — for falsifiability as the criterion that turns belief into knowledge.
- DIKW model, SECI model — for the layered view of cognition that makes the distinction between Knowledge and Wisdom precise.

---

*If you build a version of this for your domain, I'd love to see it. The pattern wants to be instantiated, not gatekept.*
