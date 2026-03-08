# TODO — 30x SEO

## v1.2.0 已完成

- [x] **修复 YAML frontmatter 解析** — 移除 8 个文件中 `---` 前的 HTML 注释
- [x] **SSRF 防护** — fetch_page.py 和 analyze_visual.py 添加私有 IP 阻止
- [x] **安装加固** — 基于 venv 的 pip，移除 `--break-system-packages`
- [x] **Windows 安装修复** — `python -m pip`、`py -3` 回退、requirements.txt 持久化
- [x] **requirements.txt 持久化** — 安装后复制到技能目录
- [x] **路径遍历防护** — capture_screenshot.py 输出路径清理，parse_html.py 文件验证

## 待办事项

- [ ] **减少 agents 的 Bash 权限范围**（优先级：中）
  评估哪些 agents 真正需要 Bash 访问。考虑用 WebFetch 替代。

- [ ] **Docker 沙箱执行**（优先级：低）
  为需要额外隔离的用户在 Docker 中沙箱运行 Python 脚本。

- [ ] **Opencode 兼容性**（优先级：低）
  适配 Opencode 的技能架构。

- [ ] **子代理超时/压缩处理**（优先级：中）
  主代理有时在子代理完成前终止。考虑鼓励子代理运行 /compact 并添加显式等待逻辑。

- [ ] **原生 Chrome 工具 vs Playwright**（优先级：中）
  Claude Code 有原生浏览器自动化。评估用内置工具替换 Playwright 以消除 ~200MB Chromium 依赖。

## 研究报告待办

- [ ] **虚假新鲜度检测**（优先级：中）
  比较可见日期（`datePublished`、`dateModified`）与实际内容修改信号。
  标记更新日期但正文未变的页面。

- [ ] **移动端内容一致性检查**（优先级：中）
  比较移动端 vs 桌面端的 meta 标签、结构化数据和内容完整性。
  标记可能影响移动优先索引的差异。

- [ ] **Discover 优化检查**（优先级：低-中）
  标题党检测、内容深度评分、本地相关性信号、煽情标记。

- [ ] **品牌提及分析 Python 实现**（优先级：低）
  目前在 `seo-geo/SKILL.md` 中有文档，但无程序化评分。

---

*最后更新：2026年3月*
