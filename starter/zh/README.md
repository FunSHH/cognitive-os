# 认知引擎 Starter · 中文版

> 一个用 LLM 搭建**判断引擎**的起手包 —— 不只是用 LLM 维护知识，是用 LLM 维护判断。

如果 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 是"把'事实是什么'的 bookkeeping 外包给 LLM"，**认知引擎就是它的上一层 —— "把'你相信什么、为什么、什么会让你改观'的 bookkeeping 外包给 LLM"。**

[English version →](../README.md)

---

## 这是什么

一份最小化的、可被 LLM 实例化的模板 —— 你用它启动一个属于自己的"判断 wiki"。每个判断节点带置信度（confidence）、证据链（evidence）、证伪条件（falsifier）、关联方法论（methodology），由 LLM 维护和升级。

它对标的不是 Knowledge 层，而是 DIKW 模型的最顶层 —— **Wisdom（智慧 / 判断）**。

核心思想见 [`cognitive-os.md`](./cognitive-os.md)，**先读这个，再用 starter**。

---

## 为什么需要这件事

**LLM 正在让 Knowledge 商品化**。你脑子里的事实数量正在贬值 —— 任何人一个 prompt 就能拿到。你的竞争优势不能再坐在"知识密度"上，它必须坐在 **判断质量**上。

而判断质量只有在一个**强制你高频、结构化地形成与更新判断**的系统里，才会复利。

LLM 是这个系统的完美维护者 —— 它不会无聊，不会忘记更新一条交叉引用，可以在一次过程里同时更新 15 个节点。**维护一个判断图谱的成本，在 LLM 介入后接近为零**。

---

## 适合谁

- **投资人** —— 每个 thesis 都是一个判断节点，仓位本身就是协议
- **研究者** —— 每个 hypothesis 都是判断，复现是验证
- **产品决策者** —— 每个 roadmap bet 都是判断，用户反馈是 falsifier 扫描
- **政策分析师** —— 每个建议都是判断，且有明确假设
- **创业者** —— 每个战略选择都是判断，收入 / 留存是方法论更新
- **任何"反复做决策、且对错重要"的脑力劳动者**

**不适合**：只想"记得更多"的知识收藏者（用 LLM Wiki）；轻度日记（用任何笔记 app）；纯创作（用任何能流畅写作的工具）。

---

## 引擎 vs 产线

认知引擎是**引擎，不是某个领域的成品系统**。

你可能在我的其他工作中看到过"投资 OS"、"内容 OS"、"产品 OS"这些词。那些是**产线** —— 在认知引擎之上、针对一个具体领域（投资 / 内容 / 产品）搭建的完整执行系统，带领域专属的 Topic、特化方法论、调度任务、仪表盘。

**本 starter 交付的是引擎。产线由你和你的 LLM agent 一起长出来。**

```
认知引擎    →    Topic   →    产线
（引擎，         （引擎          （领域成品系统 —
 本仓库）         遇到你          投资 OS、
                 的领域）         内容 OS、…）
```

starter 故意保持领域无关。模板展示结构，不展示内容。一旦你拿它去实例化自己的真实领域，Topic 就开始生长。几个月每日心跳跑下来，Topic 积累了足够多的领域专属方法论，**结晶**成产线。**同一台引擎，不同的 Topic。**

---

## Starter 包包含什么

```
cognitive-os-starter/zh/
├── README.md                    ← 你正在看的这份
├── cognitive-os.md              ← ★ 核心思想（"为什么" — 先读这个）
├── SCHEMA.md                    ← 给 LLM 每次会话开始读的配置文件
├── AGENT_PROTOCOL.md            ← Agent 操作协议 — LLM 做什么、何时做
└── templates/                   ← markdown 模板
    ├── judgment-node.md         ← 单个判断节点的 schema
    ├── daily-synthesis.md       ← LLM 每日跑完后给你的报告
    ├── feedback.md              ← 行动后你怎么记反馈
    └── lint-report.md           ← 周度巡检报告
```

Starter 包**故意做得最小化**。你 fork 它、交给你的 LLM agent、一起协同设计适合你领域的实例化版本。

---

## 怎么用

### 第 1 步 · 读 [`cognitive-os.md`](./cognitive-os.md)

别跳过。这份文档解释 *为什么*。不内化这个，模板会让你觉得任意武断。

### 第 2 步 · 把这个目录复制到你的知识仓库

建议：在你放笔记的位置旁边新建一个目录，**先别合并进现有 vault**。从空白开始，看这套范式是否对你有用。

