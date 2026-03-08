# MCP 集成指南

> **重要说明**：30x SEO 中文版默认使用 **curl 直接调用 API**，不依赖 MCP 服务器。这避免了 MCP 服务器的各种 bug 和配置问题。

## 概览

30x SEO 可以与 MCP（Model Context Protocol）服务器集成以访问外部 API。但我们推荐直接使用 curl 调用，更稳定可靠。

## 推荐方案：直接 API 调用

### DataForSEO（关键词/外链/AI 可见性）

**配置凭据：**

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

**验证：**

```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "seo", "limit": 1}]' | jq '.status_code'
# 返回 20000 = 成功
```

### PageSpeed Insights API

**直接调用（无需 MCP）：**

```bash
curl "https://www.googleapis.com/pagespeedonline/v5/runPagespeed?url=URL&key=YOUR_API_KEY"
```

获取 API Key：
1. 访问 [Google Cloud Console](https://console.cloud.google.com/)
2. 启用 PageSpeed Insights API
3. 创建 API 凭据

---

## 可选 MCP 集成

如果你仍想使用 MCP 服务器，以下是可用的集成：

### 官方 SEO MCP 服务器（2025-2026）

| 工具 | 包名 / 端点 | 类型 | 备注 |
|------|-------------|------|------|
| **Ahrefs** | `@ahrefs/mcp` | 官方 | 2025 年 7 月发布。支持本地和远程模式。|
| **Semrush** | `https://mcp.semrush.com/v1/mcp` | 官方（远程）| 通过远程 MCP 端点完整 API 访问。|
| **Google Search Console** | `mcp-server-gsc` | 社区 | 搜索性能、URL 检查、Sitemap。|
| **PageSpeed Insights** | `mcp-server-pagespeed` | 社区 | Lighthouse 审计、CWV 指标。|
| **DataForSEO** | `dataforseo-mcp-server` | 社区 | SERP、关键词、外链。⚠️ 有 bug |

### Google Search Console MCP

```json
{
  "mcpServers": {
    "google-search-console": {
      "command": "npx",
      "args": ["-y", "mcp-server-gsc"],
      "env": {
        "GOOGLE_CREDENTIALS_PATH": "/path/to/credentials.json"
      }
    }
  }
}
```

### PageSpeed Insights MCP

```json
{
  "mcpServers": {
    "pagespeed": {
      "command": "npx",
      "args": ["-y", "mcp-server-pagespeed"],
      "env": {
        "PAGESPEED_API_KEY": "your-api-key"
      }
    }
  }
}
```

---

## API 代码示例

### PageSpeed Insights

```python
import requests

def get_pagespeed_data(url: str, api_key: str) -> dict:
    """获取 URL 的 PageSpeed Insights 数据。"""
    endpoint = "https://www.googleapis.com/pagespeedonline/v5/runPagespeed"
    params = {
        "url": url,
        "key": api_key,
        "strategy": "mobile",  # 或 "desktop"
        "category": ["performance", "accessibility", "best-practices", "seo"]
    }
    response = requests.get(endpoint, params=params)
    return response.json()
```

### Chrome UX Report (CrUX)

```python
def get_crux_data(url: str, api_key: str) -> dict:
    """获取 URL 的 Chrome UX 报告数据。"""
    endpoint = "https://chromeuxreport.googleapis.com/v1/records:queryRecord"
    payload = {
        "url": url,
        "formFactor": "PHONE"  # 或 "DESKTOP"
    }
    headers = {"Content-Type": "application/json"}
    params = {"key": api_key}
    response = requests.post(endpoint, json=payload, headers=headers, params=params)
    return response.json()
```

---

## 可用指标

### PageSpeed Insights（实验室数据）

| 指标 | 描述 |
|------|------|
| LCP | 最大内容绘制 |
| INP | 交互到下一次绘制（估算）|
| CLS | 累积布局偏移 |
| FCP | 首次内容绘制 |
| TBT | 总阻塞时间 |
| Speed Index | 视觉进度速度 |

### CrUX（真实用户数据）

| 指标 | 描述 |
|------|------|
| LCP | 第 75 百分位，真实用户 |
| INP | 第 75 百分位，真实用户 |
| CLS | 第 75 百分位，真实用户 |
| TTFB | 首字节时间 |

---

## 最佳实践

1. **速率限制**：遵守 API 配额（PageSpeed 通常 25k 请求/天）
2. **缓存**：缓存结果避免重复 API 调用
3. **优先真实数据**：排名信号优先使用 CrUX 真实用户数据
4. **错误处理**：优雅处理 API 错误

---

## 无 API Key 时

即使没有 API Key，30x SEO 仍可：

1. 分析 HTML 源码发现潜在问题
2. 识别常见性能问题
3. 检查渲染阻塞资源
4. 评估图片优化机会
5. 检测 JavaScript 密集实现

分析会注明实际 Core Web Vitals 测量需要真实用户数据。
