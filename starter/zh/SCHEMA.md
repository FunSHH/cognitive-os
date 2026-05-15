# SCHEMA.md · 中文版

> **每次会话开始，让你的 LLM agent 读这份。**
> 这是配置，让通用 LLM 变成一个有纪律的认知引擎维护者。
> 与你的 agent 协同演化这份文件。

---

## 1. 仓库结构

```
your-vault/
├── _system/
│   ├── SOUL.md                 ← Agent 角色与认知引擎哲学
│   ├── SCHEMA.md               ← 本文件
│   └── AGENT_PROTOCOL.md       ← 操作协议
├── 00_inbox/                   ← 原始输入未处理
├── 01_drafts/                  ← 进行中的思考
│   └── feedback/               ← 用于反向更新的反馈文件
├── 02_memory/                  ← 高压缩背景（LLM 会话开始读）
├── 03_knowledge/               ← LLM Wiki 层：外部事实
│   ├── entities/
│   ├── concepts/
│   ├── theories/
│   ├── facts/
│   └── index.md                ← Knowledge 层索引
├── 04_cognition/               ← ★ Cognition Wiki: 你的判断
│   ├── world/                  ← 关于外部世界的判断
│   ├── domain/                 ← 关于具体领域的判断
│   ├── self/                   ← 关于自己（价值观 / 原则）的判断
│   ├── meta/                   ← 关于思维方法的判断
│   └── index.md                ← Cognition 层索引
├── 05_topics/                  ← 主题级工作台（把方法论应用到具体领域）
├── 06_workbench/               ← 日 / 周 / 决策日志
│   ├── daily/
│   ├── weekly/
│   ├── synthesis/              ← LLM 给你的报告
│   └── decisions/              ← 决策快照（不可变更）
└── 07_methodology/             ← 程序性知识：你签下的协议
```

---

## 2. 判断节点 frontmatter（必填字段）

`04_cognition/` 下的每个文件**必须**有这套 YAML frontmatter：

```yaml
---
type: cognition
domain: [你的领域 — 投资 / 研究 / 产品 / 政策 / 等]
layer: [worldview | theory | framework | thesis | observation]
confidence: 🔴 0.xx | 🟡 0.xx | 🟢 0.xx
created: YYYY-MM-DD
updated: YYYY-MM-DD
evidence:
  - YYYY-MM-DD [源页面链接]: 一句话摘要
falsifiers:
  - F1: [会让此判断失效的条件，一句话]
  - F2: [...]
  - F3: [...]
methodology: "[[关联方法论文件链接]]"   # Domain / Meta 层必填
tags: [tag1, tag2]
---
```

### 置信度语义

- **🔴 0.30 – 0.50** = 初判 / 直觉 / 单源观察。**还不是判断，更像假设**。Falsifier 已列出但未被主动监测。
- **🟡 0.50 – 0.75** = 多个独立来源验证，没有 falsifier 触发。**意见正在形成**。值得跟踪但还不到该采取行动。
- **🟢 0.75 – 0.95** = 稳定，多重收敛证据，关键 falsifier 已被测试且没触发。**可采取行动的判断**。可以驱动协议。

置信度**协同演化**。LLM 建议，你确认。LLM 永远不会静默地升级置信度 —— 只能建议，你签。

### 层级语义

- **worldview** —— 对世界某部分如何运作的广义信念（"Higher-for-longer 是结构性而非周期性"）
- **theory** —— 你会反复套用的分析框架（"收益率曲线有三层结构，分别由不同力量驱动"）
- **framework** —— 对一类问题的结构化路径（"六层投资分析：机制 → 叙事 → 传导 → 基本面 → 定价 → 配置"）
- **thesis** —— 关于具体主题的可行动判断（"领域 X 处于加速期晚段"）
- **observation** —— 单数据点的判断，随时间可能升级为 theory

---

## 3. Falsifier 命名约定

Falsifier 在一个判断节点内命名为 **F1, F2, F3...**

如需做子层级（如一个 thesis 下面分多个子判断），用 **F-Xn** 格式，X 是一个大写字母前缀（取子实体首字母），n 是序号：
- 关于实体 ABC 的 thesis → F-A1, F-A2
- 关于实体 XYZ 的 thesis → F-X1, F-X2

