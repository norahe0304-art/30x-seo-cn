---
name: 30x-seo-plan
description: >
  SEO strategy planning: competitor analysis, keyword strategy, content
  calendar, and implementation roadmap. Use when user says "SEO plan",
  "SEO strategy", "content calendar", or "SEO roadmap".
allowed-tools:
  - WebFetch
  - Read
---

# SEO Plan（SEO 策略规划）

## What This Skill Does

制定 SEO 策略：分析竞品、规划关键词、制定内容日历、输出实施路线图。

**不做的事**：
- 网站架构设计 → 用 `site-architecture`
- 技术 SEO 检查 → 用 `seo-technical`
- 内容生成 → 用 `seo-content-writer`

---

## Optional Input

| 输入 | 来源 | 说明 |
|------|------|------|
| **seo-keywords 输出** | `/seo keywords` | 如果已有关键词研究，读取作为策略输入 |

> 不是强制依赖。可以先规划再研究，也可以先研究再规划。

---

## Process

### Step 1: Discovery（收集信息）

问用户：
- 业务类型（SaaS / 电商 / 本地服务 / 媒体 / 其他）
- 目标受众（谁是你的客户？）
- 主要竞品（3-5 个）
- 目标（流量？转化？品牌？）
- 现有网站？（有 → 分析现状；没有 → 新站规划）

### Step 2: Competitor Analysis（竞品分析）

对每个竞品，分析：

| 维度 | 检查项 |
|------|--------|
| **内容** | 有哪些页面？博客频率？内容深度？|
| **关键词** | 排名哪些词？内容主题？|
| **E-E-A-T** | 作者信息？专家背书？信任信号？|
| **结构** | URL 层级？导航设计？|

工具：WebFetch + Perplexity

输出：`COMPETITOR-ANALYSIS.md`

### Step 3: Keyword Strategy（关键词策略）

如果有 seo-keywords 输出 → 读取并整合
如果没有 → 基于竞品分析 + 用户输入推断

确定：
- 核心关键词（3-5 个）
- 长尾关键词（10-20 个）
- 主题集群（Topic Clusters）

输出：整合到 `SEO-STRATEGY.md`

### Step 4: Content Planning（内容规划）

基于关键词策略，规划：

| 内容类型 | 示例 |
|---------|------|
| **支柱页** | 核心主题的权威长文 |
| **集群页** | 围绕支柱的细分文章 |
| **博客** | 定期更新的内容 |

输出：`CONTENT-CALENDAR.md`

```markdown
# Content Calendar

## Month 1
| Week | Topic | Target Keyword | Type | Priority |
|------|-------|----------------|------|----------|
| 1 | ... | ... | Pillar | High |
| 2 | ... | ... | Cluster | Medium |
```

### Step 5: Implementation Roadmap（实施路线）

简化版路线图：

| 阶段 | 时间 | 重点 |
|------|------|------|
| **启动** | Week 1-2 | 技术基础（→ seo-technical）、核心页面 |
| **内容** | Week 3-8 | 按日历发布内容（→ seo-content-writer）|
| **优化** | Week 9-12 | 监控排名、调整策略 |

输出：`IMPLEMENTATION-ROADMAP.md`

---

## Output（输出文件）

| 文件 | 内容 |
|------|------|
| `SEO-STRATEGY.md` | 完整策略：目标、关键词、主题集群 |
| `COMPETITOR-ANALYSIS.md` | 竞品分析报告 |
| `CONTENT-CALENDAR.md` | 内容日历（供 seo-content-writer 使用）|
| `IMPLEMENTATION-ROADMAP.md` | 实施路线图 |

---

## Integration（与其他技能的关系）

```
seo-keywords ──(可选)──> seo-plan
                            │
                            ├──> seo-content-writer（内容生成）
                            ├──> site-architecture（架构设计）
                            └──> seo-technical（技术检查）
```

| 技能 | 何时使用 |
|------|---------|
| `seo-keywords` | 规划前做关键词研究 |
| `site-architecture` | 需要详细架构设计时 |
| `seo-content-writer` | 按日历生成内容 |
| `seo-technical` | 检查技术基础 |

---

## Example

```
User: /seo plan
Claude: 请告诉我：
1. 业务类型？
2. 目标受众？
3. 主要竞品？
4. SEO 目标？

User: SaaS 项目管理工具，目标是中小企业，竞品是 Asana、Monday、Notion

Claude: [执行竞品分析...]
        [制定关键词策略...]
        [规划内容日历...]
        [输出 4 个文件]
```

[PROTOCOL]: 变更时更新此头部，然后检查 CLAUDE.md
