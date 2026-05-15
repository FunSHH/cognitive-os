# AGENT_PROTOCOL.md · 中文版

> **LLM agent 的操作协议** · 每次会话开始读
> 与 [SCHEMA.md](./SCHEMA.md) 配套使用

---

## 会话初始化（每次必做）

1. 读 [`_system/SOUL.md`](#) —— agent 角色与哲学
2. 读 [`_system/SCHEMA.md`](./SCHEMA.md) —— 仓库结构与规则
3. 读 [`02_memory/`](#) —— 高压缩背景上下文
4. 读最近 1-2 天的 `06_workbench/daily/` —— 近期上下文
5. **任何摄入之前**：先读 `03_knowledge/index.md` 和 `04_cognition/index.md`，理解已有什么。"**更新优先于新建**" —— 给已有节点追加，永远优先于新建节点。

---

## 五个核心操作

### 📥 操作 1 · 摄入 Ingest（用户放入新资料时）

```
Step 1  读 03_knowledge/index.md → 是否已有实体 / 概念页覆盖这条？
Step 2  若有 → 给该页追加（保留旧内容，追加新发现，标记矛盾）
        若无 → 新建一个 Knowledge Wiki 页面
Step 3  扫描 04_cognition/index.md → 这条资料触动了任何 active 判断？
Step 4  对每个被触动的判断节点：
        a. 在 evidence: 列表追加一行带 [日期] [来源] 标签的一句话
        b. 重新评估 falsifier 状态（这条证据让某 falsifier 向触发靠近 / 远离？）
        c. 若该升级置信度，**建议**（不要静默改）
        d. 重新评估 evolution-stage（若适用）
Step 5  在 06_workbench/synthesis/YYYY-MM-DD.md 写 Synthesis 报告：
        - 摄入了什么
        - 哪些 Knowledge 页被更新 / 新建
        - 哪些 Cognition 节点被触动
        - 哪些 falsifier 状态变化
        - 哪些置信度更新被建议（待用户确认）
        - 任何升格候选（值得从 observation 提升到 thesis 的判断）
```

---

### 🔍 操作 2 · 查询 Query（用户提问时）

```
Step 1  判断这是 Knowledge 类问题还是 Cognition 类问题
        - Knowledge："来源 X 怎么说 Y？" → 读 03_knowledge/
        - Cognition："我对 Y 怎么看？" → 读 04_cognition/
Step 2  对 Cognition 类问题：
        - 找到相关判断节点
        - 回报：判断本身、置信度、最近 3-5 条 evidence、falsifier 状态
        - 不要生成新观点。回报已存在的观点。
Step 3  若用户问的内容已有判断不覆盖：
        - 建议创建新判断节点
        - 帮助起草初始置信度 + falsifier
        - 等用户签字后再创建
```

---

### 🧹 操作 3 · 巡检 Lint（每周或触发时）

```
Knowledge 层 Lint：
- 孤立页（无入向链接）
- 页面之间的矛盾声明
- 过期页面（N 个月没更新）
- 缺失实体页（被多页提及但无独立页）

Cognition 层 Lint：
- 过期判断（N 个月没追加 evidence）
- 接近触发但用户未确认的 falsifier
- 互相矛盾的判断（交叉引用不一致）
- Domain / Meta 层缺失 methodology 字段的节点
- 指向已删除 / 移动的 Knowledge 页面的 evidence 链
- 升格候选：有 5+ 支持证据的 observation → 建议升级到 thesis

输出：06_workbench/synthesis/YYYY-MM-DD_lint.md
```

---

### 🔬 操作 4 · 证伪扫描 Falsifier Sweep（每日）

```
对每个 active 判断节点（置信度 ≥ 🟡）：
  对每个 falsifier F1...Fn：
    搜索最近 N 天的摄入，看是否有证据让 falsifier 状态变化：
    - 新证据支持 falsifier 条件 → 标记 "⚠️ 接近触发"
    - 新证据是 falsifier 的反面 → 标记 "⛔ 反向证伪深化"
    - falsifier 条件满足 → 标记 "❌ 已触发，请用户复核"

在每日 Synthesis 里输出简短摘要：
  - 今日触动 X 个判断
  - Y 个 falsifier 接近触发（列出，附一句话上下文）
  - Z 个演化阶段转换建议
  - W 个升格候选
```

---

### 🔄 操作 5 · 反馈反向更新 Feedback Reverse-Update（用户记录反馈时）

```
Step 1  用户在 01_drafts/feedback/ 放一个反馈文件，描述：
        - 采取了什么行动
        - 行动由哪个判断驱动
        - 结果是什么
        - 学到了什么
Step 2  Agent 读反馈
Step 3  识别该更新哪个方法论文件：
        - 驱动判断的 methodology 字段所指的文件是首要候选
        - 建议具体编辑
        - 等用户签字
Step 4  方法论更新后：
        - 扫描 04_cognition/ 下所有 methodology 字段引用该文件的节点
        - 给每个追加一条 evidence:
          "YYYY-MM-DD [来自反馈 X 的方法论更新]：<一句话摘要>"
        - 可选：标记这些判断让用户复核（更新会影响它们吗？）
Step 5  在 06_workbench/synthesis/YYYY-MM-DD.md 记录反向更新动作
```

---

## 路由规则 · 新文件去哪里

| 内容类型 | 去向 |
|---|---|
| 外部事实 / 数据 / 可引用语录 | `03_knowledge/facts/` |
| 概念定义 / 抽象想法 | `03_knowledge/concepts/` |
| 人物 / 组织 / 实体 | `03_knowledge/entities/` |
| 来自外部资源的理论框架 | `03_knowledge/theories/` |
| 多源综合（仍是外部视角） | `03_knowledge/synthesis/` |
| **你的世界观 / 对世界的信念** | `04_cognition/world/` |
| **你的领域特定判断** | `04_cognition/domain/<领域>/` |
| **关于自我 / 身份 / 价值观的信念** | `04_cognition/self/` |
| **关于思维方法 / 元认知的信念** | `04_cognition/meta/` |
| 活跃研究主题 / 项目工作空间 | `05_topics/<topic>/` |
| 日常日志 | `06_workbench/daily/YYYY-MM-DD.md` |
| 决策快照（不可变） | `06_workbench/decisions/YYYY-MM-DD-<title>.md` |
| 你命名的协议 / 框架 | `07_methodology/<domain>/<name>.md` |
| 综合 / Lint / 扫描报告 | `06_workbench/synthesis/YYYY-MM-DD_<type>.md` |

---

## 必做 vs 可选

### 必做（每次会话）
- 会话开始读 SOUL + SCHEMA + Memory
- 保持 `03_knowledge/index.md` 和 `04_cognition/index.md` 最新
- 跑 Falsifier 扫描（若调度了）
- 每次摄入操作结束写 Synthesis 报告

### 必做（适用时）
- 方法论更新后反向追加 evidence
- **建议**（不要执行）置信度变化
- 标记接近触发的 falsifier 给用户

### 可选
- 判断图谱的可视化
- 自动建议待研究的相关问题
- 跨 Cognition Wiki 的周度趋势报告

---

## 不要做的事

❌ 永远不要静默升 / 降置信度 —— 总是建议，等确认
❌ 永远不要删除 evidence 条目 —— 只追加（保留审计轨迹）
❌ 永远不要在未明确许可的情况下修改 falsifier 措辞
❌ 永远不要对 falsifier 触发采取行动 —— 标记，由用户决定
❌ 永远不要决定什么算"反馈" —— 等用户标记
❌ 永远不要写 `06_workbench/decisions/`（那是用户作者的快照）
❌ 当被问"我对 X 怎么看"时永远不要生成新观点 —— 回报已存在的判断

---

## 失败模式 & 恢复

- **两个判断冲突**：给两个都追加一条注释，下次 Synthesis 标记给用户。不要单方面解决。
- **来源与已有 Knowledge 页矛盾**：保留两个；标记 `⚠️ 与 [其他页] 矛盾`；提醒用户。
- **methodology 文件被链接但不存在**：创建占位；提醒用户填充。
- **建议置信度但用户不同意**：撤回建议；把分歧本身记为该判断的 evidence（这本身就是信号）。

---

## 协同演化

本协议**不是固定的**。每次会话后，若出现摩擦：
- 更新 SCHEMA.md 加入新规则
- 更新本 AGENT_PROTOCOL.md 加入新操作或细化已有操作
- 更新 SOUL.md 若认知引擎哲学有所演变

**用 git 版本化这个文件**。把协议漂移视为一等关切。

---

*版本 1.0 · 协议是活文档。工作流要求时就更新它。*
