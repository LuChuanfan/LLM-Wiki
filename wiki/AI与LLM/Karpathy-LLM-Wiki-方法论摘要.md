---
title: Karpathy LLM Wiki 方法论摘要
category: AI与LLM
tags: [LLM, 知识管理, Obsidian, Karpathy, RAG]
sources: [raw/articles/karpathy-llm-wiki-gist.md]
created: 2026-04-05
updated: 2026-04-05
---

# Karpathy LLM Wiki 方法论摘要

Andrej Karpathy 于 2026 年 4 月提出的个人知识库构建方法。核心思想：让 LLM 增量构建和维护一个持久化的 Markdown Wiki，而非每次查询都从头做 RAG 检索。

## 核心理念

传统 RAG 每次提问都从头发现知识，没有积累。LLM Wiki 的做法不同：LLM 读完原始资料后，主动提取关键信息，整合到一个持续维护的 Wiki 中。知识被"编译"一次后持续保鲜。

> Wiki 是一个持久的、复利增长的产物。交叉引用已经在那里，矛盾已经被标记，综合分析已经反映了你读过的所有内容。

## 三层架构

- **Raw Sources**（原始素材）：文章、论文、图片、数据文件。只读，LLM 不改。这是真理之源
- **Wiki**（知识页面）：LLM 生成和维护的 Markdown 文件——摘要、实体页、概念页、对比分析、综述
- **Schema**（配置文件）：告诉 LLM 如何组织 Wiki 的规范（如 CLAUDE.md 或 AGENTS.md）。这是把 LLM 从通用聊天机器人变成专业 Wiki 维护者的关键

## 三大操作

1. **摄入（Ingest）**：新素材 → LLM 读取 → 讨论要点 → 创建摘要 → 更新相关页面（一份素材可能触及 10-15 个页面）
2. **提问（Query）**：LLM 搜索 Wiki 页面 → 综合回答 → 好的回答可以归档回 Wiki，让探索也变成知识积累
3. **巡检（Lint）**：定期检查矛盾、孤立页面、缺失链接、过时内容。LLM 还擅长建议下一步研究方向

## 索引与日志

- **index.md**：内容导向的目录，按分类列出所有页面和一句话摘要。LLM 查询时先读索引定位页面。在中等规模（~100 篇来源，几百个页面）下效果很好
- **log.md**：时间线日志，记录每次操作（摄入、提问、巡检）。用一致的前缀格式方便检索

## Karpathy 的实践

- 使用 Obsidian 做浏览 IDE，LLM Agent 做编辑
- "Obsidian 是 IDE，LLM 是程序员，Wiki 是代码库"
- 一个研究方向积累了约 100 篇文章、40 万字
- 不需要花哨的 RAG 基础设施，LLM 自己维护索引就够了
- 推荐工具：Obsidian Web Clipper、qmd 搜索引擎、Marp 幻灯片、Dataview 查询

## 应用场景

- **个人**：目标、健康、自我提升，日记和笔记的结构化整理
- **研究**：深入某个主题数周/数月，增量构建带演进论点的综合 Wiki
- **读书**：逐章整理，构建角色、主题、情节的交叉引用（类似粉丝 Wiki）
- **团队**：由 LLM 维护的内部 Wiki，自动整理 Slack、会议记录、项目文档

## 关键洞察

> "人类放弃维护知识库，是因为维护成本增长得比价值快。LLM 不会厌倦、不会忘记更新交叉引用、一次可以改 15 个文件。"

这个理念与 1945 年 Vannevar Bush 提出的 [[Memex-概念]] 一脉相承——私人的、经过整理的知识库，文档之间的连接和文档本身同样重要。Bush 没能解决的"谁来做维护"的问题，81 年后由 LLM 解决了。

## 相关
- [[LLM-知识库-概念]]

## 来源
- [Karpathy gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [X 帖子](https://x.com/karpathy/status/2039805659525644595)
