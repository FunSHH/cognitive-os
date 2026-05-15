---
type: synthesis-lint
date: YYYY-MM-DD
scope: [knowledge-only | cognition-only | both]
trigger: [scheduled-weekly | manual]
---

# 巡检报告 · YYYY-MM-DD

> 整个 vault 的周度健康检查。
> Agent 跑，用户 ~30 分钟复核。

---

## 第一层 · 系统一致性

> Schema 在被遵守吗？索引是否最新？

- [ ] `03_knowledge/index.md` 与所有 Knowledge 页面同步
- [ ] `04_cognition/index.md` 与所有判断节点同步
- [ ] 所有判断节点有必需的 schema 字段（type/domain/layer/confidence/evidence/falsifiers）
- [ ] 所有 Domain / Meta 层节点的 `methodology` 字段已填
- [ ] 没有孤立文件（没有入向链接的页面）

**发现的问题**：
- [列出]

---

## 第二层 · Knowledge Wiki 健康

### 过期页面
> 6+ 个月没更新。可能是问题，也可能不是。

- [[页面 A]] —— 最后更新 YYYY-MM-DD

### 跨页面矛盾
> 不同页面给出相反声明。

- [[页面 X]] 说 "..." 但 [[页面 Y]] 说 "..."。建议：调和或显式对比页。

### 缺失实体 / 概念
> 多页面提及但无专属页面。

- "X" —— 5+ 页面提及，无实体页

### 断裂的证据链
> Cognition 的 `evidence:` 字段引用了已移动 / 删除的 Knowledge 页面。

- [...]

---

## 第三层 · Cognition Wiki 健康

### 过期判断
> N+ 个月没新 evidence。可能失败模式：不再相关 / 系统没注意到相关信号 / 领域不活跃。

- [[判断 A]] —— 最后 evidence YYYY-MM-DD（X 个月前）

### 接近触发的 Falsifier — 未被确认
> Falsifier 处于 `⚠️ 接近触发` 状态超过 2 周用户没复核。

- [[判断 B]] · F2 —— 自 YYYY-MM-DD 起接近触发。**建议用户行动**。

### 已触发的 Falsifier — 未被处理
> Falsifier 完全触发（`❌`）但置信度未下调 / 判断未修订。

- [[判断 C]] · F4 —— 触发于 YYYY-MM-DD。**置信度急需复核**。

### 矛盾判断
> 两个判断给出相反声明。

- [[判断 X]] 和 [[判断 Y]] 似乎矛盾。建议：解决、合并或显式标注分歧。

### 缺失 methodology 字段
> 应有 `methodology` 链接但没填的 Domain / Meta 层节点。

- [...]

### 升格候选
> 有 5+ evidence 条目的 observation 应升到 thesis。

- [[观察 O1]] —— N 条 evidence；升级？

---

## 第四层 · 方法论库健康

### 被引用但缺失的方法论
> `methodology:` 字段指向不存在的文件。

- [...]

### 最近被更新的方法论 — 反向更新审计
> 当方法论 X 被更新时，反向更新有触发吗？

- [[方法论 M]] 更新于 YYYY-MM-DD。关联判断：N。应追加 evidence：N。

### 过期方法论
> 12+ 个月没更新。可能没问题，但值得扫一眼。

- [...]

---

## 第五层 · 覆盖缺口

### 被引用但未定义的主题
> 在判断 / 工作台里被提及但没有主题工作空间。

- "..." —— 被提及 3+ 次，无 `05_topics/<name>/` 存在

### 活动高但判断密度低的领域
> 大量摄入，但判断不多。可能：大量输入但没有形成观点。值得反思。

- 领域 X：N 次摄入，仅 M 个判断

---

## 行动项

> 用户需确认或处理：

- [ ] 复核接近触发的 falsifier（见上）
- [ ] 确认或否决升格候选
- [ ] 解决矛盾判断对
- [ ] 填充缺失的 methodology 链接

---

## 摘要统计

- Knowledge 页面：N
- Cognition 节点：M（🔴 X / 🟡 Y / 🟢 Z）
- 活跃主题：K
- 接近触发的 falsifier：W
- 过期判断：Q
- 距上次 Lint 天数：D

---

*Lint 是反熵操作。没有它，wiki 静默腐烂。有它，wiki 保持活性。*
