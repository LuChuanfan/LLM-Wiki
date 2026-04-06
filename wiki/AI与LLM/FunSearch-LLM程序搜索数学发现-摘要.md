---
title: FunSearch：LLM程序搜索的数学发现
category: AI与LLM
tags: [LLM, 进化搜索, 程序合成, 数学发现, DeepMind, 参考文献]
sources: [raw/papers/others/Mathematical discoveries from program search with large language models.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# FunSearch：LLM程序搜索的数学发现

**论文信息：** Bernardino Romera-Paredes et al. (Google DeepMind). Nature, Vol. 625, January 2024.

## 核心思想

提出FunSearch（函数空间搜索），将预训练LLM与系统化评估器配对，搜索的不是解本身，而是描述"如何求解"的程序。

## 核心方法

- 程序数据库（基于岛屿模型的种群管理）
- 采样器（LLM基于best-shot提示生成新程序）
- 评估器（执行并打分）
- 用户提供evaluate函数和程序骨架，FunSearch仅进化关键函数

## 关键结果

- **Cap set问题**：发现n=8维度下大小512的cap set，超越此前已知最优(496)
- **在线装箱问题**：发现优于经典first fit和best fit的新启发式，仅比最优离线方案差0.03%
- 首次证明LLM可用于在开放数学问题上做出超越人类已知结果的发现

## "搜索程序而非搜索解"范式

生成的程序可解释、可扩展，便于领域专家交互分析。发表于Nature，是LLM科学发现的里程碑。

## 相关页面
- [[AVO-智能体变异算子-摘要]]
