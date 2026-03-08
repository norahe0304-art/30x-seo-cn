# 30x SEO 中文版

> 21 个生产级 SEO 技能，专为 Claude Code 打造。覆盖技术 SEO、内容优化、关键词研究、外链分析、AI 可见性监控全链路。

## 为什么选择 30x SEO？

🎯 **全链路覆盖** — 技术 SEO → 内容 → 关键词 → 外链 → AI 可见性，一个不落

🤖 **AI 原生** — 专为 Claude Code 设计，不是老工具的缝合怪

🔮 **面向未来** — 2026 年新标准：AI Overview、GEO 优化、LLM 引用追踪

⚡ **零依赖问题** — 直接调 API，绕过 MCP 服务器的坑

---

## 快速开始

### 安装

```bash
git clone https://github.com/YOUR_USERNAME/30x-seo-cn.git ~/.openclaw/skills/30x-seo
```

### 配置 DataForSEO（关键词/外链/SERP/AI 可见性功能需要）

```bash
# 1. 注册 https://app.dataforseo.com
# 2. 获取 API 凭据（Settings → API Access）

# 3. 生成 Base64 凭据
echo -n "你的邮箱:你的API密码" | base64

# 4. 保存凭据
mkdir -p ~/.config/dataforseo
echo "生成的Base64字符串" > ~/.config/dataforseo/auth
chmod 600 ~/.config/dataforseo/auth
```

### 验证配置

```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "seo", "limit": 1}]' | jq '.status_code'
# 返回 20000 = 成功
```

---

## 技能全览

### 技术 SEO（8 个）

| 技能 | 功能 |
|------|------|
| `seo-technical` | 8 大类审计：爬取性、索引性、安全、URL、移动端、Core Web Vitals、结构化数据、JS 渲染 |
| `seo-sitemap` | Sitemap 验证、问题检测、生成 |
| `seo-hreflang` | 多语言/多地区：自引用、返回标签、x-default |
| `seo-schema` | Schema 检测、验证、JSON-LD 生成 |
| `seo-images` | Alt 文本、格式、尺寸、懒加载、CDN |
| `seo-redirects` | 重定向链、循环、软 404、外部泄露 |
| `seo-internal-links` | 孤立页、点击深度、锚文本、权重分布 |
| `seo-geo-technical` | AI 爬虫管理：GPTBot、ClaudeBot、llms.txt |

### 内容优化（8 个）

| 技能 | 功能 |
|------|------|
| `seo-content-audit` | E-E-A-T 评分 + AI 可引用性分析 |
| `seo-content-brief` | 基于关键词生成内容简报 |
| `seo-content-writer` | SEO + AI 优化写作指南 |
| `seo-content-decay` | 内容衰退检测，更新建议 |
| `seo-cannibalization` | 关键词蚕食检测 |
| `seo-page` | 单页深度分析 |
| `seo-competitor-pages` | 对比 SERP 前 10 竞品 |
| `seo-programmatic` | 程序化 SEO，质量门控 |

### 关键词 & SERP（3 个）— *需要 DataForSEO*

| 技能 | 功能 |
|------|------|
| `seo-keywords` | 关键词创意、搜索量、难度、意图、趋势 |
| `seo-serp` | 实时 SERP、排名追踪、历史数据、SERP 特性 |
| `seo-backlinks` | 外链概览、锚文本、毒链、差距分析 |

### AI 可见性（2 个）— *需要 DataForSEO*

| 技能 | 功能 |
|------|------|
| `seo-ai-visibility` | 追踪品牌在 ChatGPT、Claude、Perplexity、Gemini、Google AI Overview 中的曝光 |
| `seo-plan` | 生成完整 SEO 策略 |

---

## 常用命令

```bash
# 技术 SEO
/seo technical https://example.com
/seo schema https://example.com
/seo sitemap analyze https://example.com/sitemap.xml

# 内容优化
/seo content-audit https://example.com/page
/seo content-brief "目标关键词"

# 关键词 & SERP（需 DataForSEO）
/seo keywords research "种子关键词"
/seo serp check "关键词"
/seo backlinks profile example.com

# AI 可见性（需 DataForSEO）
/seo ai-visibility domain example.com
/seo ai-visibility keyword "最好的CRM软件"
```

---

## 目录结构

```
30x-seo/
├── skills/           # 21 个 SEO 技能
│   └── 30x-seo-*/    # 各技能目录
├── agents/           # 6 个子代理（并行执行）
├── docs/             # 架构、命令、MCP 集成文档
├── schema/           # JSON-LD 模板
└── seo/              # 主技能 + 参考资料
```

---

## 依赖关系

| 技能类别 | 数量 | 依赖 |
|----------|------|------|
| 技术 SEO | 8 | WebFetch（内置）|
| 内容优化 | 8 | WebFetch（内置）|
| 关键词/SERP/外链 | 3 | DataForSEO API |
| AI 可见性 | 2 | DataForSEO API |

**16 个技能无需任何 API 配置即可使用。**

---

## 亮点功能

### 🔥 AI 可见性监控

这是 2026 年的刚需。追踪你的品牌在 AI 搜索中的曝光：

```bash
/seo ai-visibility domain example.com
```

输出：
- Google AI Overview 提及次数
- ChatGPT 引用追踪
- Claude 引用追踪
- Perplexity 引用追踪
- 竞品 AI 可见性对比

### 🎯 E-E-A-T + GEO 双维度

传统 SEO 和 AI 搜索优化并重：

- **E-E-A-T**：经验、专业、权威、可信
- **GEO**：可提取性、引用信号、第三方存在

### ⚡ DataForSEO 直调

绕过 MCP 服务器的 bug，直接用 curl 调 API：

```bash
curl -s -X POST "https://api.dataforseo.com/v3/..." \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{...}]'
```

---

## 详细文档

- [SETUP-CN.md](SETUP-CN.md) — 21 个技能详细说明 + API 端点参考

---

## 包含内容

- **9,300+ 行** SEO 指导文档
- **2025-2026 更新**：INP 指标、AI Overview 优化、E-E-A-T 新准则
- **AI 可见性监控**：追踪 LLM 引用
- **GEO 优化**：针对 AI 搜索的生成式引擎优化
- **质量门控**：防止薄内容、门页

---

## 常见问题

### DataForSEO 返回 401？

```bash
# 确保凭据格式正确（邮箱:密码，用冒号分隔）
echo -n "邮箱:密码" | base64

# 确保文件没有换行符
cat -A ~/.config/dataforseo/auth  # 不应有 $（换行符）
```

### WebFetch 超时？

目标网站可能有反爬。稍后重试或换个页面。

### 16 个免费技能够用吗？

够用。技术 SEO + 内容优化完全不需要 API。只有关键词研究、外链分析、AI 可见性需要 DataForSEO。

---

## License

MIT
