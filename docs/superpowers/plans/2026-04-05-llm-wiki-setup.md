# LLM Wiki 个人知识库搭建 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 搭建基于 Karpathy LLM Wiki 模式的个人知识库框架，包括目录结构、CLAUDE.md schema、Git 初始化、Obsidian vault 配置，并完成一次端到端的素材摄入验证。

**Architecture:** 三层架构（raw 原始素材 / wiki LLM 维护的知识页面 / CLAUDE.md schema），Obsidian 做浏览 IDE，Claude Code 做维护者，Git 做版本控制。所有内容基于 Markdown 文件，无数据库。

**Tech Stack:** Obsidian, Git, Claude Code, Markdown

---

### Task 1: 创建目录结构

**Files:**
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/raw/articles/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/raw/papers/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/raw/notes/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/raw/misc/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/博士研究/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/AI与LLM/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/编程与工程/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/职业发展/.gitkeep`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/个人成长/.gitkeep`

- [ ] **Step 1: 创建所有目录和 .gitkeep 占位文件**

```bash
cd "D:/LCF 博士研究生所用资料/LLM-Wiki"
mkdir -p raw/articles raw/papers raw/notes raw/misc
mkdir -p "wiki/博士研究" "wiki/AI与LLM" "wiki/编程与工程" "wiki/职业发展" "wiki/个人成长"
touch raw/articles/.gitkeep raw/papers/.gitkeep raw/notes/.gitkeep raw/misc/.gitkeep
touch "wiki/博士研究/.gitkeep" "wiki/AI与LLM/.gitkeep" "wiki/编程与工程/.gitkeep" "wiki/职业发展/.gitkeep" "wiki/个人成长/.gitkeep"
```

- [ ] **Step 2: 验证目录结构**

```bash
find "D:/LCF 博士研究生所用资料/LLM-Wiki" -type d | sort
```

Expected: 应该看到 raw/ 下 4 个子目录，wiki/ 下 5 个分类子目录，加上 docs/ 目录。

---

### Task 2: 创建 CLAUDE.md（Schema）

**Files:**
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/CLAUDE.md`

- [ ] **Step 1: 写入 CLAUDE.md**

```markdown
# LLM Wiki — Schema

你是这个个人知识库的全职维护者。你的工作是读取 `raw/` 中的原始素材，将知识整理到 `wiki/` 中，并持续维护所有页面的交叉引用和一致性。

## 目录结构

```
raw/                    # 原始素材（只读，你不改这里的文件）
  articles/             # 网页文章、微信文章的 Markdown
  papers/               # 论文 PDF
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
- [[V2G-充放电优化]] — 电动汽车参与电网调度的优化方法

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
```

- [ ] **Step 2: 验证 CLAUDE.md 已创建**

```bash
head -5 "D:/LCF 博士研究生所用资料/LLM-Wiki/CLAUDE.md"
```

Expected: 显示 `# LLM Wiki — Schema` 开头的内容。

---

### Task 3: 创建 index.md 和 log.md

**Files:**
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/index.md`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/log.md`

- [ ] **Step 1: 创建 index.md**

```markdown
# 知识库索引

## 博士研究

（暂无条目）

## AI与LLM

（暂无条目）

## 编程与工程

（暂无条目）

## 职业发展

（暂无条目）

## 个人成长

（暂无条目）
```

- [ ] **Step 2: 创建 log.md**

```markdown
# 操作日志

## [2026-04-05] init | 知识库初始化
创建了目录结构、CLAUDE.md、index.md、log.md。5 个分类：博士研究、AI与LLM、编程与工程、职业发展、个人成长。
```

- [ ] **Step 3: 验证两个文件**

```bash
cat "D:/LCF 博士研究生所用资料/LLM-Wiki/index.md"
cat "D:/LCF 博士研究生所用资料/LLM-Wiki/log.md"
```

Expected: index.md 有 5 个分类标题，log.md 有一条 init 记录。

---

### Task 4: 创建 .gitignore 并初始化 Git 仓库

