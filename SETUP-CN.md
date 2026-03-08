# Claude SEO Skills 配置指南

> 21 个 SEO 技能，覆盖技术 SEO、内容优化、关键词研究、外链分析、AI 可见性监控全链路。

---

## 快速开始

### 1. 配置 DataForSEO API（关键词/外链/SERP/AI 可见性）

```bash
# 1. 注册账户
https://app.dataforseo.com

# 2. 获取凭据（Settings → API Access）
# 格式：email:password 编码为 Base64

# 3. 生成 Base64 凭据
echo -n "your-email@example.com:your-api-password" | base64

# 4. 创建凭据文件
mkdir -p ~/.config/dataforseo
echo "你的Base64编码凭据" > ~/.config/dataforseo/auth
chmod 600 ~/.config/dataforseo/auth
```

**验证配置**：
```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "seo", "limit": 1}]' | jq '.status_code'
# 返回 20000 = 成功
```

### 2. 配置 MCP 服务器（可选）

编辑 `~/.config/claude/mcp.json`：

```json
{
  "mcpServers": {
    "perplexity": {
      "command": "uvx",
      "args": ["perplexity-mcp"],
      "env": {
        "PPLX_API_KEY": "your-perplexity-api-key"
      }
    },
    "google-workspace": {
      "command": "gws",
      "args": ["mcp", "-s", "drive,sheets,gmail,docs", "--tool-mode", "compact"]
    }
  }
}
```

| MCP | 用途 | 获取 Key |
|-----|------|----------|
| perplexity | AI 搜索研究 | https://perplexity.ai/settings/api |
| google-workspace | 输出到 Sheets/Docs | 需安装 gws CLI |

---

## Skills 详解（21 个）

### 技术 SEO（8 个）

#### 1. seo-technical — 技术 SEO 审计

检查 8 大类：
```
├── 爬取性：robots.txt、sitemap、noindex、爬取深度
├── 索引性：canonical、duplicate content、meta robots
├── 安全：HTTPS、安全头（CSP、HSTS、X-Frame-Options）
├── URL 结构：规范化、参数处理、重定向链
├── 移动端：响应式、viewport、触控目标
├── Core Web Vitals：LCP <2.5s、INP <200ms、CLS <0.1
├── 结构化数据：schema 检测与验证
└── JS 渲染：关键内容是否依赖 JavaScript
```

**特色**：包含 AI 爬虫管理指南（GPTBot、ClaudeBot、PerplexityBot）

---

#### 2. seo-sitemap — Sitemap 分析/生成

**分析模式**：
- 验证 XML 格式是否合规
- 检查 URL 数量 < 50,000
- 检测不该出现的 URL（noindex、301/302、4xx/5xx）
- 验证 lastmod 是否真实更新

**生成模式**：
- 按行业模板生成（电商、博客、企业站）
- 质量门控：30+ 地点页警告，50+ 强制停止

---

#### 3. seo-hreflang — 多语言/多地区 SEO

检查项：
- 自引用标签（每个页面必须有）
- 返回标签（A→B 必须有 B→A）
- x-default 标签（默认版本）
- 语言代码格式（en, ja, zh-Hans）
- 区域代码格式（en-US, en-GB, zh-TW）
- canonical 与 hreflang 对齐

---

#### 4. seo-schema — Schema 结构化数据

**功能**：
- 检测现有 schema（JSON-LD / Microdata / RDFa）
- 验证必填属性是否完整
- 检查已废弃类型（HowTo、FAQ 限制、SpecialAnnouncement）
- 推荐缺失的 schema 类型
- 生成 JSON-LD 代码

**支持类型**：Organization, LocalBusiness, Article, Product, VideoObject, Event, JobPosting, Course, BreadcrumbList, WebSite 等

---

#### 5. seo-images — 图片 SEO

