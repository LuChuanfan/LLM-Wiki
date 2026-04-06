---
title: 协调模型预测控制的V2G充放电调度
category: 博士研究
tags: [V2G, MPC, MILP, 充电调度, 电池退化, CC-CV, 自己的论文]
sources: [raw/papers/mine/A_Coordinated_Model_Predictive_Control_Accepted.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# 协调模型预测控制的V2G充放电调度

**论文信息：** Chuan-Fan Lu, Guo-Ping Liu, Yi Yu, Jinqiang Cui. IEEE Transactions on Transportation Electrification, Vol. 11, No. 2, April 2025.

## 核心思想

电动汽车大部分时间闲置，可通过V2G技术实现与电网双向能量交互。但仅以最大化个体利润为目标会导致高峰需量费用。本文提出**协调模型预测控制（CMPC）**的V2G调度方法。

## 核心方法

- 基于CMPC的**混合整数线性规划（MILP）**优化
- 考虑里程焦虑、电池退化（日历老化+循环老化）和CC-CV充电模式
- 功率变化率惩罚项抑制功率剧烈波动
- **控制包策略**和在线滚动优化降低计算负担、应对随机充电需求

## 主要贡献

- 提出CMPC的V2G充放电调度方法，可避免峰值需量费用惩罚并抑制充放电功率剧烈波动
- 建立考虑里程焦虑、电池退化和CC-CV充电模式的MILP优化模型
- 提出控制包策略和在线滚动优化方法，降低计算负担并应对随机充电需求到达
- 仿真和硬件实验验证

## 与其他工作的关系

本文侧重**单充电站的集中式V2G调度**，与 [[ADMM分布式经济调度-摘要]] 的分布式多智能体框架互补——后者可将本文扩展为多充电站协调。两篇均采用CC-CV充电模式和电池退化建模。

## 相关页面
- [[LA-ADMM-V2G微电网经济调度-摘要]]
- [[ADMM分布式经济调度-摘要]]
- [[分布式V2G时变网络经济调度-摘要]]
