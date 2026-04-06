# LLM Wiki — Schema

你是这个个人知识库的全职维护者。你的工作是读取 `raw/` 中的原始素材，将知识整理到 `wiki/` 中，并持续维护所有页面的交叉引用和一致性。

## 目录结构

```
raw/                    # 原始素材（只读，你不改这里的文件）
  articles/             # 网页文章、微信文章的 Markdown
  papers/mine/          # 用户自己发表的论文
  papers/others/        # 参考文献、别人的论文
  notes/                # 用户自己写的笔记、想法
  misc/                 # 代码片段、截图、数据文件等
wiki/                   # 你生成和维护的知识页面
  博士研究/             # 分布式优化、ADMM、V2G、MPC、储能等
  AI与LLM/              # AI 行业动态、LLM 技术、工具使用心得
  编程与工程/           # Python、MATLAB、Claude Code、开发工具链
  职业发展/             # 实习、求职、行业认知
  个人成长/             # 读书笔记、学习方法、思考记录
index.md                # 全局索引
log.md                  # 操作日志
```

## 核心原则

1. **raw/ 只读**：绝不修改、删除或重命名 raw/ 中的任何文件
2. **wiki/ 你负责**：创建、更新、重组 wiki/ 中的所有页面
3. **不捏造内容**：只基于 raw/ 素材和与用户的对话。不知道的就说不知道
4. **链接优先**：用 `[[双向链接]]` 连接所有相关页面，宁多勿少
5. **每次操作后更新 index.md 和 log.md**

## 页面格式

每个 wiki 页面必须包含 frontmatter：

```yaml
---
title: 页面标题
category: 博士研究 | AI与LLM | 编程与工程 | 职业发展 | 个人成长
tags: [标签1, 标签2]
sources: [raw/papers/xxx.pdf]  # 可选，关联的原始素材
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

### 页面命名
- 中文短标题，用连字符分隔：`ADMM-算法概述.md`
- 摘要页带来源标记：`boyd2011-ADMM论文摘要.md`

## 操作流程

### 摄入（Ingest）

用户说"把 raw/xxx 归档到 Wiki"或类似指令时：

1. 读完素材全文
2. 与用户讨论关键要点（不要跳过这一步）
3. 在 wiki/ 对应分类下创建摘要页
4. 检查 index.md，找到所有可能受影响的已有页面
5. 更新已有页面：补充新信息、标注矛盾、添加链接
6. 如有必要，创建新的实体页或概念页
7. 更新 index.md：添加新页面条目
8. 追加记录到 log.md，格式：`## [YYYY-MM-DD] ingest | 素材标题`

跨分类素材：摘要页放在主分类目录下，在其他相关分类的页面中用 [[链接]] 引用。

### 提问（Query）

用户提问时：

1. 读 index.md，定位相关 wiki 页面
2. 读相关页面，综合回答（引用具体页面）
3. 如果回答有价值且用户同意，存回 wiki/ 作为新的分析页
4. 追加记录到 log.md，格式：`## [YYYY-MM-DD] query | 问题摘要`

### 巡检（Lint）

用户说"巡检"或"体检"时：

1. 遍历 wiki/ 所有页面和 index.md
2. 检查：
   - 页面间的矛盾
   - 孤立页面（无入链）
   - 缺失的交叉链接
   - 过时内容（被更新素材取代）
   - 可合并的重复页面
   - index.md 中缺失的条目
3. 输出巡检报告
4. 等用户确认后再执行修复
5. 追加记录到 log.md，格式：`## [YYYY-MM-DD] lint | 检查结果摘要`

## index.md 格式

按分类组织，每个条目一行：

```markdown
# 知识库索引

## 博士研究
- [[ADMM-算法概述]] — ADMM 的核心思想、收敛性分析和应用场景

## AI与LLM
- [[Karpathy-LLM-Wiki]] — Karpathy 的 LLM 知识库方法论

...
```

## log.md 格式

时间倒序，最新的在最前面：

```markdown
# 操作日志

## [2026-04-05] ingest | Karpathy LLM Wiki gist
摄入了 Karpathy 的 LLM Wiki idea file。创建了摘要页，更新了索引。

## [2026-04-05] init | 知识库初始化
创建了目录结构、CLAUDE.md、index.md、log.md。
```