**Files:**
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/.gitignore`

- [ ] **Step 1: 创建 .gitignore**

```
# Obsidian
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/*/data.json
.trash/

# OS
Thumbs.db
.DS_Store

# Temp
*.tmp
~$*
```

- [ ] **Step 2: 初始化 Git 仓库并提交**

```bash
cd "D:/LCF 博士研究生所用资料/LLM-Wiki"
git init
git add -A
git commit -m "init: 搭建 LLM Wiki 个人知识库框架"
```

Expected: 提交成功，包含 CLAUDE.md、index.md、log.md、.gitignore 和各目录的 .gitkeep。

- [ ] **Step 3: 验证 Git 状态**

```bash
cd "D:/LCF 博士研究生所用资料/LLM-Wiki" && git log --oneline
```

Expected: 显示一条 init 提交。

---

### Task 5: 配置 Obsidian Vault

这个任务需要用户在 Obsidian 中手动操作，Claude Code 提供指引。

- [ ] **Step 1: 在 Obsidian 中打开 LLM-Wiki 为新 Vault**

指引用户：
1. 打开 Obsidian
2. 左下角点击 Vault 图标（保险柜图标）
3. 选择 "Open folder as vault"
4. 选择 `D:\LCF 博士研究生所用资料\LLM-Wiki`
5. 点击 "Open"

- [ ] **Step 2: 验证 Vault 已加载**

```bash
ls "D:/LCF 博士研究生所用资料/LLM-Wiki/.obsidian/" 2>/dev/null && echo "VAULT_OK" || echo "VAULT_NOT_FOUND"
```

Expected: `VAULT_OK`（Obsidian 会自动创建 .obsidian/ 目录）

- [ ] **Step 3: 安装 Obsidian Web Clipper 浏览器插件**

指引用户：
1. 在 Chrome 中打开扩展商店，搜索 "Obsidian Web Clipper"
2. 安装官方插件（开发者：Obsidian）
3. 安装后点击插件图标，选择 LLM-Wiki 这个 Vault 作为目标
4. 设置默认保存路径为 `raw/articles/`

---

### Task 6: 端到端验证 — 摄入 Karpathy LLM Wiki gist

用之前已经拿到的 Karpathy gist 内容做第一次完整的摄入操作，验证整套流程。

**Files:**
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/raw/articles/karpathy-llm-wiki-gist.md`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/AI与LLM/Karpathy-LLM-Wiki-方法论摘要.md`
- Create: `D:/LCF 博士研究生所用资料/LLM-Wiki/wiki/AI与LLM/LLM-知识库-概念.md`
- Modify: `D:/LCF 博士研究生所用资料/LLM-Wiki/index.md`
- Modify: `D:/LCF 博士研究生所用资料/LLM-Wiki/log.md`

- [ ] **Step 1: 保存原始素材到 raw/**

将 Karpathy 的 gist 全文保存为 `raw/articles/karpathy-llm-wiki-gist.md`。内容就是之前获取的 gist 原文（75 行 Markdown），不做任何修改。

- [ ] **Step 2: 创建摘要页**

在 `wiki/AI与LLM/` 下创建 `Karpathy-LLM-Wiki-方法论摘要.md`：

```markdown
---
title: Karpathy LLM Wiki 方法论摘要
category: AI与LLM
tags: [LLM, 知识管理, Obsidian, Karpathy, RAG]
sources: [raw/articles/karpathy-llm-wiki-gist.md]
created: 2026-04-05
updated: 2026-04-05
---

# Karpathy LLM Wiki 方法论摘要

Andrej Karpathy 于 2026 年 4 月提出的个人知识库构建方法。核心思想：让 LLM 增量构建和维护一个持久化的 Markdown Wiki，而非每次查询都从头做 RAG 检索。

## 核心理念

传统 RAG 每次提问都从头发现知识，没有积累。LLM Wiki 的做法不同：LLM 读完原始资料后，主动提取关键信息，整合到一个持续维护的 Wiki 中。知识被"编译"一次后持续保鲜。

## 三层架构

- **Raw Sources**（原始素材）：只读，LLM 不改
- **Wiki**（知识页面）：LLM 生成和维护的 Markdown 文件
- **Schema**（配置文件）：告诉 LLM 如何组织 Wiki 的规范（如 CLAUDE.md）

## 三大操作

1. **摄入（Ingest）**：新素材 → LLM 读取 → 创建摘要 → 更新相关页面（一份素材可能触及 10-15 个页面）
2. **提问（Query）**：LLM 搜索 Wiki 页面 → 综合回答 → 好的回答归档回 Wiki
3. **巡检（Lint）**：定期检查矛盾、孤立页面、缺失链接

## Karpathy 的实践

- 使用 Obsidian 做浏览 IDE，LLM Agent 做编辑
- 一个研究方向积累了约 100 篇文章、40 万字
- 不需要花哨的 RAG，LLM 自己维护索引就够了
- 推荐工具：Obsidian Web Clipper、qmd 搜索引擎、Marp 幻灯片、Dataview 查询

## 关键洞察

> "人类放弃维护知识库，是因为维护成本增长得比价值快。LLM 不会厌倦、不会忘记更新交叉引用、一次可以改 15 个文件。"

这个理念与 1945 年 Vannevar Bush 提出的 Memex 概念一脉相承——私人的、经过整理的知识库。Bush 没能解决的"谁来做维护"的问题，81 年后由 LLM 解决了。

## 相关
- [[LLM-知识库-概念]]

## 来源
- [Karpathy gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [X 帖子](https://x.com/karpathy/status/2039805659525644595)
```

- [ ] **Step 3: 创建概念页**

在 `wiki/AI与LLM/` 下创建 `LLM-知识库-概念.md`：

```markdown
---
title: LLM 知识库
category: AI与LLM
tags: [LLM, 知识管理, RAG, Wiki]
created: 2026-04-05
updated: 2026-04-05
---

# LLM 知识库

一种用 LLM 增量构建和维护的个人知识管理系统。与传统 RAG（每次查询从头检索）不同，LLM 知识库将知识"编译"成结构化的 Markdown 文件，持续更新和保鲜。

## 与 RAG 的对比

| 维度 | 传统 RAG | LLM 知识库 |
|------|----------|-----------|
| 知识积累 | 每次从头检索，无积累 | 增量编译，持续积累 |
| 交叉引用 | 无 | 自动维护双向链接 |
| 可见性 | 黑箱（嵌入向量） | 透明（Markdown 文件） |
| 维护成本 | 低（但质量也低） | 趋近于零（LLM 代劳） |
| 数据所有权 | 依赖平台 | 本地文件，完全可控 |

## 代表实践
- [[Karpathy-LLM-Wiki-方法论摘要]] — Karpathy 的原创方法论

## 相关概念
- RAG（Retrieval-Augmented Generation）
- Obsidian
- Memex（Vannevar Bush, 1945）
```

- [ ] **Step 4: 更新 index.md**

将 index.md 的 `## AI与LLM` 部分更新为：

```markdown
## AI与LLM

- [[Karpathy-LLM-Wiki-方法论摘要]] — Karpathy 的 LLM 知识库方法论：三层架构、三大操作、实践经验
- [[LLM-知识库-概念]] — LLM 增量维护的个人知识管理系统，与 RAG 的对比
```

- [ ] **Step 5: 更新 log.md**

在 log.md 的 `# 操作日志` 标题后、init 记录之前，插入新记录：

```markdown
## [2026-04-05] ingest | Karpathy LLM Wiki gist
摄入了 Karpathy 的 LLM Wiki idea file（gist）。创建了方法论摘要页和 LLM 知识库概念页，更新了索引。
```

- [ ] **Step 6: 在 Obsidian 中验证**

指引用户：
1. 在 Obsidian 中打开 LLM-Wiki vault
2. 检查 wiki/AI与LLM/ 下能看到两个新页面
3. 点击页面中的 [[双向链接]]，确认能正常跳转
4. 打开图谱视图（左侧栏图标），确认两个页面有连线

- [ ] **Step 7: Git 提交**

```bash
cd "D:/LCF 博士研究生所用资料/LLM-Wiki"
git add -A
git commit -m "feat: 第一次素材摄入 — Karpathy LLM Wiki gist"
```

Expected: 提交成功，包含 raw/ 素材、两个 wiki 页面、更新的 index.md 和 log.md。

---

### Task 7: 安装 Obsidian 社区插件（可选）

用户在 Obsidian 中手动操作。

- [ ] **Step 1: 启用社区插件**

指引用户：
1. Obsidian → Settings (齿轮图标)
2. Community plugins → Turn on community plugins
3. 点击 Browse

- [ ] **Step 2: 安装 Dataview**

搜索 "Dataview"，安装并启用。Dataview 可以对 frontmatter 字段做查询，例如在任意页面插入：

````markdown
```dataview
TABLE tags, updated
FROM "wiki"
WHERE category = "博士研究"
SORT updated DESC
```
````

这会生成一个动态表格，列出"博士研究"分类下的所有页面。

- [ ] **Step 3: 配置 Obsidian 附件路径**

指引用户：
1. Settings → Files and links
2. "Default location for new attachments" 设为 "In the folder specified below"
3. "Attachment folder path" 设为 `raw/misc`

这样在 Obsidian 中粘贴的图片会自动存到 raw/misc/。
