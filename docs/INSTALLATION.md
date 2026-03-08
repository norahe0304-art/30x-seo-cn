# 安装指南

## 前提条件

- **Claude Code CLI** 已安装并配置
- **Git** 用于克隆仓库

可选：
- **Python 3.8+** 用于脚本功能
- **Playwright** 用于截图功能

## 快速安装

```bash
git clone https://github.com/YOUR_USERNAME/30x-seo-cn.git ~/.openclaw/skills/30x-seo
```

## 配置 DataForSEO（可选）

关键词研究、外链分析、AI 可见性监控需要 DataForSEO API。

### 1. 注册账号

访问 [app.dataforseo.com](https://app.dataforseo.com) 注册。

### 2. 获取 API 凭据

Settings → API Access → 复制邮箱和密码。

### 3. 生成 Base64 凭据

```bash
echo -n "你的邮箱:你的API密码" | base64
```

### 4. 保存凭据

```bash
mkdir -p ~/.config/dataforseo
echo "生成的Base64字符串" > ~/.config/dataforseo/auth
chmod 600 ~/.config/dataforseo/auth
```

### 5. 验证配置

```bash
curl -s -X POST "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -H "Authorization: Basic $(cat ~/.config/dataforseo/auth)" \
  -H "Content-Type: application/json" \
  -d '[{"keyword": "seo", "limit": 1}]' | jq '.status_code'
# 返回 20000 = 成功
```

---

## 安装路径

| 组件 | 路径 |
|------|------|
| 主技能 | `~/.openclaw/skills/30x-seo/` |
| 子技能 | `~/.openclaw/skills/30x-seo/skills/30x-seo-*/` |
| 子代理 | `~/.openclaw/skills/30x-seo/agents/seo-*.md` |
| 文档 | `~/.openclaw/skills/30x-seo/docs/` |

---

## 验证安装

1. 启动 Claude Code：

```bash
claude
```

2. 测试技能：

```
/seo
```

应该看到帮助信息或提示输入 URL。

3. 测试具体命令：

```
/seo technical https://example.com
```

---

## 可选：安装 Playwright

用于视觉分析和截图功能。

```bash
pip install playwright
playwright install chromium
```

如果 Playwright 未安装，视觉分析会使用 WebFetch 作为后备。

---

## 卸载

```bash
rm -rf ~/.openclaw/skills/30x-seo
```

---

## 升级

```bash
# 1. 备份配置
cp -r ~/.openclaw/skills/30x-seo ~/.openclaw/skills/30x-seo-backup

# 2. 删除旧版
rm -rf ~/.openclaw/skills/30x-seo

# 3. 安装新版
git clone https://github.com/YOUR_USERNAME/30x-seo-cn.git ~/.openclaw/skills/30x-seo
```

---

## 故障排除

### "技能未找到" 错误

确保技能安装在正确位置：

```bash
ls ~/.openclaw/skills/30x-seo/seo/SKILL.md
```

如果文件不存在，重新克隆仓库。

### DataForSEO 401 错误

检查凭据格式：

```bash
# 确保是 邮箱:密码 格式，用冒号分隔
echo -n "邮箱:密码" | base64

# 确保文件没有换行符
cat -A ~/.config/dataforseo/auth
```

### Playwright 截图错误

安装 Chromium 浏览器：

```bash
playwright install chromium
```

### 权限错误（Unix）

确保脚本可执行：

```bash
chmod +x ~/.openclaw/skills/30x-seo/scripts/*.py
chmod +x ~/.openclaw/skills/30x-seo/hooks/*.py
```

---

## 技能依赖一览

| 技能类别 | 数量 | 依赖 |
|----------|------|------|
| 技术 SEO | 8 | WebFetch（内置）|
| 内容优化 | 8 | WebFetch（内置）|
| 关键词/SERP/外链 | 3 | DataForSEO API |
| AI 可见性 | 2 | DataForSEO API |

**16 个技能无需任何 API 配置即可使用。**