```bash
# 克隆整个 repo（starter 是其中一个目录）：
git clone https://github.com/FunSHH/cognitive-os.git
cd cognitive-os/starter/zh

# — 或者 — 从 GitHub 下载 zip，解压后取出 starter/zh/ 目录即可。
```

### 第 3 步 · 用你的 LLM agent 打开它

Claude Code / Cowork / Cursor / Codex / OpenAI Agent —— 任何能读写文件的 LLM。告诉它：

> "读 `cognitive-os.md` 和 `SCHEMA.md`。从现在起，把这个目录当作认知引擎仓库。按 `AGENT_PROTOCOL.md` 的操作协议工作。帮我把 schema 调整到适合我的领域。"

### 第 4 步 · 与 LLM 协同演化 schema

starter 里的 schema 是泛例。你需要：
- 决定你的领域命名（投资 / 研究 / 产品 / 政策 / …）
- 决定你的演化阶段分类
- 决定你的 falsifier 命名约定
- 决定 🔴 / 🟡 / 🟢 各对应什么状态
- 决定日 / 周维护协议

别想着一次写完。每次会话发现"LLM 做了 X 但应该做 Y"，就把规则写进 schema，下次它就照做。

### 第 5 步 · 从一个判断开始

别想着一次填满 vault。挑你现在正在做的一个判断（一个投资 thesis、一个研究假设、一个产品 bet），用 `templates/judgment-node.md` 创建第一个判断节点。让 LLM 帮你填证据、写 falsifier、关联方法论。

一周后你会知道这套范式是否适合你。一个月后你会有 ~10 个判断节点，schema 也已经被定制成你自己的样子。

### 第 6 步 · 加每日扫描

当你有 ≥5 个 active 判断时，配一个每日任务（cron / GitHub Action / agent 的调度任务）。agent 自动扫描所有判断，报告"接近触发的 falsifier"、标记"过期判断"、建议"置信度更新"。**你花 5 分钟读报告**。

这一刻开始，系统从"又一个笔记目录"变成"活的判断引擎"。

---

## 与 LLM Wiki 的关系

如果你读过 Karpathy 的 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)，这里是核心差异：

|               | LLM Wiki              | 认知引擎                                                                  |
| ------------- | --------------------- | --------------------------------------------------------------------- |
| **目标**        | 知识积累                  | **判断积累**                                                              |
| **Wiki 内容**   | 实体页 / 概念页 / 综合页       | **判断节点 + 置信度 + 证伪条件**                                                 |
| **架构**        | Raw + Wiki + Schema   | Raw + Knowledge + **Cognition** + Methodology                         |
| **操作**        | Ingest / Query / Lint | + **Falsifier 扫描** + **反馈反向更新**                                       |
| **Schema 文件** | CLAUDE.md / AGENTS.md | SCHEMA.md + AGENT_PROTOCOL.md                                         |
| **可叠加？**      | 是 — 用作 Knowledge 层    | **建议直接用 LLM Wiki 做 Knowledge 层**，认知引擎在它之上加 Cognition + Methodology 两层 |

**两者可以共存。** Knowledge Wiki 在下游，Cognition Wiki 在上游 —— 判断节点的 `evidence` 字段直接引用 Knowledge Wiki 的页面。

---

## 成熟度

🟡 **Pre-1.0**。范式在一个生产 vault 里完整跑通（一个个人投资 / 研究 / 产品复合操作，~8 个月运转时间，~100 个判断节点，~22 个活跃主题）。这里的 schema 和协议模板都是从那个 vault 提取并匿名化的。

范式稳定，模板会随着更多领域的尝试而演进。

---

## 实例 / Examples in the wild

如果你为自己的领域搭建了一个认知引擎实例，**欢迎 PR 或开 issue** 附上你的 fork 链接。这个范式想被实例化，不想被独占。

**已知实例**：
- 投资 thesis 跟踪（~22 主题，~100 判断节点，~8 个月运转）—— 这个 starter 的源 vault

---

## License

MIT 用于模板和代码。CC BY-NC 4.0 用于思想类文档。

外部引用（LLM Wiki / DIKW 模型 / SECI 模型 / Memex / Popper 的可证伪性）在文档内署名。

---

## 致谢

- **Andrej Karpathy** —— [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)，框定了这套范式所延伸的模式
- **Vannevar Bush** —— Memex（1945），两套范式共同的祖父
- **Karl Popper** —— 可证伪性，让"相信"变成可测试的知识
- **DIKW & SECI 模型** —— 让认知的层次划分变得精确

---

*认知引擎本身就是用认知引擎搭建的。整个 starter 包 —— 包括这份 README —— 是先在一个真实的 vault 里作为判断节点存在，然后导出的。它在吃自己的狗粮。*
