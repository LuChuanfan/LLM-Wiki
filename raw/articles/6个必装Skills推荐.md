---
title: 分享6个我觉得应该必装的Skills
source: https://mp.weixin.qq.com/s/udSpp7eMqwiRo5yVShRzLw
author: 卡兹克、可达
created: 2026-04-06
---

# 分享6个我觉得应该必装的Skills

## 一. Frontend Design
- Anthropic 官方插件网站排名第一
- 链接：https://github.com/anthropics/skills/tree/main/skills/frontend-design
- 解决 AI 做前端的品味问题：禁止 Inter/Roboto/Arial 烂大街字体，禁止紫色渐变配白底
- 要求 AI 写代码前先想清楚美学方向（极简主义、复古未来风等），排版、留白、字体、动效围绕方向来
- 能力越差的模型，效果提升越明显

## 二. 办公必备四件套（docx/xlsx/pdf/pptx）
- Anthropic 官方出品
- 链接：https://github.com/anthropics/skills/tree/main/skills
- 不装时 Agent 每次现写代码从零摸索排版，效果随机
- 装上后自带文档处理流程和代码模板（页面大小、宽度、图片类型等）
- 实测对比：论文笔记从"一坨"变成统一色调、页眉页脚齐全的专业文档
- 可叠加 Frontend Design 一起用，PPT 颜值再上台阶

## 三. Web Access Skill
- 作者：@一泽
- 链接：https://github.com/eze-is/web-access
- 通过 Chrome DevTools Protocol 直连本地 Chrome，带登录态
- 可访问小红书、B站、微博、飞书等站内内容
- 支持 Jina 中间层预处理，节省 token
- 自动沉淀每个网站的操作经验（按域名存操作记录）
- 多 Agent 并行操作不同浏览器标签页
- 需要 Chrome 最新版 + 允许远程调试（chrome://inspect/#remote-debugging）

## 四. PUA
- 链接：https://github.com/tanweai/pua
- 解决 AI 摆烂问题：试两三次没搞定就说"建议您手动检查"
- 四级压力升级机制：同一思路原地打转时强制打断，执行 7 项检查清单，逼换思路
- v3 版本根据任务类型自动选方法论（阿里/字节/华为/腾讯/Netflix/Apple 等十几家）
- 建议不开默认模式，卡住时手动 /pua

## 五. Claude-mem
- 链接：https://github.com/thedotmack/claude-mem
- 解决记忆持久化：自动记录对话关键信息，新会话自动注入相关上下文
- 三层渐进式检索：索引 → 时间线上下文 → 完整细节（省 Token）
- 本地 Web 界面 localhost:37777 查看记忆内容
- 隐私控制：<private>标签跳过敏感内容

## 六. Skill-Creator
- 链接：https://claude.com/plugins/skill-creator
- 作者认为最重要的 Skill
- 帮你把自己的需求和经验封装成 Skills
- 核心观点：最牛的 skill 永远是你自己造的那个
- 通用技能在贬值，"知道自己需要什么"的能力在升值
