# Cognitive OS Starter

> 中文版 → [zh/](./zh/)

A starter pack for building **judgment engines** — wikis where the LLM maintains your judgments, not just your knowledge.

If [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) is "outsource the bookkeeping of what's true," **Cognitive OS is "outsource the bookkeeping of what you believe and why."**

---

## What this is

A minimal, opinionated template for an LLM-maintained wiki of **judgments** — opinions with structured confidence, evidence trails, falsifier conditions, and feedback-driven updates. Pointed at the same problem space as LLM Wiki, but one DIKW layer higher: **Wisdom, not Knowledge**.

The core idea is in [`cognitive-os.md`](./cognitive-os.md). Read it first.

---

## Why

LLMs commoditize Knowledge. Your competitive position can't sit on knowledge density. It has to sit on **judgment quality** — and judgment quality compounds only if there's a system that forces frequent, structured forming-and-updating of judgments.

The bookkeeping that kills human wikis (cross-references, falsifier monitoring, evidence trails, methodology updates) is exactly what LLMs are good at. **The cost of maintaining a judgment graph is near zero with an LLM agent.**

---

## Who this is for

- **Investors** — every thesis is a judgment with falsifiers; positions are protocols
- **Researchers** — every hypothesis is a judgment with evidence; replication is verification
- **Product leaders** — every roadmap bet is a judgment; user feedback is the falsifier sweep
- **Policy analysts** — every recommendation is a judgment with explicit assumptions
- **Founders** — every strategic call is a judgment; revenue / churn are the methodology updates
- **Anyone whose work involves making calls and being right matters**

This is *not* for: knowledge collectors who just want to remember more (use LLM Wiki). Casual journaling (use any note app). Pure creative writing (use whatever helps you flow).

---

## Engine vs Production Line

Cognitive OS is **the engine, not a turnkey domain system**.

You may see references to "Invest OS", "Content OS", or "Product OS" in adjacent work. Those are **production lines** — full execution systems for a specific domain (investment / content / product), built *on top of* Cognitive OS with domain-specific Topics, methodologies, schedules, and dashboards.

This starter ships the engine. You — with your LLM agent — grow the production line.

```
Cognitive OS  →   Topic   →   Production Line
 (engine,         (engine        (turnkey domain
  this repo)       meets          system —
                   your           Invest OS,
                   domain)        Content OS, …)
```

The starter is intentionally domain-agnostic. Templates show structure, not content. The moment you instantiate it against your real domain, you start growing your own Topic. After a few months of daily heartbeat runs, the Topic has accumulated enough domain-specific Methodology that it crystallizes into a Production Line. **Same engine, different Topics.**

---

## What's in the starter pack

```
cognitive-os-starter/
├── README.md                    ← you are here
├── cognitive-os.md              ← the core idea (the "why" — read first)
├── SCHEMA.md                    ← the configuration file your LLM reads at every session
├── AGENT_PROTOCOL.md            ← the operating protocol — what the LLM does, when
└── templates/                   ← markdown templates
    ├── judgment-node.md         ← schema for a single judgment
    ├── daily-synthesis.md       ← what the LLM writes back after a daily run
    ├── feedback.md              ← how you log feedback after actions
    └── lint-report.md           ← weekly health check template
```

The starter pack is **deliberately minimal**. You fork it, hand it to your LLM agent, and co-design the instantiation that fits your domain.

---

## How to use it

### Step 1 — Read [`cognitive-os.md`](./cognitive-os.md)

Don't skip. This explains the pattern. Without internalizing why, the templates will feel arbitrary.

### Step 2 — Copy this folder into your knowledge directory

Suggested: a new directory next to where you keep notes. Don't merge into an existing vault yet — start clean, see if the pattern works for you.

```bash
# Clone the whole repo (the starter is one folder inside it):
git clone https://github.com/FunSHH/cognitive-os.git
cd cognitive-os/starter

# — or — download just the zip from GitHub and extract the starter/ folder.
```

