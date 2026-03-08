---
name: 30x-seo-geo-technical
description: >
  Technical SEO for AI search engines. Checks AI crawler accessibility,
  llms.txt compliance, robots.txt configuration, server-side rendering.
  Outputs problems + fixes (generates llms.txt, robots.txt modifications).
  Use when user says "AI crawlers", "llms.txt", "GPTBot", "GEO technical".
allowed-tools:
  - WebFetch
  - Read
---

# GEO Technical（AI 搜索技术检查）

## What This Skill Does

检查网站对 AI 搜索引擎的**技术可访问性**，发现问题并帮助修复。

**不做的事**：
- 内容质量分析 → 用 `seo-content-audit`（E-E-A-T + AI 可引用性）

---

## Process

### Step 1: Check AI Crawler Access（检查 AI 爬虫访问）

读取 `robots.txt`，检查这些爬虫是否被允许：

| 爬虫 | 所有者 | 用途 | 建议 |
|------|--------|------|------|
| GPTBot | OpenAI | ChatGPT 搜索 | ✅ 允许 |
| OAI-SearchBot | OpenAI | OpenAI 搜索 | ✅ 允许 |
| ChatGPT-User | OpenAI | ChatGPT 浏览 | ✅ 允许 |
| ClaudeBot | Anthropic | Claude 搜索 | ✅ 允许 |
| PerplexityBot | Perplexity | Perplexity AI | ✅ 允许 |
| CCBot | Common Crawl | 训练数据 | ⚠️ 可选阻止 |
| anthropic-ai | Anthropic | Claude 训练 | ⚠️ 可选阻止 |
| Bytespider | ByteDance | TikTok AI | ⚠️ 可选阻止 |

**问题示例**：
```
❌ GPTBot 被阻止 → ChatGPT 无法引用你的内容
❌ PerplexityBot 被阻止 → Perplexity 无法引用
```

**修复输出**：
```
# robots.txt 修改建议
User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /
```

### Step 2: Check llms.txt（检查 llms.txt）

检查 `/llms.txt` 是否存在：

| 状态 | 说明 |
|------|------|
| ✅ 存在且完整 | 有标题、描述、关键页面列表 |
| ⚠️ 存在但不完整 | 缺少关键信息 |
| ❌ 不存在 | 需要创建 |

**修复输出**（生成 llms.txt）：
```markdown
# [网站名称]
> [一句话描述]

## 核心页面
- [首页](https://example.com/): 网站首页
- [产品](https://example.com/products): 产品列表
- [关于我们](https://example.com/about): 公司介绍

## 关键信息
- 成立于 XXXX 年
- 服务 XXX 客户
- 主营业务：XXX
```

### Step 3: Check Server-Side Rendering（检查 SSR）

**AI 爬虫不执行 JavaScript**，关键内容必须在 HTML 中直接可见。

检查方法：
1. 禁用 JavaScript 访问页面
2. 检查关键内容是否可见

| 状态 | 说明 |
|------|------|
| ✅ SSR | 关键内容在 HTML 中 |
| ❌ CSR | 关键内容需要 JS 加载 |

**问题示例**：
```
❌ 产品描述在 JS 渲染后才出现
❌ 文章正文依赖 React hydration
```

**修复建议**：
- 使用 SSR/SSG 框架（Next.js、Nuxt、Astro）
- 预渲染关键页面
- 确保 `<noscript>` 有内容

### Step 4: Platform-Specific Check（平台检查）

| 平台 | 技术要求 |
|------|---------|
| **Google AI Overviews** | 传统 SEO 基础 + Schema |
| **ChatGPT** | GPTBot 访问 + llms.txt |
| **Perplexity** | PerplexityBot 访问 |
| **Bing Copilot** | Bing 索引 + IndexNow |

---

## Output（输出）

### 1. GEO 技术报告

```markdown
# GEO Technical Report

## AI 爬虫访问状态
| 爬虫 | 状态 | 问题 |
|------|------|------|
| GPTBot | ✅ 允许 | — |
| ClaudeBot | ❌ 阻止 | robots.txt 第 12 行 |
| PerplexityBot | ✅ 允许 | — |

## llms.txt 状态
❌ 不存在

## SSR 状态
⚠️ 部分页面依赖 JS

## 问题汇总
1. ClaudeBot 被阻止
2. 缺少 llms.txt
3. /products 页面内容依赖 JS
```

### 2. 修复代码

```markdown
# 修复建议

## robots.txt 修改
[生成修改后的 robots.txt]

## llms.txt 生成
[生成完整的 llms.txt]

## SSR 修复建议
- 页面 /products 需要启用 SSR
- 建议迁移到 Next.js SSG
```

---

## Reference: AI Crawler Details

### robots.txt 完整配置示例

```
# AI 搜索爬虫（允许）
User-agent: GPTBot
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

# AI 训练爬虫（可选阻止）
User-agent: CCBot
Disallow: /

User-agent: anthropic-ai
Disallow: /
```

### llms.txt 完整格式

```markdown
# Site Name
> Brief description of the site

## Main Sections
- [Page Title](url): Description
- [Another Page](url): Description

## Key Facts
- Fact 1
- Fact 2

## Contact
- Email: xxx
- Social: xxx
```

### RSL 1.0（Really Simple Licensing）

机器可读的 AI 许可条款（2025.12）。

支持者：Reddit、Yahoo、Medium、Quora、Cloudflare、Akamai、Creative Commons

---

## Integration

| 相关技能 | 用途 |
|---------|------|
| seo-technical | 传统技术 SEO 检查 |
| seo-content-audit | 内容质量 + AI 可引用性分析 |

[PROTOCOL]: 变更时更新此头部，然后检查 CLAUDE.md
