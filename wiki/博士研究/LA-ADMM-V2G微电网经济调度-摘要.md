---
title: 学习加速ADMM的V2G微电网经济调度
category: 博士研究
tags: [ADMM, 深度学习, V2G, 分布式优化, 经济调度, 时变网络, MPC, 自己的论文]
sources: [raw/papers/mine/Learning-Accelerated_Distributed_Economic_Dispatch_in_Vehicle-to-Grid_Integrated_Microgrids_Pubulished.pdf]
created: 2026-04-06
updated: 2026-04-06
---

# 学习加速ADMM的V2G微电网经济调度

**论文信息：** Chuan-Fan Lu, Guo-Ping Liu (IEEE Fellow), Jinqiang Cui, Jiankun Yang. IEEE Transactions on Smart Grid, Vol. 16, No. 6, November 2025.

## 核心思想

针对含V2G的微电网分布式经济调度面临的通信计算负担重、EV充电不确定性及电池寿命退化等挑战，提出一种**学习加速的分布式优化框架（LA-ADMM）**。

## 核心方法

- **LA-ADMM**：用深度神经网络预测最优对偶变量实现热启动，加速ADMM收敛
- 时变通信网络下的ADMM收敛性证明（含节点/链路随机失效）
- MPC滚动优化 + **调度包（Dispatch Package）策略**：稳态时复用历史解，减少不必要重计算
- CC-CV充电协议的分段线性近似，作为运行约束嵌入优化

## 主要贡献

- 提出LA-ADMM，迭代次数较传统ADMM-MPC**减少70.9%**
- 提出MPC调度包策略，动态复用历史优化结果
- 将CC-CV充电协议以物理约束形式嵌入优化框架
- 8个树莓派节点的硬件在环实验，仿真与实物功率偏差**<2%**

## 与其他工作的关系

本文是 [[ADMM分布式经济调度-摘要]] 的直接升级版，新增DNN学习加速。与 [[分布式V2G时变网络经济调度-摘要]] 共享相同的问题建模和硬件平台，但发表在更高级别的IEEE TSG上，体现了从基础方法到学习增强方法的递进式研究路线。

## 相关页面
- [[ADMM分布式经济调度-摘要]]
- [[CMPC-V2G充放电调度-摘要]]
- [[分布式V2G时变网络经济调度-摘要]]