### Step 3 — Open it with your LLM agent

Claude Code / Cowork / Cursor / Codex / OpenAI Agent — any LLM that can read files and edit them. Tell it:

> "Read `cognitive-os.md` and `SCHEMA.md`. From now on, treat this directory as a Cognitive OS vault. Follow the operating protocol in `AGENT_PROTOCOL.md`. Help me adapt the schema to my domain."

### Step 4 — Co-evolve the schema for your domain

The schema in this starter is generic. You'll need to:
- Decide your domain naming (investment / research / etc.)
- Decide your evolution-stage taxonomy
- Decide your falsifier naming convention
- Decide what counts as 🔴 vs 🟡 vs 🟢 confidence
- Decide your daily / weekly maintenance protocols

Don't try to perfect it. Each session you'll discover "the LLM did X but should have done Y" — write the rule into the schema, it follows next time.

### Step 5 — Start with one judgment

Don't try to populate a whole vault. Take one current call you're making (an investment thesis, a hypothesis, a product bet). Use `templates/judgment-node.md` to create the first judgment node. Let the LLM help you fill in evidence, falsifiers, methodology link.

After a week, you'll have a feel for whether the pattern fits. After a month, you'll have ~10 judgment nodes and the schema will be customized to you.

### Step 6 — Add a daily sweep

Once you have ≥5 active judgments, schedule a daily run (cron / GitHub Action / your agent's scheduled task). The agent scans all judgments, reports approaching falsifiers, flags stale nodes, suggests confidence updates. You spend 5 minutes reading the report.

This is when the system starts feeling alive instead of being yet-another-note-folder.

---

## Differences from LLM Wiki

If you've read Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), here's the diff:

| | LLM Wiki | Cognitive OS |
|---|---|---|
| Goal | Knowledge accumulation | **Judgment accumulation** |
| Wiki content | Entity pages, concept pages, syntheses | **Judgment nodes with confidence + falsifiers** |
| Architecture | Raw + Wiki + Schema | Raw + Knowledge + **Cognition** + Methodology |
| Operations | Ingest / Query / Lint | + **Falsifier Sweep** + **Feedback Reverse-Update** |
| Schema file | CLAUDE.md / AGENTS.md | SCHEMA.md + AGENT_PROTOCOL.md |
| LLM Wiki built? | Yes, optional layer here | Yes — use LLM Wiki as your Knowledge layer underneath |

**Cognitive OS sits on top of LLM Wiki.** You can have both. The Knowledge Wiki is upstream; the Cognition Wiki is where *your* judgments live. Evidence in a judgment node cites Knowledge Wiki pages.

---

## Stability & maturity

🟡 **Pre-1.0.** Pattern is fully working in one production vault (a personal investment / research / product operation, ~8 months runtime, ~100 judgment nodes, ~22 active themes). Schema and protocol templates here are extracted and anonymized from that vault.

The pattern is stable. The templates will evolve as more domains try it.

---

## Examples in the wild

If you build a Cognitive OS instantiation for your domain, **open a PR or issue** with a link to your fork. The pattern wants to be instantiated, not gatekept.

Current known instantiations:
- Investment thesis tracking (~22 themes, ~100 judgments, ~8 months) — the source vault for this starter

---

## License

MIT for the templates and code. CC BY-NC 4.0 for the idea documents.

External references (LLM Wiki, DIKW model, SECI model, Memex, Popper's falsifiability) are credited inline.

---

## Credits

- **Andrej Karpathy** — [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), which framed the pattern this extends
- **Vannevar Bush** — Memex (1945), grandfather of both patterns
- **Karl Popper** — falsifiability, which is what turns belief into testable knowledge
- **DIKW & SECI models** — for the layered view of cognition

---

*Cognitive OS is itself a Cognitive OS. The whole starter pack — including this README — was authored as judgment nodes in a real vault, then exported. It eats its own dog food.*
