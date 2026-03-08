---
name: 30x-seo-content-audit
description: >
  Content quality audit for both traditional SEO (E-E-A-T) and AI search
  (citability, structure, authority). Use when user says "content audit",
  "content quality", "E-E-A-T", "AI citability", "content analysis", or
  "is my content good for SEO".
allowed-tools:
  - WebFetch
  - Read
---

# Content Quality Audit

> 同时检查传统 SEO（E-E-A-T）和 AI 搜索（可引用性）

## 两个维度

| 维度 | 目标 | 关键指标 |
|------|------|----------|
| **传统 SEO** | Google 排名 | E-E-A-T 评分、关键词、结构 |
| **AI 可引用性** | ChatGPT/Perplexity 引用 | 可提取性、权威信号、第三方存在 |

---

## Part 1: 传统 SEO - E-E-A-T 分析

## E-E-A-T Framework (updated Sept 2025 QRG)

Read `seo/references/eeat-framework.md` for full criteria.

### Experience (first-hand signals)
- Original research, case studies, before/after results
- Personal anecdotes, process documentation
- Unique data, proprietary insights
- Photos/videos from direct experience

### Expertise
- Author credentials, certifications, bio
- Professional background relevant to topic
- Technical depth appropriate for audience
- Accurate, well-sourced claims

### Authoritativeness
- External citations, backlinks from authoritative sources
- Brand mentions, industry recognition
- Published in recognized outlets
- Cited by other experts

### Trustworthiness
- Contact information, physical address
- Privacy policy, terms of service
- Customer testimonials, reviews
- Date stamps, transparent corrections
- Secure site (HTTPS)

## Content Metrics

### Word Count Analysis
Compare against page type minimums:
| Page Type | Minimum |
|-----------|---------|
| Homepage | 500 |
| Service page | 800 |
| Blog post | 1,500 |
| Product page | 300+ (400+ for complex products) |
| Location page | 500-600 |

> **Important:** These are **topical coverage floors**, not targets. Google has confirmed word count is NOT a direct ranking factor. The goal is comprehensive topical coverage — a 500-word page that thoroughly answers the query will outrank a 2,000-word page that doesn't. Use these as guidelines for adequate coverage depth, not rigid requirements.

### Readability
- Flesch Reading Ease: target 60-70 for general audience

> **Note:** Flesch Reading Ease is a useful proxy for content accessibility but is NOT a direct Google ranking factor. John Mueller has confirmed Google does not use basic readability scores for ranking. Yoast deprioritized Flesch scores in v19.3. Use readability analysis as a content quality indicator, not as an SEO metric to optimize directly.
- Grade level: match target audience
- Sentence length: average 15-20 words
- Paragraph length: 2-4 sentences

### Keyword Optimization
- Primary keyword in title, H1, first 100 words
- Natural density (1-3%)
- Semantic variations present
- No keyword stuffing

### Content Structure
- Logical heading hierarchy (H1 → H2 → H3)
- Scannable sections with descriptive headings
- Bullet/numbered lists where appropriate
- Table of contents for long-form content

### Multimedia
- Relevant images with proper alt text
- Videos where appropriate
- Infographics for complex data
- Charts/graphs for statistics

### Internal Linking
- 3-5 relevant internal links per 1000 words
- Descriptive anchor text
- Links to related content
- No orphan pages

### External Linking
- Cite authoritative sources
- Open in new tab for user experience
- Reasonable count (not excessive)

## AI Content Assessment (Sept 2025 QRG addition)

Google's raters now formally assess whether content appears AI-generated.

### Acceptable AI Content
- Demonstrates genuine E-E-A-T
- Provides unique value
- Has human oversight and editing
- Contains original insights

### Low-Quality AI Content Markers
- Generic phrasing, lack of specificity
- No original insight
- Repetitive structure across pages
- No author attribution
- Factual inaccuracies

> **Helpful Content System (March 2024):** The Helpful Content System was merged into Google's core ranking algorithm during the March 2024 core update. It no longer operates as a standalone classifier. Helpfulness signals are now weighted within every core update — the same principles apply (people-first content, demonstrating E-E-A-T, satisfying user intent), but enforcement is continuous rather than through separate HCU updates.

## AI Citation Readiness (GEO signals)

Optimize for AI search engines (ChatGPT, Perplexity, Google AI Overviews):

- Clear, quotable statements with statistics/facts
- Structured data (especially for data points)
- Strong heading hierarchy (H1→H2→H3 flow)
- Answer-first formatting for key questions
- Tables and lists for comparative data
- Clear attribution and source citations

### AI Search Visibility & GEO (2025-2026)

