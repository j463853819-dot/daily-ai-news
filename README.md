# Daily AI News

English | [中文](#中文说明)

Daily AI News is a Codex Skill for creating a verified daily AI industry briefing as a Markdown report.

The core job is simple:

1. Collect recent AI news.
2. Verify the important facts.
3. Deduplicate repeated coverage.
4. Write a structured Markdown briefing.

Everything after Markdown, such as syncing to Feishu/Lark, rendering an HTML page, or preparing a WeChat draft, is optional downstream work that users can choose based on their own publishing setup.

## What It Does

- Collects recent AI news from primary sources, credible media, company blogs, papers, releases, and public statements.
- Deduplicates repeated coverage of the same event.
- Verifies dates, source links, funding numbers, model names, quotes, and sensitive claims.
- Generates a polished Markdown report in Chinese by default.
- Keeps publishing decisions separate from the core news-generation workflow.

## What It Does Not Do By Default

- It does not automatically sync to Feishu/Lark.
- It does not automatically publish to WeChat.
- It does not automatically generate HTML.
- It does not include personal QR codes, private document links, API keys, or local machine paths.

Users can still ask Codex to perform those downstream steps after the Markdown report is generated.

## Folder Structure

```text
daily-ai-news/
├── SKILL.md
├── README.md
├── .gitignore
└── references/
    ├── format.md
    ├── html-style.md
    └── sources.md
```

## Installation

Copy the `daily-ai-news` folder into your Codex skills directory.

Typical location:

```bash
~/.codex/skills/daily-ai-news
```

Then restart Codex or reload your skills, depending on your environment.

## Basic Usage

Ask Codex:

```text
Run today's AI daily news report.
```

Or in Chinese:

```text
帮我跑一下今天的 AI 日报。
```

By default, the Skill generates:

```text
ai-news-YYYY-MM-DD.md
```

## Report Style

The default report is concise, analytical, and written in Chinese. It avoids generic AI-sounding phrasing and focuses on why each news item matters.

See `references/format.md` for the Markdown report template.

## Optional: Sync To Feishu/Lark

After the Markdown report is generated, users may ask Codex to sync it to Feishu/Lark.

This requires the user's own Feishu/Lark environment:

- `lark-cli` must already be installed locally.
- The user must already be authenticated with `lark-cli`.
- The user must provide their own target document or wiki URL.
- The user should choose an insertion strategy, such as append, insert before a block, or replace a date section.

The Skill does not ship with any private Feishu document URL or account-specific setup.

Example request:

```text
把今天生成的 AI 日报同步到我的飞书文档。
```

## Optional: Generate An HTML Page

After the Markdown report is generated, users may ask Codex to convert it into an HTML briefing page.

The recommended visual direction is:

- White background.
- Clean editorial layout.
- Compact cards.
- Soft borders and subtle section colors.
- Clear source links that are easy to copy.
- Mobile-friendly reading experience.

See `references/html-style.md` for a white-background style guide inspired by the included briefing example.

Example request:

```text
把今天生成的 AI 日报转成 HTML 页面。
```

## Optional: Prepare A WeChat Draft

Users may also adapt the Markdown report for WeChat Official Account drafts if they have their own publishing script or API setup.

The Skill does not include WeChat credentials or a bundled publishing pipeline.

## Safety Notes

- Do not commit API keys, access tokens, private document URLs, or account-specific assets.
- Do not commit generated reports unless you intentionally want to publish examples.
- Verify sensitive claims before using the report in a public channel.
- For Feishu/Lark sync, avoid overwriting a whole document unless you are certain about the target range.

## Verification Philosophy

This Skill is designed to reduce stale, duplicated, or speculative AI news.

It should:

- Prefer original announcements and authoritative reporting.
- Exclude old news repackaged as today's update.
- Avoid unverified rumors.
- Use direct URLs for every selected item.
- Clearly skip or mark claims that cannot be confirmed.

See `references/sources.md` for source and verification guidance.

---

# 中文说明

Daily AI News 是一个用于生成每日 AI 行业资讯简报的 Codex Skill。它的核心任务是生成一份经过采集、校验、去重和整理的 Markdown 日报。

核心流程很简单：

1. 采集近期 AI 新闻。
2. 校验关键信息。
3. 合并重复报道。
4. 生成结构清晰的 Markdown 日报。

Markdown 之后的动作，比如同步到飞书/Lark、生成 HTML 页面、整理成微信公众号草稿，都属于用户可自行选择的后续发布流程。

## 它能做什么

- 从官方博客、可信媒体、论文、开源发布、公司公告、公开人物发言中采集 AI 新闻。
- 按真实事件去重，避免同一新闻被多个标题重复收录。
- 校验日期、来源链接、融资金额、模型名称、人物引述和敏感信息。
- 默认生成中文 Markdown 日报。
- 把“生成内容”和“发布到哪里”分开，避免 Skill 绑定某个私有账号或平台。

## 默认不做什么

- 默认不同步飞书/Lark。
- 默认不发布微信公众号。
- 默认不生成 HTML。
- 不包含个人二维码、私有飞书链接、API 密钥或本机路径。

如果用户需要，这些都可以在 Markdown 生成后再让 Codex 继续处理。

## 目录结构

```text
daily-ai-news/
├── SKILL.md
├── README.md
├── .gitignore
└── references/
    ├── format.md
    ├── html-style.md
    └── sources.md
```

## 安装方式

把 `daily-ai-news` 文件夹复制到你的 Codex skills 目录。

常见路径：

```bash
~/.codex/skills/daily-ai-news
```

然后重启 Codex，或根据你的环境重新加载 Skills。

## 基础用法

你可以这样对 Codex 说：

```text
帮我跑一下今天的 AI 日报。
```

默认情况下，它会生成：

```text
ai-news-YYYY-MM-DD.md
```

## 日报风格

默认日报是中文，风格清晰、克制、有判断，不做机械翻译，也不堆砌空泛结论。每条新闻都应该解释“发生了什么”和“为什么重要”。

日报模板见 `references/format.md`。

## 可选：同步到飞书/Lark

Markdown 日报生成后，用户可以继续让 Codex 同步到飞书/Lark。

这需要用户自己的飞书/Lark 环境：

- 本地需要已经安装 `lark-cli`。
- 本地需要已经完成 `lark-cli` 登录授权。
- 用户需要提供自己的目标文档或知识库 URL。
- 用户需要选择插入方式，比如追加、插入到某个块之前，或替换某一天的日报段落。

这个 Skill 不内置任何私有飞书文档链接或账号配置。

示例：

```text
把今天生成的 AI 日报同步到我的飞书文档。
```

## 可选：生成 HTML 页面

Markdown 日报生成后，用户也可以继续让 Codex 把它转成 HTML 页面。

推荐视觉方向：

- 白色背景。
- 清爽的编辑型排版。
- 紧凑的信息卡片。
- 柔和边框和低饱和分区色。
- 来源链接清晰，方便复制。
- 移动端阅读友好。

HTML 样式参考见 `references/html-style.md`。这份样式基于原有简报页面做了白底化和阅读体验调整。

示例：

```text
把今天生成的 AI 日报转成 HTML 页面。
```

## 可选：整理成微信公众号草稿

如果用户有自己的微信公众号发布脚本或 API 配置，也可以把 Markdown 日报继续整理成公众号草稿。

这个 Skill 不内置微信公众号凭证，也不绑定任何发布流水线。

## 安全提醒

- 不要提交 API 密钥、访问令牌、私有文档链接或账号专属素材。
- 不要提交生成的日报，除非你明确希望把它作为示例公开。
- 公开发布前，需要再次确认敏感信息和事实来源。
- 同步飞书/Lark 时，不要在不确定范围的情况下覆盖整篇文档。

## 校验原则

这个 Skill 的目标不是堆满新闻，而是减少旧闻、重复新闻和未经证实的传言。

它应该：

- 优先使用官方公告和权威报道。
- 排除被包装成今日新闻的旧内容。
- 避免未经证实的传闻。
- 每条精选新闻都保留直接 URL。
- 对无法确认的信息选择跳过，或明确标注不确定。

信源与事实校验规则见 `references/sources.md`。
