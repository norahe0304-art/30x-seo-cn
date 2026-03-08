---
name: 30x-seo-content-writer
description: >
  SEO-optimized content generation. Two modes: plan mode (reads seo-plan
  output) or standalone mode (user provides keyword directly). Outputs
  markdown files. Use when user says "write SEO blog", "generate SEO content",
  "create blog post", or "SEO article".
allowed-tools:
  - WebFetch
  - Read
---

# SEO Content Writer

## What This Skill Does

生成 SEO 优化的博客文章。

## Two Modes（两种模式）

| 模式 | 输入 | 适用场景 |
|------|------|---------|
| **计划模式** | seo-plan 输出文件 | 有完整 SEO 策略，按日历写作 |
| **独立模式** | 用户提供关键词 | 快速写一篇文章，无需完整规划 |

---

## Mode 1: Plan Mode（计划模式）

### Prerequisites

已有 SEO 计划（`/seo plan`）：
- `CONTENT-CALENDAR.md` - 内容日历
- `SEO-STRATEGY.md` - 关键词和主题策略

### Process

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   seo-plan      │     │                 │     │                 │
│   输出文件      │ ──> │    Generate     │ ──> │   Markdown      │
│ CONTENT-CALENDAR│     │   SEO Content   │     │   博客文章      │
│ SEO-STRATEGY    │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

### Context from Plan

| 信息 | 来源 | 用途 |
|------|------|------|
| **目标关键词** | SEO-STRATEGY.md | 标题、H2、正文优化 |
| **主题集群** | SEO-STRATEGY.md | 内链规划 |
| **竞品分析** | COMPETITOR-ANALYSIS.md | 差异化角度 |

---

## Mode 2: Standalone Mode（独立模式）

### When to Use

- 只想快速写一篇文章
- 没有完整的 SEO 计划
- 已经知道目标关键词

### Required Input

问用户：

1. **Topic/Title**: 文章主题
2. **Target Keyword**: 主关键词
3. **Secondary Keywords**: 次要关键词（可选）
4. **Search Intent**: Informational / Commercial / Transactional
5. **Target Length**: Short (800-1200) / Medium (1500-2000) / Long (2500+)
6. **CTA Goal**: 读者应采取什么行动？

---

## Content Generation（内容生成）

### Article Structure

```markdown
# [H1: Include primary keyword, 50-60 chars]

[Hook: Engaging first paragraph, mention keyword naturally]

## [H2: Section with keyword variation]

[Content with semantic keywords, 2-4 paragraphs]

### [H3: Subsection if needed]

[Supporting content]

## [H2: Another main section]

[Continue pattern...]

## Conclusion / Key Takeaways

[Summary, reiterate value, include CTA]
```

### SEO Requirements Checklist

| Element | Requirement |
|---------|-------------|
| **Title (H1)** | Include primary keyword, 50-60 characters |
| **Meta Description** | Include keyword, 150-160 characters, compelling |
| **URL Slug** | Short, keyword-rich, hyphenated |
| **First 100 Words** | Include primary keyword naturally |
| **Headings** | H2s include keyword variations, logical hierarchy |
| **Keyword Density** | 1-2%, natural placement |
| **Internal Links** | 3-5 relevant internal links (placeholder: [Internal: topic]) |
| **External Links** | 2-3 authoritative sources |
| **Images** | Suggest placements with alt text descriptions |
| **Readability** | Short paragraphs, bullet lists, scannable |

### E-E-A-T Signals to Include

| Signal | How to Include |
|--------|----------------|
| **Experience** | First-hand examples, case studies, "we tested" |
| **Expertise** | Technical depth, accurate information, citations |
| **Authoritativeness** | Cite reputable sources, link to studies |
| **Trustworthiness** | Clear attribution, honest claims, no exaggeration |

### AI Citation Readiness (GEO)

For AI search visibility:
- Include clear, quotable definitions
- Use structured formats (tables, lists)
- Answer questions directly in the first sentence
- Include specific data points and statistics

---

## Output Format

### Deliverables

1. **Blog Article** (Markdown format)
   - Full article with SEO optimization
   - Meta title and description
   - Suggested URL slug

2. **SEO Checklist** (verification)
   - [ ] Primary keyword in title
   - [ ] Primary keyword in first 100 words
   - [ ] H2s with keyword variations
   - [ ] Internal link placeholders
   - [ ] External authoritative links
   - [ ] Image suggestions with alt text
   - [ ] CTA included

---

## Commands

| 命令 | 模式 |
|------|------|
| `/seo content-writer` | 自动检测（有 seo-plan 输出则计划模式，否则独立模式）|
| `/seo content-writer "topic"` | 独立模式，直接指定主题 |

---

## Integration with Other Skills

| Skill | When to Use |
|-------|-------------|
| **seo-plan** | 先制定计划，再用计划模式生成内容 |
| **seo-internal-links suggest** | 写完后生成内链建议 |
| **seo-content-audit** | 写完后审计质量 |

---

## Quality Gates

### Before Generation
- [ ] Target keyword confirmed
- [ ] Search intent understood
- [ ] Length decided

### After Generation
- [ ] Keyword naturally integrated (not stuffed)
- [ ] E-E-A-T signals present
- [ ] Readability appropriate for audience
- [ ] CTA aligned with business goal
- [ ] No factual claims without sources

[PROTOCOL]: 变更时更新此头部，然后检查 CLAUDE.md