**Google AI Mode** launched publicly in May 2025 as a separate tab in Google Search, available in 180+ countries. Unlike AI Overviews (which appear above organic results), AI Mode provides a fully conversational search experience with **zero organic blue links** — making AI citation the only visibility mechanism.

**Key optimization strategies for AI citation:**
- **Structured answers:** Clear question-answer formats, definition patterns, and step-by-step instructions that AI systems can extract and cite
- **First-party data:** Original research, statistics, case studies, and unique datasets are highly cited by AI systems
- **Schema markup:** Article, FAQ (for non-Google AI platforms), and structured content schemas help AI systems parse and attribute content
- **Topical authority:** AI systems preferentially cite sources that demonstrate deep expertise — build content clusters, not isolated pages
- **Entity clarity:** Ensure brand, authors, and key concepts are clearly defined with structured data (Organization, Person schema)
- **Multi-platform tracking:** Monitor visibility across Google AI Overviews, AI Mode, ChatGPT, Perplexity, and Bing Copilot — not just traditional rankings. Treat AI citation as a standalone KPI alongside organic rankings and traffic.

**Generative Engine Optimization (GEO):**
GEO is the emerging discipline of optimizing content specifically for AI-generated answers. Key GEO signals include: quotability (clear, concise extractable facts), attribution (source citations within your content), structure (well-organized heading hierarchy), and freshness (regularly updated data). Cross-reference the `seo-geo` skill for detailed GEO workflows.

## Content Freshness

- Publication date visible
- Last updated date if content has been revised
- Flag content older than 12 months without update for fast-changing topics

## Output

### Content Quality Score: XX/100

### E-E-A-T Breakdown
| Factor | Score | Key Signals |
|--------|-------|-------------|
| Experience | XX/25 | ... |
| Expertise | XX/25 | ... |
| Authoritativeness | XX/25 | ... |
| Trustworthiness | XX/25 | ... |

### AI Citation Readiness: XX/100

### Issues Found
### Recommendations

---

## Part 2: AI 可引用性 - 三大支柱

> 来源：Princeton GEO 研究 + 行业最佳实践

### 支柱 1: 结构（可提取性）

AI 系统提取的是段落，不是整页。每个关键主张应该能独立成文。

| 内容块类型 | 适用场景 | 示例 |
|-----------|---------|------|
| 定义块 | "什么是 X?" | "CRM 是一种管理客户关系的软件..." |
| 步骤块 | "怎么做 X?" | "第一步...第二步...第三步..." |
| 对比表 | "X vs Y" | 功能对比表格 |
| 优缺点块 | 评估类问题 | "优点：... 缺点：..." |
| FAQ 块 | 常见问题 | Q: ... A: ... |
| 统计块 | 数据支撑 | "根据 2025 年调查，73% 的用户..." |

**结构规则**：
- 每段开头直接给答案（不要埋在后面）
- 关键段落 40-60 词（AI 提取最佳长度）
- H2/H3 标题用问句形式（匹配用户搜索）
- 对比内容用表格，步骤内容用列表

### 支柱 2: 权威（可引用性）

| 优化方法 | 可见性提升 | 怎么做 |
|---------|:----------:|--------|
| 引用来源 | +40% | 添加权威引用和链接 |
| 添加统计 | +37% | 具体数字 + 来源 |
| 专家引言 | +30% | "据 [专家] 称..." |
| 权威语气 | +25% | 展示专业知识 |
| 关键词堆砌 | **-10%** | **会降低 AI 可见性** |

**最佳组合**：流畅度 + 统计数据 = 最大提升

### 支柱 3: 存在（第三方曝光）

AI 不只引用你的网站，还引用你出现的地方。

| 平台 | AI 引用占比 | 行动 |
|------|:----------:|------|
| Wikipedia | 7.8% | 确保品牌页面准确 |
| Reddit | 1.8% | 在相关社区参与讨论 |
| YouTube | 高 | 创建视频内容 |
| 评测网站 | 中 | G2, Capterra 保持更新 |
| Quora | 中 | 深度回答相关问题 |

---

## 综合评分输出

```
内容质量审计报告

1. 传统 SEO 得分: XX/100
   - Experience: XX/25
   - Expertise: XX/25
   - Authoritativeness: XX/25
   - Trustworthiness: XX/25

2. AI 可引用性得分: XX/100
   - 结构可提取性: XX/33
   - 权威信号: XX/33
   - 第三方存在: XX/33

3. 综合得分: XX/100

4. 优先修复项
   - [具体建议]
```

[PROTOCOL]: 变更时更新此头部，然后检查 CLAUDE.md
