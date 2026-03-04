---
name: deep-research
description: 对复杂话题进行多轮结构化深度研究，自动拆解子问题、迭代搜索、综合多来源信息并输出带引用的报告。支持 Quick/Standard/Deep 三种深度模式，内置 DeFi/Web3 来源优先级与时效性数据处理。触发词：深度研究、深研、深度调研、研究一下、research、调研、分析一下、help me research、deep research。
license: MIT
compatibility: Requires internet access (WebSearch, WebFetch tools)
metadata:
  author: ben
  version: "1.2"
---

# Deep Research

多轮迭代研究工作流，参考 Kimi Deep Research / Perplexity 设计理念，聚焦结果质量。

## 研究深度模式

用户可指定，未指定默认 **Standard**：

| 模式 | 子问题数 | 迭代轮次 | 最低来源数 | 适用场景 |
|------|---------|---------|---------|---------|
| **Quick** | 2–3 | 1 | ≥3 | 快速了解、验证单一事实 |
| **Standard** | 3–5 | 2 | ≥5 | 一般调研、方案对比 |
| **Deep** | 5–7 | 3+ | ≥10 | 重要决策、完整市场分析 |

## 核心流程

### Phase 1 — 拆解问题

收到请求后，**先不搜索**：

1. 识别深度模式（用户未指定则默认 Standard）
2. 拆解为对应数量子问题，覆盖：背景定义 → 核心机制 → 横向对比 → 风险/争议
3. 向用户展示研究计划，确认后执行

### Phase 2 — 多轮搜索

**并行优先**：同一轮次的多个子问题，尽可能在单次响应中并行发起 `WebSearch`，而不是逐个串行。`WebFetch` 精读同理。

每个子问题：

1. `WebSearch` 获取来源列表
2. `WebFetch` 精读最重要的 2–3 个页面全文
3. 记录：关键发现 + 来源 URL + 可信度评估

**DeFi/Web3 来源优先级：**
- P0：官方文档、白皮书、审计报告（CertiK、Trail of Bits 等）
- P1：链上数据（DeFiLlama、Dune、Token Terminal）— **必须标注数据抓取时间**
- P2：主流媒体（The Block、Decrypt、Bankless）
- P3：社区讨论（governance forum、Discord、核心开发者 Twitter）

**通用来源优先级：**
官方文档 > 同行评审论文 > 权威媒体 > 社区讨论

### Phase 3 — 反思与补漏

每轮搜索后检查：
- 哪些子问题仍未充分回答？
- 来源间是否存在矛盾？
- 是否有新的关键问题浮现？

**终止条件（满足任一即停止迭代）：**
- 所有子问题已有 P0/P1 来源支撑
- 已达当前模式的最大轮次上限
- 新一轮搜索未带来实质性新信息

### Phase 4 — 综合输出

按 [references/report-template.md](references/report-template.md) 生成报告。如模板文件不可访问，使用以下最小结构：`TL;DR → 关键发现表格 → 深度分析各节 → 争议与不确定性 → 来源列表`。

综合原则：
- 最重要的洞见开头（倒金字塔）
- 区分"共识结论"与"有争议的观点"
- 明确写出不确定性和信息空白
- 每个事实性主张附来源链接
- 价格、TVL、APY 等时效性数据**必须标注获取时间**

## 质量检查

- [ ] 达到当前模式的最低来源数量
- [ ] 每个关键主张有来源支撑
- [ ] 来源矛盾已注明
- [ ] 不确定点和信息空白已标出
- [ ] 报告以 TL;DR 开头
- [ ] 所有时效性数据已标注获取时间

## 补充说明

- 报告默认**中文**输出，用户指定则用英文
- 信息量极大时，可分"基础层"和"深度层"两次输出
- 某子问题找不到可靠来源时，明确告知而非猜测填充

## 参考资源

- 输出模板：[references/report-template.md](references/report-template.md)