检查项：
- alt 属性：是否存在、是否描述性
- 文件名：是否有意义（非 IMG_001.jpg）
- 格式：WebP/AVIF 优先
- 尺寸：是否适配显示尺寸
- 懒加载：首屏图片不应 lazy load
- CDN：是否使用图片 CDN

---

#### 6. seo-redirects — 重定向审计

检查项：
- 重定向链（A→B→C→D，应 < 2 跳）
- 重定向循环
- 302 应为 301 的情况
- 软 404（200 状态但内容为 404）
- 外部重定向（流失权重）

---

#### 7. seo-internal-links — 内链分析/生成

**分析模式**：
- 孤立页面（0 内链指向）
- 点击深度（重要页面应 ≤3 clicks）
- 锚文本分析（避免 "点击这里"）
- 断链检测
- 链接权重分布

**生成模式**：
- 输入新文章 → 输出应链接到哪些页面
- 输出哪些旧页面应链接到新文章
- 建议锚文本

---

#### 8. seo-geo-technical — GEO 技术优化

针对 AI 搜索引擎的技术优化：
- AI 爬虫 robots.txt 配置（GPTBot、ClaudeBot、PerplexityBot）
- llms.txt 生成（AI 友好的站点说明）
- SSR vs CSR 检测（AI 爬虫不执行 JS）
- 结构化答案格式检查

---

### 内容优化（8 个）

#### 9. seo-content-audit — 内容质量审计

**两个维度**：

| 维度 | 目标 | 指标 |
|------|------|------|
| 传统 SEO | Google 排名 | E-E-A-T 评分 |
| AI 可引用性 | ChatGPT/Perplexity 引用 | 结构、权威、存在 |

**E-E-A-T 检查**：
- Experience：原创研究、案例、第一手经验
- Expertise：作者资质、专业深度
- Authoritativeness：外部引用、行业认可
- Trustworthiness：联系方式、隐私政策、HTTPS

**AI 可引用性检查**：
- 段落可提取性（40-60 词最佳）
- 统计数据 + 来源
- 问答格式标题

---

#### 10. seo-content-brief — 内容简报生成

输入关键词，输出：
- 搜索意图分析
- SERP 竞品内容分析
- 推荐标题/H2 结构
- 目标字数
- 必须覆盖的子话题
- 内链建议

---

#### 11. seo-content-writer — 内容写作指南

基于 content-brief 的写作执行指南：
- 开头模板（直接回答问题）
- 段落结构（主张 → 证据 → 示例）
- AI 优化格式（可引用段落）
- CTA 位置建议

---

#### 12. seo-content-decay — 内容衰退检测

识别流量下降的内容：
- 对比历史排名/流量
- 检查内容新鲜度
- 竞品内容更新情况
- 推荐更新策略

---

#### 13. seo-cannibalization — 关键词蚕食检测

检测多个页面竞争同一关键词：
- 识别蚕食关键词
- 分析哪个页面应保留
- 合并/重定向建议

---

#### 14. seo-page — 单页面深度分析

针对单个 URL 的完整 SEO 检查：
- Title（50-60 字符，含关键词）
- Meta description（150-160 字符）
- H1（唯一，匹配意图）
- H2-H6 层级
- 关键词密度
- 内链/外链
- Schema
- 图片优化

---

#### 15. seo-competitor-pages — 竞品页面分析

对比你的页面与 SERP 前 10：
- 内容长度对比
- 标题/H2 结构对比
- 关键词覆盖差距
- 反向链接差距
- 内容差异化机会

---

#### 16. seo-programmatic — 程序化 SEO

大规模页面生成策略：
- 模板设计（城市页、产品页、对比页）
- 数据源规划
- 质量门控（避免薄内容）
- 内链策略
- 索引控制

---

### 关键词 & SERP（3 个，需 DataForSEO）

#### 17. seo-keywords — 关键词研究

**功能**：
- 关键词创意生成
- 搜索量查询
- 关键词难度评估（0-100）
- 搜索意图分类（信息/导航/商业/交易）
- 站点关键词分析
- 历史趋势

