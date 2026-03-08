# 故障排除

## 常见问题

### 技能未加载

**症状：** `/seo` 命令无法识别

**解决方案：**

1. 验证安装：
```bash
ls ~/.openclaw/skills/30x-seo/seo/SKILL.md
```

2. 检查 SKILL.md 格式：
```bash
head -5 ~/.openclaw/skills/30x-seo/seo/SKILL.md
```
应以 `---` 开头，后跟 YAML。

3. 重启 Claude Code：
```bash
claude
```

4. 重建索引：
```bash
python3 ~/Desktop/SEO\ skills/scripts/rebuild-index.py
```

---

### DataForSEO 返回 401

**症状：** API 调用返回认证失败

**解决方案：**

1. 确保凭据格式正确（邮箱:密码，用冒号分隔）：
```bash
echo -n "邮箱:密码" | base64
```

2. 确保文件没有换行符：
```bash
cat -A ~/.config/dataforseo/auth
# 不应有 $（换行符）
```

3. 测试 API：
```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "test", "limit": 1}]' | jq '.status_code'
# 返回 20000 = 成功
```

4. 重新生成密码：
   - 登录 https://app.dataforseo.com
   - Settings → API Access → 重新生成密码
   - 更新 `~/.config/dataforseo/auth`

---

### WebFetch 超时

**症状：** 请求超时或无响应

**解决方案：**

1. 目标网站可能有反爬 — 稍后重试
2. 目标网站响应慢 — 耐心等待
3. 换一个页面测试
4. 检查网络连接

---

### Playwright 截图错误

**症状：** `playwright._impl._errors.Error: Executable doesn't exist`

**解决方案：**
```bash
pip install playwright
playwright install chromium
```

如果失败：
```bash
python3 -m playwright install chromium
```

---

### 权限拒绝错误

**症状：** `Permission denied` 运行脚本时

**解决方案：**
```bash
chmod +x ~/.openclaw/skills/30x-seo/scripts/*.py
chmod +x ~/.openclaw/skills/30x-seo/hooks/*.py
chmod +x ~/.openclaw/skills/30x-seo/hooks/*.sh
```

---

### 子代理未找到

**症状：** `Agent 'seo-technical' not found`

**解决方案：**

1. 验证代理文件存在：
```bash
ls ~/.openclaw/skills/30x-seo/agents/seo-*.md
```

2. 检查代理 frontmatter：
```bash
head -5 ~/.openclaw/skills/30x-seo/agents/seo-technical.md
```

3. 确保代理目录正确。

---

### 请求超时

**症状：** `Request timed out after 30 seconds`

**解决方案：**

1. 目标网站可能慢 — 重试
2. 检查网络连接
3. 某些网站阻止自动化请求
4. 尝试不同的 URL

---

### Schema 验证误报

**症状：** Hook 阻止有效的 Schema

**检查：**

1. 确保占位符已替换
2. 验证 @context 是 `https://schema.org`
3. 检查废弃类型（HowTo、SpecialAnnouncement）
4. 在 [Google 富媒体结果测试](https://search.google.com/test/rich-results) 验证

---

### 审计性能慢

**症状：** 全站审计耗时过长

**解决方案：**

1. 审计最多爬取 500 页 — 大站点需要时间
2. 子代理并行运行加速分析
3. 快速检查用 `/seo page` 分析特定 URL
4. 检查目标站点响应时间

---

## 获取帮助

1. **查看文档：** [COMMANDS.md](COMMANDS.md) 和 [ARCHITECTURE.md](ARCHITECTURE.md)

2. **GitHub Issues：** 在仓库报告 Bug

3. **日志：** 检查 Claude Code 输出获取错误详情

## 调试模式

查看详细输出，直接运行脚本测试：

```bash
# 测试获取
python3 ~/.openclaw/skills/30x-seo/scripts/fetch_page.py https://example.com

# 测试解析
python3 ~/.openclaw/skills/30x-seo/scripts/parse_html.py page.html --json

# 测试截图
python3 ~/.openclaw/skills/30x-seo/scripts/capture_screenshot.py https://example.com
```

---

## DataForSEO API 调试

### 测试关键词 API

```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "seo", "language_code": "zh", "location_code": 2156, "limit": 3}]' | jq
```

### 测试外链 API

```bash
curl -s -X POST "https://api.dataforseo.com/v3/backlinks/summary/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"target": "example.com"}]' | jq
```

### 测试 AI 可见性 API

```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/ai_optimization/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "best crm software", "location_code": 2840, "language_code": "en"}]' | jq
```

### 常见状态码

| 状态码 | 含义 |
|--------|------|
| 20000 | 成功 |
| 40100 | 认证失败（检查凭据）|
| 40200 | 余额不足 |
| 40400 | 参数无效 |
| 50000 | 服务器错误（稍后重试）|
