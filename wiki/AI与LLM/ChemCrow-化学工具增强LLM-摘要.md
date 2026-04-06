---
title: ChemCrow：化学工具增强LLM
category: AI与LLM
tags: [LLM, 智能体, 化学, 工具增强, 自动化实验, 参考文献]
sources: [raw/papers/others/Augmenting large language models with chemistry tools.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# ChemCrow：化学工具增强LLM

**论文信息：** Andres M. Bran et al. Nature Machine Intelligence, Vol. 6, May 2024.

## 核心思想

提出ChemCrow，一个集成18种专家设计工具的LLM化学智能体，基于GPT-4，可完成有机合成、药物发现和材料设计等任务。

## 核心方法

- 将18种化学专用工具（分子/反应/安全/通用）集成到GPT-4
- 采用Thought-Action-Observation链式推理框架（类ReAct）
- 连接RoboRXN机器人平台实现物理实验执行

## 主要贡献

- 首次将18种化学专用工具与LLM集成
- 自主完成4种化合物的合成实验
- 通过人机协作发现了一种新型发色团（336nm）
- 降低了非专业人员进入化学研究的门槛

## 相关页面
- [[Coscientist-自主化学研究-摘要]]
- [[LLM-RDF-端到端化学合成-摘要]]
- [[AI科学家安全风险-摘要]]