**API 端点**：
```bash
# 关键词建议
/v3/dataforseo_labs/google/keyword_suggestions/live

# 关键词难度
/v3/dataforseo_labs/bulk_keyword_difficulty/live

# 搜索量
/v3/keywords_data/google_ads/search_volume/live

# 搜索意图
/v3/dataforseo_labs/google/search_intent/live
```

---

#### 18. seo-serp — SERP 追踪

**功能**：
- 实时 SERP 查询
- 域名排名概览
- 历史 SERP 变化
- SERP 特性分析（AI Overview、Featured Snippet、PAA）
- 竞品排名对比

**API 端点**：
```bash
# 实时 SERP
/v3/serp/google/organic/live/advanced

# 域名排名
/v3/dataforseo_labs/google/ranked_keywords/live

# 域名概览
/v3/dataforseo_labs/google/domain_rank_overview/live
```

---

#### 19. seo-backlinks — 外链分析

**功能**：
- 外链概览（总数、域名数、权重）
- 锚文本分布
- 新增/丢失外链趋势
- 竞品外链对比
- 链接差距分析（竞品有你没有的外链来源）
- 毒链检测（高 spam score）

**API 端点**：
```bash
# 外链摘要
/v3/backlinks/summary/live

# 外链列表
/v3/backlinks/backlinks/live

# 锚文本
/v3/backlinks/anchors/live

# 链接差距
/v3/backlinks/domain_intersection/live

# 竞品对比
/v3/backlinks/competitors/live
```

---

### AI 可见性（2 个，需 DataForSEO）

#### 20. seo-ai-visibility — AI 搜索可见性监控

监控品牌在 AI 平台的曝光：

**支持平台**：
- Google AI Overview
- ChatGPT
- Claude
- Gemini
- Perplexity

**功能**：
- 域名 AI 提及次数
- 被引用的具体问题/查询
- 竞品 AI 可见性对比
- 跨平台曝光分析
- 获取各 LLM 对特定查询的回复

**API 端点**：
```bash
# LLM 提及搜索
/v3/ai_optimization/llm_mentions/search/live

# 被引用最多的页面
/v3/ai_optimization/llm_mentions/top_pages/live

# 关键词下被引用最多的域名
/v3/ai_optimization/llm_mentions/top_domains/live

# ChatGPT 回复
/v3/ai_optimization/chat_gpt/llm_responses/live

# Claude 回复
/v3/ai_optimization/claude/llm_responses/live
```

---

#### 21. seo-plan — SEO 策略规划

综合分析后生成 SEO 执行计划：
- 现状评估
- 优先级排序
- 时间线规划
- 资源需求
- KPI 设定

---

## 依赖关系总结

| Skill 类别 | 数量 | 依赖 |
|------------|------|------|
| 技术 SEO | 8 | WebFetch（内置）|
| 内容优化 | 8 | WebFetch（内置）|
| 关键词/SERP | 3 | **DataForSEO** |
| AI 可见性 | 2 | **DataForSEO** |

**无需 DataForSEO 即可使用 16 个 skills**。

---

## 常见问题

### DataForSEO 返回 401？

凭据格式错误。确保：
1. 格式是 `email:password`（不是 `email password`）
2. Base64 编码时没有换行符
3. 文件权限正确 `chmod 600`

### WebFetch 超时？

目标网站可能有反爬。尝试：
1. 稍后重试
2. 使用不同页面 URL
3. 检查网站是否需要登录

### 如何批量分析多个页面？

使用 `/seo audit` 会自动调用多个 skills 并行分析。

---

## 更新日志

- **2026-03-07**: 统一 21 个 skills 格式
- **2026-03-07**: 新增 seo-ai-visibility
- **2026-03-07**: DataForSEO 改用 curl 直调（MCP 有 bug）
- **2026-03-07**: 移除 Firecrawl（额度问题，WebFetch 够用）

---

## License

MIT
