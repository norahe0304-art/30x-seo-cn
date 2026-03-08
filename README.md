```
██████╗  ██████╗ ██╗  ██╗    ███████╗███████╗ ██████╗
╚════██╗██╔═══██╗╚██╗██╔╝    ██╔════╝██╔════╝██╔═══██╗
 █████╔╝██║   ██║ ╚███╔╝     ███████╗█████╗  ██║   ██║
 ╚═══██╗██║   ██║ ██╔██╗     ╚════██║██╔══╝  ██║   ██║
██████╔╝╚██████╔╝██╔╝ ██╗    ███████║███████╗╚██████╔╝
╚═════╝  ╚═════╝ ╚═╝  ╚═╝    ╚══════╝╚══════╝ ╚═════╝
```

> 23 个生产级 SEO 技能 + Squirrelscan CLI，8 大类，专为 Claude Code 打造。覆盖审计、技术 SEO、链接、内容、规划、程序化 SEO、监控、数据全链路。

## 为什么选择 30x SEO？

- **8 大类 23 技能** — 完整 SEO 工作流，一个不落
- **AI 原生** — 专为 Claude Code 设计，不是老工具的缝合怪
- **面向 2026** — AI Overview、GEO 优化、LLM 引用追踪
- **零依赖问题** — 直接调 API，绕过 MCP 服务器的坑

---

## 快速开始

```bash
git clone https://github.com/norahe0304-art/30x-seo-cn.git ~/.openclaw/skills/30x-seo
```

**可选：配置 DataForSEO**（关键词/外链/SERP/AI 可见性需要）

```bash
echo -n "邮箱:密码" | base64 > ~/.config/dataforseo/auth
chmod 600 ~/.config/dataforseo/auth
```

---

## 技能全览（8 大类 23 技能 + 1 总控）

### 总控编排器

| 技能 | 功能 |
|------|------|
| `seo` | 主编排器：路由命令到 23 个子技能，调度 6 个并行子代理，自动检测行业类型 |

### 一、诊断审计类（1 技能 + CLI）

| 技能 | 功能 |
|------|------|
| `30x-seo-page` | 单页深度分析：标题、meta、H1-H6、链接、图片、Schema、E-E-A-T |
| `squirrelscan` *(CLI)* | 整站体检：230+ 条规则、21 个类别、健康评分 0-100。安装：`npm i -g squirrelscan` |

### 二、技术 SEO 类（5 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-technical` | 8 大类审计：爬取性、索引性、安全、URL、移动端、CWV、结构化数据、JS |
| `30x-seo-sitemap` | Sitemap 验证、问题检测、生成 |
| `30x-seo-hreflang` | 多语言 SEO：自引用、返回标签、x-default、ISO 代码 |
| `30x-seo-schema` | Schema 检测、验证、JSON-LD 生成 |
| `30x-seo-geo-technical` | AI 爬虫管理：GPTBot、ClaudeBot、llms.txt、SSR 检查 |

### 三、链接类（3 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-internal-links` | 孤立页、点击深度、锚文本、权重分布 |
| `30x-seo-backlinks` | 外链概览、锚文本、毒链、差距分析 *（需 DataForSEO）* |
| `30x-seo-redirects` | 重定向链、循环、301/302 混用、协议问题、斜杠一致性 |

### 四、内容类（6 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-content-audit` | E-E-A-T 评分 + AI 可引用性分析 |
| `30x-seo-images` | Alt 文本、文件大小、格式（WebP/AVIF）、懒加载、CLS |
| `30x-seo-content-decay` | 内容衰退检测，刷新优先级建议 |
| `30x-seo-cannibalization` | 关键词蚕食检测 |
| `30x-seo-content-brief` | 分析 SERP Top 10，生成内容简报 |
| `30x-seo-content-writer` | SEO + AI 优化写作指南 |

### 五、规划类（2 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-plan` | 竞品分析、关键词策略、内容日历、4 阶段路线图 |
| `30x-seo-architecture` | URL 结构、导航设计、内链策略 |

### 六、程序化 SEO 类（2 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-programmatic` | 规模化内容：数据源、模板、质量门控、索引控制 |
| `30x-seo-competitor-pages` | X vs Y 对比页、替代品页面、特性矩阵 |

### 七、监控类（3 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-monitor` | 监控自己网站：排名、点击、CTR、位置变化 *（需 Google Search Console）* |
| `30x-seo-serp` | 追踪任意网站 SERP 排名、特性、历史数据 *（需 DataForSEO）* |
| `30x-seo-ai-visibility` | 追踪 ChatGPT、Claude、Perplexity、Gemini、AI Overview 中的品牌曝光 *（需 DataForSEO）* |

### 八、数据类（1 技能）

| 技能 | 功能 |
|------|------|
| `30x-seo-keywords` | 关键词创意、搜索量、难度、意图、趋势 *（需 DataForSEO）* |

---

## 常用命令

```bash
# 诊断审计
/30x-seo page https://example.com/page
squirrelscan audit https://example.com --format llm

# 技术 SEO
/30x-seo technical https://example.com
/30x-seo schema https://example.com
/30x-seo sitemap https://example.com/sitemap.xml

# 链接
/30x-seo internal-links https://example.com
/30x-seo redirects https://example.com
/30x-seo backlinks profile example.com        # 需 DataForSEO

# 内容
/30x-seo content-audit https://example.com/page
/30x-seo content-brief "目标关键词"

# 规划
/30x-seo plan saas
/30x-seo architecture https://example.com

# 程序化 SEO
/30x-seo programmatic plan
/30x-seo competitor-pages generate

# 监控
/30x-seo monitor overview                     # GSC - 自己网站
/30x-seo monitor keywords                     # GSC - 自己排名
/30x-seo serp check "关键词"                  # DataForSEO - 任意网站
/30x-seo ai-visibility domain example.com     # DataForSEO

# 数据
/30x-seo keywords research "种子关键词"        # 需 DataForSEO
```

---

## 依赖关系

| 类别 | 技能数 | 依赖 |
|------|--------|------|
| 诊断审计 | 1 | WebFetch |
| 技术 SEO | 5 | WebFetch |
| 链接 | 3 | WebFetch + DataForSEO（backlinks）|
| 内容 | 6 | WebFetch |
| 规划 | 2 | WebFetch |
| 程序化 SEO | 2 | WebFetch |
| 监控 | 3 | GSC + DataForSEO |
| 数据 | 1 | DataForSEO |

**18 个技能无需任何 API。4 个技能需要 DataForSEO。1 个技能需要 Google Search Console。**

---

## DataForSEO 配置

1. 注册 [app.dataforseo.com](https://app.dataforseo.com)
2. 获取凭据：Settings → API Access
3. 生成 Base64 凭据：

```bash
echo -n "你的邮箱:你的API密码" | base64
```

4. 保存凭据：

```bash
mkdir -p ~/.config/dataforseo
echo "生成的Base64字符串" > ~/.config/dataforseo/auth
chmod 600 ~/.config/dataforseo/auth
```

5. 验证：

```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "seo", "limit": 1}]' | jq '.status_code'
# 返回 20000 = 成功
```

---

## License

MIT
