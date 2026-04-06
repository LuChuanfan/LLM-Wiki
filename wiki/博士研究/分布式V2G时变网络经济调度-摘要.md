---
title: 分布式V2G时变网络经济调度
category: 博士研究
tags: [ADMM, V2G, 分布式优化, 经济调度, 时变网络, MPC, 自己的论文]
sources: [raw/papers/mine/Distributed economic dispatch for microgrids with vehicle-to-grid undertime-varying network_Acccepted.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# 分布式V2G时变网络经济调度

**论文信息：** Chuan-Fan Lu, Guo-Ping Liu, Rui Yan, Jinqiang Cui. Journal of Energy Storage, Vol. 147, 2026.

## 核心思想

针对含V2G的微电网经济调度中集中式方法鲁棒性差、通信计算开销大、隐私保护不足等问题，提出全分布式经济调度方法。

## 核心方法

- 将V2G的MIQP问题转化为凸二次规划（通过放松互补约束并证明等价性）
- 分布式ADMM求解 + 时变网络补偿机制
- MPC滚动优化处理EV即插即用的不确定性
- **调度包策略**：将多步控制信号打包，减少优化触发频率
- CC-CV充电约束和充放电效率因子的建模与嵌入

## 主要贡献

- 将V2G的MIQP问题简化为凸二次规划，由分布式ADMM求解
- 提出MPC调度包策略处理EV即插即用和时变网络
- CC-CV充电模式和电池充放电效率因子作为关键约束纳入优化
- 通过仿真和树莓派硬件实验平台验证
- 提供时变网络下算法收敛至最优解的理论证明

## 与其他工作的关系

本文是 [[LA-ADMM-V2G微电网经济调度-摘要]] 的基础版本/前期工作。后者在本文的ADMM+MPC+调度包框架上进一步引入DNN学习加速（热启动），实现了70.9%的迭代削减。本文发表于JES，后者发表于IEEE TSG，体现递进式研究路线。

## 相关页面
- [[LA-ADMM-V2G微电网经济调度-摘要]]
- [[ADMM分布式经济调度-摘要]]
- [[CMPC-V2G充放电调度-摘要]]
