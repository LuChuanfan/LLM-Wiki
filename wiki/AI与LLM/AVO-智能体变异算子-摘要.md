---
title: AVO：智能体变异算子
category: AI与LLM
tags: [进化搜索, LLM, 智能体, GPU优化, NVIDIA, 参考文献]
sources: [raw/papers/others/AVO Agentic Variation Operators for Autonomous Evolutionary Search.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# AVO：智能体变异算子

**论文信息：** Terry Chen et al. (NVIDIA). arXiv预印本, 2026年3月.

## 核心思想

提出"智能体变异算子"(AVO)，用自主编程智能体替代传统进化搜索中固定的变异/交叉等手工启发式操作。

## 核心方法

- 将变异算子从"LLM单次生成"提升为"自主编程智能体循环"
- 智能体拥有完整工具链（代码编辑、编译、性能剖析、文档检索）
- 自监督机制在停滞时自动调整搜索方向
- 单谱系连续进化，每个版本以git commit持久化

## 关键结果

在NVIDIA B200 GPU多头注意力核优化中：
- 超越cuDNN最多**3.5%**
- 超越FlashAttention-4最多**10.5%**
- 7天连续自主进化
- 发现的优化可迁移至GQA（仅需30分钟适配）

## 相关页面
- [[FunSearch-LLM程序搜索数学发现-摘要]]
