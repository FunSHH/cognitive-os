# 认知引擎 · Cognitive OS

> 一个为「**判断**」而设计的工程系统 —— 不是为「知识」。
>
> An engineering system for **judgment**, not knowledge.

[English version →](./README.md)

如果 [Karpathy 的 LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 是"把'事实是什么'的 bookkeeping 外包给 LLM"，**认知引擎就是它的上一层 —— "把'你相信什么、为什么、什么会让你改观'的 bookkeeping 外包给 LLM"。**

---

## 仓库里的两个表面

| | 在哪 | 是什么 |
|---|---|---|
| 🌐 **展示网站** | [`docs/`](./docs) → [在线访问 →](https://funshh.github.io/cognitive-os/) | 双语 marketing 网站。讲"为什么" + 可视化 Demo。 |
| 📦 **Starter 包** | [`starter/`](./starter)（英文） · [`starter/zh/`](./starter/zh)（中文） | Fork-and-go 模板。讲"怎么做" —— schema、agent 协议、判断节点模板。 |

两份都是同一套范式。网站用来浏览；starter 用来真正搭建。

---

## TL;DR

LLM 正在让 Knowledge 商品化。你的竞争优势不能再坐在"知识密度"上，它必须坐在 **判断质量**上。

认知引擎是一个用 LLM 维护**判断 wiki**的范式：每个判断节点带结构化的置信度（🔴/🟡/🟢）、证据链、证伪条件、演化阶段、反馈回归。**LLM 做维护工作，你做相信这件事本身。**

90 天实战跑了一条投资判断流水线，最近开始扩展到内容创作和产品开发 —— 同一台引擎，不同的 Topic。

---

## 快速上手

```bash
git clone https://github.com/FunSHH/cognitive-os.git
cd cognitive-os/starter/zh      # 中文版
# — 或者 —
cd cognitive-os/starter         # English version
```

然后从 [`starter/zh/cognitive-os.md`](./starter/zh/cognitive-os.md) 读起 —— 这是核心思想。再按 [`starter/zh/README.md`](./starter/zh/README.md) 一步一步搭起来。

---

## 项目结构

```
cognitive-os/
├── README.md              ← English
├── README.zh.md           ← 你正在看这份
├── LICENSE
├── docs/                  ← GitHub Pages 源文件（展示网站）
│   ├── index.html         → funshh.github.io/cognitive-os/
│   ├── Demo1-*.html       → 判断生命周期
│   ├── Demo2-*.html       → 判断到决策
│   ├── Demo3-*.html       → 每日心跳
│   ├── themes/            → 投资主题示例（领域应用样本）
│   └── en/                → 英文版展示页
└── starter/               ← fork-and-go 模板
    ├── README.md          ← English
    ├── cognitive-os.md    ← 核心思想（先读这个）
    ├── SCHEMA.md
    ├── AGENT_PROTOCOL.md
    ├── templates/
    └── zh/                ← 中文镜像
        ├── README.md
        ├── cognitive-os.md
        ├── SCHEMA.md
        ├── AGENT_PROTOCOL.md
        └── templates/
```

---

## 引擎 vs 产线

认知引擎是**引擎**，不是某个领域的成品系统。投资 OS / 内容 OS / 产品 OS 这些**产线**，是在引擎之上、针对一个具体领域搭出来的执行系统。

```
认知引擎    →    Topic    →    产线
（本仓库）       （引擎遇到        （投资 OS、
                 你的领域）         内容 OS、…）
```

starter 交付引擎。你的产线，是在你长期使用过程中、随着领域专属的 Cognition 节点和 Methodology 特化协议慢慢长出来的。

完整架构论述见 [`starter/zh/cognitive-os.md`](./starter/zh/cognitive-os.md) §"引擎 vs 产线"。

---

## License

- **模板和代码** → MIT
- **思想类文档**（`cognitive-os.md`、各 README）→ CC BY-NC 4.0

---

## 致谢

- **[Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** —— LLM Wiki，框定了这套范式所延伸的模式
- **Vannevar Bush** —— Memex（1945），两套范式共同的祖父
- **Karl Popper** —— 可证伪性，让"相信"变成可测试的知识
- **DIKW & SECI 模型** —— 让认知的层次划分变得精确

---

*如果你为自己的领域搭建了一个认知引擎实例，欢迎 PR 或开 issue 附上你的 fork 链接。这个范式想被实例化，不想被独占。 —— Maxwell*
