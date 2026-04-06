---
title: LLM-RDF：端到端化学合成开发平台
category: AI与LLM
tags: [LLM, 多智能体, 化学合成, 端到端自动化, 参考文献]
sources: [raw/papers/others/An automatic end-to-end chemical synthesis development platform powered by large language models.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# LLM-RDF：端到端化学合成开发平台

**论文信息：** Yixiang Ruan et al. Nature Communications, 2024.

## 核心思想

提出LLM-RDF，利用GPT-4构建六种专用智能体的多智能体系统，覆盖化学合成开发全流程。

## 核心方法

- 六个专用智能体：Literature Scouter、Experiment Designer、Hardware Executor、Spectrum Analyzer、Separation Instructor、Result Interpreter
- 结合Semantic Scholar、Opentrons OT-2、GC-FID-MS等
- Web应用实现人机自然语言交互，支持RAG和链式推理

## 主要贡献

- 首个覆盖合成开发全流程（文献→筛选→动力学→优化→放大→纯化）的统一LLM框架
- 以Cu/TEMPO催化醇氧化反应为案例完整演示
- 在三种不同反应上验证通用性
- Spectrum Analyzer可自动分析GC-FID-MS数据

## 相关页面
- [[ChemCrow-化学工具增强LLM-摘要]]
- [[Coscientist-自主化学研究-摘要]]
