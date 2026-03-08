# 架构设计

## 概览

30x SEO 遵循 Anthropic 官方 Claude Code 技能规范，采用模块化、多技能架构。

## 目录结构

```
~/.openclaw/skills/30x-seo/
├── seo/                         # 主编排技能
│   ├── SKILL.md                     # 入口 + 路由逻辑
│   └── references/                  # 按需加载的参考文件
│       ├── cwv-thresholds.md
│       ├── schema-types.md
│       ├── eeat-framework.md
│       └── quality-gates.md
│
├── skills/                      # 21 个 SEO 技能
│   ├── 30x-seo-technical/           # 技术 SEO
│   ├── 30x-seo-content-audit/       # 内容 E-E-A-T 分析
│   ├── 30x-seo-schema/              # Schema 结构化数据
│   ├── 30x-seo-sitemap/             # Sitemap 分析/生成
│   ├── 30x-seo-hreflang/            # 多语言 SEO
│   ├── 30x-seo-images/              # 图片优化
│   ├── 30x-seo-redirects/           # 重定向分析
│   ├── 30x-seo-internal-links/      # 内链分析
│   ├── 30x-seo-geo-technical/       # AI 爬虫管理
│   ├── 30x-seo-content-brief/       # 内容简报
│   ├── 30x-seo-content-writer/      # 写作指南
│   ├── 30x-seo-content-decay/       # 内容衰退检测
│   ├── 30x-seo-cannibalization/     # 关键词蚕食
│   ├── 30x-seo-page/                # 单页分析
│   ├── 30x-seo-competitor-pages/    # 竞品对比
│   ├── 30x-seo-programmatic/        # 程序化 SEO
│   ├── 30x-seo-keywords/            # 关键词研究
│   ├── 30x-seo-serp/                # SERP 分析
│   ├── 30x-seo-backlinks/           # 外链分析
│   ├── 30x-seo-ai-visibility/       # AI 可见性监控
│   └── 30x-seo-plan/                # 战略规划
│       └── assets/                      # 行业模板
│
├── agents/                      # 6 个子代理（并行执行）
│   ├── seo-technical.md
│   ├── seo-content.md
│   ├── seo-schema.md
│   ├── seo-sitemap.md
│   ├── seo-performance.md
│   └── seo-visual.md
│
├── schema/                      # JSON-LD 模板
│
└── docs/                        # 文档
    ├── COMMANDS.md
    ├── ARCHITECTURE.md
    ├── TROUBLESHOOTING.md
    ├── MCP-INTEGRATION.md
    └── INSTALLATION.md
```

## 组件类型

### 技能（Skills）

技能是带有 YAML frontmatter 的 Markdown 文件，定义能力和指令。

**SKILL.md 格式：**
```yaml
---
name: skill-name
description: >
  何时使用此技能。包含激活关键词
  和具体用例。
allowed-tools:
  - WebFetch
  - Bash
---

# 技能标题

指令和文档...

[PROTOCOL]: 变更时更新此头部
```

### 子代理（Subagents）

子代理是可委托任务的专业执行者。拥有独立上下文和工具。

**Agent 格式：**
```yaml
---
name: agent-name
description: 此代理的功能。
tools: Read, Bash, Write, Glob, Grep
---

代理指令...
```

### 参考文件（Reference Files）

参考文件包含按需加载的静态数据，避免主技能膨胀。

## 编排流程

### 全站审计 (`/seo audit`)

```
用户请求
    │
    ▼
┌─────────────────┐
│   seo           │  ← 主编排器
│   (SKILL.md)    │
└────────┬────────┘
         │
         │  检测业务类型
         │  并行启动子代理
         │
    ┌────┴────┬────────┬────────┬────────┬────────┐
    ▼         ▼        ▼        ▼        ▼        ▼
┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐
│技术   │ │内容   │ │Schema │ │Sitemap│ │性能   │ │视觉   │
│代理   │ │代理   │ │代理   │ │代理   │ │代理   │ │代理   │
└───┬───┘ └───┬───┘ └───┬───┘ └───┬───┘ └───┬───┘ └───┬───┘
    │         │        │        │        │        │
    └─────────┴────────┴────┬───┴────────┴────────┘
                            │
                            ▼
                    ┌───────────────┐
                    │  汇总结果     │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────┐
                    │  生成报告     │
                    └───────────────┘
```

### 单一命令

```
用户请求（如 /seo page）
    │
    ▼
┌─────────────────┐
│   seo           │  ← 路由到子技能
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   seo-page      │  ← 子技能直接处理
│   (SKILL.md)    │
└─────────────────┘
```

## 设计原则

### 1. 渐进式披露

- 主 SKILL.md 简洁（<200 行）
- 参考文件按需加载
- 详细指令在子技能中

### 2. 并行处理

- 子代理在审计时并发运行
- 独立分析互不阻塞
- 全部完成后汇总结果

### 3. 质量门控

- 内置阈值防止糟糕建议
- 位置页面限制（30 警告，50 硬停止）
- Schema 废弃感知
- FID → INP 替换强制执行

### 4. 行业感知

- 不同业务类型的模板
- 从首页信号自动检测
- 按行业定制建议

## 文件命名约定

| 类型 | 模式 | 示例 |
|------|------|------|
| 技能 | `30x-seo-{name}/SKILL.md` | `30x-seo-technical/SKILL.md` |
| 代理 | `seo-{name}.md` | `seo-technical.md` |
| 参考 | `{topic}.md` | `cwv-thresholds.md` |
| 脚本 | `{action}_{target}.py` | `fetch_page.py` |
| 模板 | `{industry}.md` | `saas.md` |

## 扩展点

### 添加新子技能

1. 创建 `skills/30x-seo-newskill/SKILL.md`
2. 添加包含 name 和 description 的 YAML frontmatter
3. 编写技能指令
4. 更新主 `seo/SKILL.md` 路由到新技能

### 添加新子代理

1. 创建 `agents/seo-newagent.md`
2. 添加包含 name、description、tools 的 YAML frontmatter
3. 编写代理指令
4. 在相关技能中引用

### 添加新参考文件

1. 在适当的 `references/` 目录创建文件
2. 在技能中用按需加载指令引用

## 依赖关系图

```
┌──────────────────────────────────────────────────────────┐
│                    Claude Code 内置                       │
│  WebFetch │ Read │ Write │ Glob │ Grep │ Bash │ Task    │
└──────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────┐
│                    30x SEO 技能                           │
├──────────────────────────────────────────────────────────┤
│  技术 SEO (8)  │  内容优化 (8)  │  关键词/外链 (3)  │  AI (2)  │
│  仅 WebFetch   │  仅 WebFetch   │  DataForSEO API   │  DataForSEO │
└──────────────────────────────────────────────────────────┘
```

**16 个技能无需任何 API 配置即可使用。**
