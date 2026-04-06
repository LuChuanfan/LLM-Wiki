# LLM Wiki 个人知识库设计文档

## 概述

基于 Karpathy 的 LLM Wiki 模式，搭建一个综合型个人知识库。LLM（Claude Code）全自动维护，Obsidian 浏览和可视化。从新内容开始积累，不迁移旧资料。

## 目录结构

```
D:/LCF 博士研究生所用资料/LLM-Wiki/
├── .obsidian/              # Obsidian 配置（自动生成）
├── CLAUDE.md               # Schema：LLM 的行为规范
├── index.md                # 全局索引（按分类列出所有 Wiki 页面）
├── log.md                  # 操作日志（时间线：摄入、提问、巡检）
├── raw/                    # 原始素材（只读，LLM 不改）
│   ├── articles/           # 网页文章、微信文章的 Markdown
│   ├── papers/             # 论文 PDF
│   ├── notes/              # 用户自己写的笔记、想法
│   └── misc/               # 代码片段、截图、数据文件等
└── wiki/                   # LLM 生成和维护的知识页面
    ├── 博士研究/
    ├── AI与LLM/
    ├── 编程与工程/
    ├── 职业发展/
    └── 个人成长/
```

### 分层职责

| 层 | 目录 | 谁写 | 谁读 |
|---|------|------|------|
| Raw Sources | `raw/` | 用户 | LLM（只读） |
| Wiki | `wiki/` | LLM | 用户 + LLM |
| Schema | `CLAUDE.md` | 用户 + LLM 共同演化 | LLM |
| 索引 | `index.md` | LLM | 用户 + LLM |
| 日志 | `log.md` | LLM | 用户 + LLM |

## Wiki 页面格式

每个 LLM 生成的 Wiki 页面统一格式：

```markdown
---
title: 页面标题
category: 分类名
tags: [标签1, 标签2]
sources: [raw/papers/xxx.pdf]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# 页面标题

正文内容，使用 [[双向链接]] 连接相关页面。

## 来源
- [[来源摘要页]] — 说明
```

### 页面命名规范

- 中文短标题，用连字符分隔：`ADMM-算法概述.md`
- 摘要页带来源标记：`boyd2011-ADMM论文摘要.md`

### frontmatter 字段

| 字段 | 必填 | 说明 |
|------|------|------|
| title | 是 | 页面标题 |
| category | 是 | 所属分类（5 选 1） |
| tags | 是 | 标签数组，便于 Dataview 查询 |
| sources | 否 | 关联的 raw/ 素材路径 |
| created | 是 | 创建日期 |
| updated | 是 | 最后更新日期 |

## 三大操作流程

### 1. 摄入（Ingest）

用户把素材放入 `raw/` 对应子目录，告诉 Claude Code 归档。流程：

1. LLM 读完素材，与用户讨论关键要点
2. 在 `wiki/` 对应分类下创建摘要页
3. 更新或创建相关的实体页、概念页（一份素材可能触发 5-15 个页面更新）
4. 更新 `index.md`（添加新页面条目）
5. 追加记录到 `log.md`

跨分类素材：摘要页放主分类，其他分类用 `[[链接]]` 引用。

### 2. 提问（Query）

1. LLM 读 `index.md` 定位相关页面
2. 读 Wiki 页面，综合回答（带引用）
3. 有价值的回答存回 `wiki/` 作为新分析页

### 3. 巡检（Lint）

定期让 LLM 对 Wiki 做体检：

- 找矛盾（新旧内容冲突）
- 补孤立页面的链接
- 标记需要深入研究的方向
- 建议下一步可以读什么
- 输出巡检报告，用户确认后再执行修复

## 喂料格式处理

| 素材类型 | 放哪里 | 怎么处理 |
|---------|--------|---------|
| 网页/微信文章 | `raw/articles/` | Obsidian Web Clipper 抓成 .md |
| 论文 PDF | `raw/papers/` | Claude Code 直接读 PDF |
| 自己的笔记 | `raw/notes/` | 直接写 .md 或丢进去 |
| 代码/数据/截图 | `raw/misc/` | 按需引用 |

## Schema（CLAUDE.md）核心规则

### 角色定位
- LLM 是这个 Wiki 的全职维护者，不是通用聊天机器人
- `raw/` 只读不改，`wiki/` 由 LLM 负责创建和维护

### 摄入规则
- 先读完素材，和用户讨论要点后再动手
- 每个素材必须创建一个摘要页
- 主动更新所有受影响的已有页面（新信息补充、矛盾标注）
- 跨分类素材：摘要页放主分类，其他分类用链接引用

### 维护规则
- 每次操作后必须更新 `index.md` 和 `log.md`
- 用 `[[双向链接]]` 连接所有相关页面，宁多勿少
- 绝不捏造内容，只基于 `raw/` 素材和对话中的信息
- LLM 每次更新页面时自动改 `updated` 日期

### 巡检规则
- 检查项：矛盾、孤立页面、缺失链接、过时内容、可合并的重复页面
- 输出巡检报告，用户确认后再执行修复

## 工具链

- **Obsidian** — 浏览和可视化 Wiki 的 IDE
- **Obsidian Web Clipper** — 浏览器插件，一键抓网页转 Markdown
- **Claude Code** — Wiki 的"程序员"，负责所有读写维护
- **Git** — 版本控制，整个 Wiki 是一个 Git 仓库
- **Marp**（可选）— Obsidian 插件，从 Wiki 内容生成幻灯片
- **Dataview**（可选）— Obsidian 插件，对 frontmatter 做查询

## 5 大分类

1. **博士研究** — 分布式优化、ADMM、V2G、MPC、储能等
2. **AI与LLM** — AI 行业动态、LLM 技术、工具使用心得
3. **编程与工程** — Python、MATLAB、Claude Code、开发工具链
4. **职业发展** — 实习、求职、行业认知
5. **个人成长** — 读书笔记、学习方法、思考记录

分类可随时扩展，在 CLAUDE.md 中添加即可。