每个 falsifier **必须**：
- **一句话**（强制清晰）
- **可观察**（你能识别它发生没）
- **彼此独立**（不重叠）

**Falsifier 状态**（LLM 跟踪）：
- `🟢 未触发` —— 没有证据接近此条件
- `⚠️ 接近触发` —— 最近证据在向此条件靠近
- `⛔ 反向证伪深化` —— 原 falsifier 的反面在被证实（判断在变强）
- `❌ 已触发` —— falsifier 条件满足；判断需要重新审视

---

## 4. 演化阶段分类

对于跟踪随时间演化的现象的判断，标注：

| 阶段 | 符号 | 含义 |
|---|---|---|
| 萌芽 / Emerging | E | 早期信号，多为猜测 |
| 加速 / Accelerating | A | 现象有明确证据，势头在增强 |
| 制度化 / Institutionalizing | S- | 现象正在被正式化 / 接受 |
| 拥挤 / Crowded | S+ | 共识形成，惊喜空间消失 |
| 退潮 / Fading | B- | 反转开始，共识瓦解 |

你的领域可能用不同分类 —— 在这里定义。

---

## 5. methodology 字段

每个 Domain / Meta 层判断**必须**有 `methodology` 字段，指向 `07_methodology/` 下的程序性文件。

当那个方法论文件因为反馈被升级时，LLM 扫描所有判断节点的此字段，**自动追加一条 evidence**：

```yaml
evidence:
  - 2026-XX-XX [来自反馈 Y 的方法论更新]: 方法论已升级，请确认本判断是否仍然成立
```

这就是**反馈反向更新（Feedback Reverse-Update）**操作。

---

## 6. 索引文件（仿 LLM Wiki 约定）

- `03_knowledge/index.md` —— Knowledge 层内容目录
- `04_cognition/index.md` —— Cognition 层内容目录，按 domain / layer 分组
- `06_workbench/synthesis/log.md` —— 按时间顺序记录每次 ingest / synthesis / lint

每个索引条目应包含：页面链接、一句话摘要、最后更新日期、（对 Cognition）当前置信度。

---

## 7. LLM **不要静默做**的事

- ❌ 永远不要不经确认就升 / 降置信度 —— 必须建议，你确认
- ❌ 永远不要修改判断的 `falsifiers` 列表（你写的，你改）
- ❌ 永远不要删除 evidence 条目（只追加，保留完整审计轨迹）
- ❌ 永远不要对 falsifier 触发采取行动 —— 标记，你决定
- ❌ 永远不要决定什么算"反馈" —— 等你标记
- ❌ 永远不要直接写 `06_workbench/decisions/` —— 那是你作者的快照

---

## 8. LLM **应该不问就做**的事

- ✅ 新摄入明显触动某判断节点时追加 evidence
- ✅ 当证据支持演化阶段转换时更新该字段（在 evidence 里一句话注明）
- ✅ 每天写 Daily Synthesis 报告总结过去 24 小时所有变化
- ✅ 每周跑 Lint 并产出报告
- ✅ 每天跑 Falsifier 扫描，标记接近触发的
- ✅ 方法论更新时反向追加 evidence 到所有引用它的节点
- ✅ 始终保持 `index.md` 文件最新
- ✅ 交叉引用：新建判断时扫描相关判断，添加双向链接

---

## 9. 定制清单

跑这套之前先定制：

- [ ] 领域值（替换"投资 / 研究 / 等"为你实际做的）
- [ ] 层级分类（扩展或简化 worldview / theory / framework / thesis 这套划分）
- [ ] 置信度阈值（你的 0.50 可能与别人不同）
- [ ] 演化阶段命名（中文 / 英文 / 领域特定）
- [ ] Falsifier 前缀约定（如做投资，stock-thesis 层用 F-Xn）
- [ ] 日 / 周任务调度时间
- [ ] Inbox 路由规则

**有疑虑时：不要预先优化**。让 schema 在第一个月真实摩擦中自然累积。

---

*版本 1.0 · 每次会话有摩擦时，与你的 LLM 一起演化这份文件。*
