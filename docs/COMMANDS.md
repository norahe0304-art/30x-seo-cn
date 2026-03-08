# 命令参考手册

## 概览

所有命令以 `/seo` 开头，后接子命令。

---

## 命令列表

### `/seo audit <url>`

全站 SEO 审计，6 个子代理并行分析。

**示例：**
```
/seo audit https://example.com
```

**执行流程：**
1. 爬取最多 500 个页面
2. 自动检测业务类型
3. 并行调度 6 个专业子代理
4. 生成 SEO 健康分数（0-100）
5. 创建优先级行动计划

**输出文件：**
- `FULL-AUDIT-REPORT.md`
- `ACTION-PLAN.md`
- `screenshots/`（如已安装 Playwright）

---

### `/seo page <url>`

单页深度分析。

**示例：**
```
/seo page https://example.com/about
```

**分析内容：**
- 页面 SEO（标题、meta、标题层级、URL）
- 内容质量（字数、可读性、E-E-A-T）
- 技术元素（canonical、robots、Open Graph）
- Schema 结构化数据
- 图片优化（alt 文本、尺寸、格式）
- Core Web Vitals 潜在问题

---

### `/seo technical <url>`

技术 SEO 审计，覆盖 8 大类别。

**示例：**
```
/seo technical https://example.com
```

**8 大类别：**
1. 爬取性（Crawlability）
2. 索引性（Indexability）
3. 安全性（Security）
4. URL 结构
5. 移动端优化
6. Core Web Vitals（LCP、INP、CLS）
7. 结构化数据
8. JavaScript 渲染

---

### `/seo content <url>`

E-E-A-T 与内容质量分析。

**示例：**
```
/seo content https://example.com/blog/post
```

**评估维度：**
- 经验信号（第一手知识）
- 专业性（作者资质）
- 权威性（外部认可）
- 可信度（透明度、安全性）
- AI 引用就绪度
- 内容新鲜度

---

### `/seo schema <url>`

Schema 结构化数据检测、验证、生成。

**示例：**
```
/seo schema https://example.com
```

**功能：**
- 检测现有 Schema（JSON-LD、Microdata、RDFa）
- 按 Google 要求验证
- 识别缺失机会
- 生成可用的 JSON-LD

---

### `/seo geo <url>`

AI 搜索优化（GEO / Generative Engine Optimization）。

**示例：**
```
/seo geo https://example.com/blog/guide
```

**分析内容：**
- 可引用性分数（可引用的事实、统计数据）
- 结构可读性（标题、列表、表格）
- 实体清晰度（定义、上下文）
- 权威信号（资质、来源）
- 结构化数据支持

---

### `/seo images <url>`

图片优化分析。

**示例：**
```
/seo images https://example.com
```

**检查项：**
- Alt 文本存在与质量
- 文件大小（标记 >200KB）
- 格式（推荐 WebP/AVIF）
- 响应式图片（srcset、sizes）
- 懒加载
- CLS 预防（尺寸声明）

---

### `/seo sitemap <url>`

分析现有 XML Sitemap。

**示例：**
```
/seo sitemap https://example.com/sitemap.xml
```

**验证内容：**
- XML 格式
- URL 数量（每文件 <50k）
- URL 状态码
- lastmod 准确性
- 已废弃标签（priority、changefreq）
- 覆盖率 vs 爬取页面

---

### `/seo sitemap generate`

生成新 Sitemap，带行业模板。

**示例：**
```
/seo sitemap generate
```

**流程：**
1. 选择或自动检测业务类型
2. 交互式结构规划
3. 应用质量门控（30/50 位置页限制）
4. 生成有效 XML
5. 创建文档

---

### `/seo plan <type>`

SEO 战略规划。

**类型：** `saas`、`local`、`ecommerce`、`publisher`、`agency`

**示例：**
```
/seo plan saas
```

**生成内容：**
- 完整 SEO 策略
- 竞品分析
- 内容日历
- 实施路线图（4 阶段）
- 站点架构设计

---

### `/seo competitor-pages [url|generate]`

竞品对比页面生成。

