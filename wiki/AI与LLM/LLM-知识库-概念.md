---
title: LLM 知识库
category: AI与LLM
tags: [LLM, 知识管理, RAG, Wiki]
created: 2026-04-05
updated: 2026-04-05
---

# LLM 知识库

一种用 LLM 增量构建和维护的个人知识管理系统。与传统 RAG（每次查询从头检索）不同，LLM 知识库将知识"编译"成结构化的 Markdown 文件，持续更新和保鲜。

## 与 RAG 的对比

| 维度 | 传统 RAG | LLM 知识库 |
|------|----------|-----------|
| 知识积累 | 每次从头检索，无积累 | 增量编译，持续积累 |
| 交叉引用 | 无 | 自动维护双向链接 |
| 可见性 | 黑箱（嵌入向量） | 透明（Markdown 文件） |
| 维护成本 | 低（但质量也低） | 趋近于零（LLM 代劳） |
| 数据所有权 | 依赖平台 | 本地文件，完全可控 |

## 核心特征

1. **持久化**：知识编译一次后持续保鲜，不是每次查询都重新推导
2. **复利增长**：每次摄入新素材和每次提问，都在给知识库添砖加瓦
3. **透明可控**：所有内容都是 Markdown 文件，可检查、可版本控制、可迁移
4. **BYOAI**：可以接入任何 LLM（Claude、GPT、开源模型），不被锁定

## 代表实践
- [[Karpathy-LLM-Wiki-方法论摘要]] — Karpathy 的原创方法论
- Farzapedia — Farza 从 2500 条日记生成的个人维基百科（400 篇文章）

## 相关概念
- RAG（Retrieval-Augmented Generation）
- Obsidian
- Memex（Vannevar Bush, 1945）
