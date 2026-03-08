---
name: 30x-seo-internal-links
description: >
  Internal link analysis AND generation. Analyzes orphan pages, link equity,
  anchor text. Also generates link suggestions for new content. Use when
  user says "internal linking", "orphan pages", "link suggestions", "where
  should I link", or "internal link recommendations".
allowed-tools:
  - WebFetch
  - Read
---

# Internal Link Analysis + Generation

## What This Skill Does

**两个功能**：

| 模式 | 输入 | 输出 |
|------|------|------|
| **分析模式** | 网站 URL | 内链问题报告 |
| **生成模式** | 新文章 + 网站结构 | 内链建议（链接到哪里、锚文本）|

Good internal linking:
- Helps Google find all your pages
- Distributes "link juice" (ranking power) to important pages
- Guides users through your content

## Why Internal Links Matter

- **Orphan pages** (no internal links) = Google can't find them = not indexed
- **Deep pages** (6+ clicks from homepage) = Google thinks they're not important
- **Link hoarding** (homepage links to everything) = diluted equity per link
- **Poor anchor text** = Google doesn't understand what the linked page is about

## Check Categories

### 1. Orphan Pages
Pages with ZERO internal links pointing to them.

**How to find:**
1. Crawl entire site to find all pages
2. Check which pages have no inbound internal links
3. Cross-reference with sitemap (orphan pages often only accessible via sitemap)

**Severity:**
- Orphan + in sitemap = Medium (Google can find via sitemap, but weak)
- Orphan + not in sitemap = Critical (Google may never find it)

### 2. Click Depth Analysis

| Depth | Meaning | SEO Impact |
|-------|---------|------------|
| 1 click | Linked from homepage | Highest priority |
| 2 clicks | Linked from main sections | High priority |
| 3 clicks | Standard content | Normal priority |
| 4+ clicks | Buried content | Lower priority |
| 6+ clicks | Too deep | Likely not indexed well |

**Rule**: Important pages should be within 3 clicks of homepage.

### 3. Internal Link Distribution

**PageRank flow analysis:**
- Which pages receive the most internal links?
- Which pages receive the fewest?
- Does distribution match business priority?

**Common problems:**
| Problem | Description | Fix |
|---------|-------------|-----|
| Homepage hoarding | Homepage has 500 outlinks | Consolidate navigation, use hub pages |
| Orphan cluster | Group of pages only link to each other | Add links from main site sections |
| Dead ends | Pages with no outbound internal links | Add contextual links to related content |
| Link silos | Sections don't link between each other | Add cross-section contextual links |

### 4. Anchor Text Analysis

**Good anchor text:**
- Descriptive of target page content
- Contains relevant keywords naturally
- Varies across different linking pages

**Bad anchor text patterns:**
| Pattern | Example | Problem |
|---------|---------|---------|
| Generic | "click here", "read more" | No keyword signal |
| Over-optimized | Every link = "best SEO tool" | Looks spammy |
| Naked URLs | "https://site.com/page" | Wastes keyword opportunity |
| Mismatched | Anchor = "dogs", target = cat page | Confusing signal |

### 5. Broken Internal Links
Links pointing to 404 pages within your own site.

**Impact:**
- Wastes link equity
- Bad user experience
- Wastes crawl budget

### 6. Nofollow on Internal Links
Using `rel="nofollow"` on internal links = bad practice.

**When it's wrong:**
- Regular content links marked nofollow
- Navigation links marked nofollow

**When it's acceptable:**
- User-generated content (comments)
- Login/signup pages (PageRank sculpting is dead, but still ok)

### 7. Link Equity Sinks
Pages that receive lots of internal links but provide no value:
- Thank you pages
- Login pages
- Terms of service (linked from every page footer)

**Solution:** Add `nofollow` or reduce links to low-value pages.

### 8. Contextual vs Navigation Links

| Type | Description | SEO Value |
|------|-------------|-----------|
| Navigation | Header, footer, sidebar | Lower (same on every page) |
| Contextual | Within article content | Higher (unique, topically relevant) |

**Goal:** Important pages should have BOTH navigation AND contextual links.

## Analysis Method

### Step 1: Crawl Site
- Use crawler to discover all pages
- Record all internal links (source URL, target URL, anchor text)