**示例：**
```
/seo competitor-pages https://example.com/vs/competitor
/seo competitor-pages generate
```

**功能：**
- 生成「X vs Y」对比页面布局
- 创建「X 替代品」页面结构
- 构建带评分的功能对比矩阵
- 生成 Product + AggregateRating Schema
- 应用转化优化的 CTA 布局
- 强制执行公平性准则（准确数据、来源引用）

---

### `/seo hreflang [url]`

Hreflang 与国际化 SEO 审计生成。

**示例：**
```
/seo hreflang https://example.com
```

**功能：**
- 验证 hreflang 自引用标签
- 检查返回标签互惠（A→B 需要 B→A）
- 验证 x-default 标签存在
- 验证 ISO 639-1 语言和 ISO 3166-1 地区代码
- 检查 canonical URL 与 hreflang 对齐
- 检测协议不匹配（HTTP vs HTTPS）
- 生成正确的 hreflang link 标签和 sitemap XML

---

### `/seo programmatic [url|plan]`

程序化 SEO 分析与规划（大规模生成页面）。

**示例：**
```
/seo programmatic https://example.com/tools/
/seo programmatic plan
```

**功能：**
- 评估数据源质量（CSV、JSON、API、数据库）
- 规划模板引擎，确保每页独特内容
- 设计 URL 模式策略（`/tools/[tool-name]`、`/[city]/[service]`）
- 自动化内部链接（hub/spoke、相关项、面包屑）
- 强制执行薄内容保护（质量门控、字数阈值）
- 防止索引膨胀（noindex 低价值、分页、faceted nav）

---

### `/seo keywords research "关键词"`

关键词研究 — **需要 DataForSEO**。

**示例：**
```
/seo keywords research "seo 工具"
```

**输出：**
- 关键词创意
- 搜索量
- 难度评分
- 搜索意图
- 趋势数据

---

### `/seo serp check "关键词"`

实时 SERP 分析 — **需要 DataForSEO**。

**示例：**
```
/seo serp check "最好的 crm 软件"
```

**输出：**
- 实时排名
- SERP 特性（精选摘要、PAA、本地包等）
- 历史排名数据
- 竞品分析

---

### `/seo backlinks profile <domain>`

外链分析 — **需要 DataForSEO**。

**示例：**
```
/seo backlinks profile example.com
```

**输出：**
- 外链概览
- 锚文本分布
- 毒链检测
- 竞品差距分析

---

### `/seo ai-visibility domain <domain>`

AI 可见性监控 — **需要 DataForSEO**。

**示例：**
```
/seo ai-visibility domain example.com
```

**输出：**
- Google AI Overview 提及
- ChatGPT 引用追踪
- Claude 引用追踪
- Perplexity 引用追踪
- Gemini 引用追踪
- 竞品 AI 可见性对比

---

## 快速参考

| 命令 | 用途 | 依赖 |
|------|------|------|
| `/seo audit <url>` | 全站审计 | WebFetch |
| `/seo page <url>` | 单页分析 | WebFetch |
| `/seo technical <url>` | 技术 SEO | WebFetch |
| `/seo content <url>` | E-E-A-T 分析 | WebFetch |
| `/seo schema <url>` | Schema 验证 | WebFetch |
| `/seo geo <url>` | AI 搜索优化 | WebFetch |
| `/seo images <url>` | 图片优化 | WebFetch |
| `/seo sitemap <url>` | Sitemap 验证 | WebFetch |
| `/seo sitemap generate` | 创建 Sitemap | WebFetch |
| `/seo plan <type>` | 战略规划 | WebFetch |
| `/seo competitor-pages` | 竞品对比页 | WebFetch |
| `/seo hreflang [url]` | 多语言 SEO | WebFetch |
| `/seo programmatic` | 程序化 SEO | WebFetch |
| `/seo keywords research` | 关键词研究 | DataForSEO |
| `/seo serp check` | SERP 分析 | DataForSEO |
| `/seo backlinks profile` | 外链分析 | DataForSEO |
| `/seo ai-visibility` | AI 可见性 | DataForSEO |
