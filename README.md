# Cognitive OS

> An engineering system for **judgment**, not knowledge.
>
> 一个为"判断"而设计的工程系统。

If [Andrej Karpathy's LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) is "outsource the bookkeeping of what's true," **Cognitive OS is the layer above it — outsource the bookkeeping of what you believe and why.**

---

## Two surfaces in this repo

| | Where | What |
|---|---|---|
| 🌐 **Showcase site** | [`docs/`](./docs) → [live →](https://funshh.github.io/cognitive-os/) | Bilingual marketing site. The "why" + visual demos. |
| 📦 **Starter pack** | [`starter/`](./starter) (EN) · [`starter/zh/`](./starter/zh) (中文) | Fork-and-go template. The "how" — schema, agent protocol, judgment-node templates. |

Both describe the same pattern. The site is for browsing; the starter is for building.

---

## TL;DR

LLMs commoditize Knowledge. Your edge can't sit on knowledge density — it has to sit on **judgment quality**.

Cognitive OS is a pattern for an LLM-maintained wiki of **judgments**: opinions with structured confidence (🔴/🟡/🟢), evidence trails, falsifier conditions, evolution stages, and feedback-driven updates. The LLM does the maintenance; you do the believing.

90 days running on an investment production line, now extending to content and product. Same engine, different Topics.

---

## Quick start

```bash
git clone https://github.com/FunSHH/cognitive-os.git
cd cognitive-os/starter         # English
# — or —
cd cognitive-os/starter/zh      # 中文
```

Then read the starter's [`cognitive-os.md`](./starter/cognitive-os.md) for the core idea, and follow [`starter/README.md`](./starter/README.md) for setup.

---

## Project structure

```
cognitive-os/
├── README.md              ← you are here
├── LICENSE
├── docs/                  ← GitHub Pages source (the showcase site)
│   ├── index.html         → funshh.github.io/cognitive-os/
│   ├── Demo1-*.html       → 判断生命周期 / Judgment Lifecycle
│   ├── Demo2-*.html       → 判断到决策 / Judgment to Decision
│   ├── Demo3-*.html       → 每日心跳 / Daily Heartbeat
│   ├── themes/            → Investment theme dynamic pages (sample domain)
│   └── en/                → English version of the showcase
└── starter/               ← the fork-and-go template
    ├── README.md
    ├── cognitive-os.md    ← the core idea (read first)
    ├── SCHEMA.md
    ├── AGENT_PROTOCOL.md
    ├── templates/
    └── zh/                ← Chinese mirror of the above
```

---

## Engine vs Production Line

Cognitive OS is **the engine**. Production lines (Invest OS / Content OS / Product OS) are what you build with it.

```
Cognitive OS  →   Topic   →   Production Line
 (this repo)      (engine        (turnkey domain
                   meets          system —
                   your           Invest OS,
                   domain)        Content OS, …)
```

The starter ships the engine. Your Production Line emerges as you accumulate domain-specific Cognition nodes and specialize Methodology over time.

See [`starter/cognitive-os.md`](./starter/cognitive-os.md) § "Engine vs Production Line" for the full architecture.

---

## License

- **Templates and code** → MIT
- **Idea documents** (`cognitive-os.md`, READMEs) → CC BY-NC 4.0

---

## Credits

- **[Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** — for LLM Wiki, which framed the pattern this builds on
- **Vannevar Bush** — for Memex (1945), grandfather of both patterns
- **Karl Popper** — for falsifiability, which turns belief into testable knowledge
- **DIKW & SECI models** — for the layered view of cognition

---

*If you build a version of this for your domain, I'd love to see it. The pattern wants to be instantiated, not gatekept. — Maxwell*