### Step 2: Build Link Graph
- Create adjacency matrix of page relationships
- Calculate inbound/outbound link counts per page

### Step 3: Calculate Metrics
- **Click depth**: BFS from homepage
- **Internal PageRank**: Simplified PageRank calculation
- **Orphan detection**: Pages with 0 inbound links

### Step 4: Cross-Reference with Goals
- Which pages should rank? (money pages, pillar content)
- Do those pages have strong internal link support?

## Output Format

### Internal Link Health Score: XX/100

### Site Structure Overview
```
Total pages: XXX
Total internal links: XXX
Average links per page: XX
Max click depth: X

Link Distribution:
├── Depth 1: XX pages (XX%)
├── Depth 2: XX pages (XX%)
├── Depth 3: XX pages (XX%)
├── Depth 4+: XX pages (XX%)
└── Orphans: XX pages (XX%)
```

### Critical Issues

#### Orphan Pages (XX found)
| URL | In Sitemap? | Suggested Link From |
|-----|-------------|---------------------|

#### Deep Pages (6+ clicks) (XX found)
| URL | Current Depth | Suggested Link From |

#### Broken Internal Links (XX found)
| Source URL | Broken Link | Suggested Fix |

### Link Equity Analysis

#### Top 10 Pages by Internal Links
| URL | Inbound Links | Is Priority Page? |

#### Under-Linked Priority Pages
| URL | Current Links | Recommended Links |

### Anchor Text Report

#### Over-Optimized Anchors
| Anchor Text | Count | Target Pages |

#### Generic Anchors (fix these)
| Anchor Text | Count | Better Alternative |

### Recommendations
1. [Specific fix instructions based on findings]

---

## Part 2: Link Generation Mode（生成模式）

### When to Use

写完新文章后，不知道该链接到哪里。

### Input

1. **新文章内容**（或 URL）
2. **网站现有页面列表**（或网站 URL 让技能爬取）

### Process

#### Step 1: Analyze New Article
- 提取文章主题、关键词
- 识别可链接的概念/术语

#### Step 2: Match with Existing Pages
- 找出与新文章主题相关的现有页面
- 按相关性排序

#### Step 3: Generate Suggestions

**输出 3 类建议**：

| 类型 | 说明 |
|------|------|
| **Outbound** | 新文章应该链接到哪些现有页面 |
| **Inbound** | 哪些现有页面应该添加链接指向新文章 |
| **Anchor Text** | 每个链接的建议锚文本 |

### Output Format

```markdown
# Internal Link Suggestions

## 新文章信息
- 标题: [文章标题]
- URL: [文章 URL]
- 主题: [主要主题]
- 关键词: [关键词列表]

## Outbound Links（新文章 → 现有页面）

| 链接位置 | 目标页面 | 建议锚文本 | 原因 |
|---------|---------|-----------|------|
| 第 2 段 "SEO 优化" | /seo-guide | "SEO 优化指南" | 主题相关 |
| 第 5 段 "关键词研究" | /keyword-research | "关键词研究方法" | 深入阅读 |
| 结尾 CTA | /services | "我们的服务" | 转化引导 |

## Inbound Links（现有页面 → 新文章）

| 来源页面 | 建议添加位置 | 建议锚文本 |
|---------|-------------|-----------|
| /seo-guide | "内部链接"相关段落 | "内部链接策略" |
| /blog-index | 最新文章列表 | [文章标题] |

## 实施清单

- [ ] 在新文章第 2 段添加链接到 /seo-guide
- [ ] 在新文章第 5 段添加链接到 /keyword-research
- [ ] 更新 /seo-guide 添加反向链接
```

### Example

```
User: 我写了一篇关于"Core Web Vitals优化"的文章，应该链接到哪里？

Claude: [读取文章内容]
        [读取网站现有页面]
        [匹配相关页面]

输出:
- 链接到 /technical-seo（"技术SEO"）
- 链接到 /page-speed（"页面速度优化"）
- 链接到 /google-ranking-factors（"Google排名因素"）
- 建议 /technical-seo 反向链接到这篇新文章
```

---

## Commands

| 命令 | 模式 |
|------|------|
| `/seo internal-links https://example.com` | 分析模式 |
| `/seo internal-links suggest [新文章]` | 生成模式 |

[PROTOCOL]: 变更时更新此头部，然后检查 CLAUDE.md
