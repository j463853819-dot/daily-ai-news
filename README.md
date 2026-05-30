# Daily AI News

English | [中文](#中文说明)

Daily AI News is a Codex Skill for creating a reliable daily AI industry briefing. It collects recent AI news from web sources, verifies key facts, writes a structured Markdown report, and can optionally publish the result to WeChat Official Account drafts or sync it to Feishu/Lark Docs.

The public version does not include personal QR codes, private document links, API keys, or local machine paths. Bring your own publishing configuration if you want to use WeChat or Feishu/Lark.

## What It Does

- Collects recent AI news from primary sources, credible media, company blogs, papers, releases, and public statements.
- Deduplicates repeated coverage of the same event.
- Verifies dates, source links, funding numbers, model names, quotes, and sensitive claims.
- Generates a polished Markdown report in Chinese by default.
- Optionally creates a WeChat Official Account draft.
- Optionally syncs the report to a Feishu/Lark document.

## Folder Structure

```text
daily-ai-news/
├── SKILL.md
├── README.md
├── .env.example
└── references/
    ├── configuration.md
    ├── feishu-sync.md
    ├── format.md
    ├── sources.md
    └── wechat-publish.md
```

## Installation

Copy the `daily-ai-news` folder into your Codex skills directory.

Typical location:

```bash
~/.codex/skills/daily-ai-news
```

Then restart Codex or reload your skills, depending on your environment.

## Basic Usage

Ask Codex something like:

```text
Run today's AI daily news report.
```

Or in Chinese:

```text
帮我跑一下今天的 AI 日报。
```

By default, the Skill generates a Markdown report only:

```text
ai-news-YYYY-MM-DD.md
```

## Output Modes

You can ask for different modes:

```text
Generate today's AI news report only.
```

```text
Generate today's AI news and sync it to Feishu.
```

```text
Generate today's AI news and create a WeChat draft.
```

```text
Run the full workflow: report, WeChat draft, and Feishu sync.
```

Supported modes:

| Mode | Result |
| --- | --- |
| `report` | Generate Markdown only. |
| `wechat` | Generate Markdown and create a WeChat draft. |
| `feishu` | Generate Markdown and sync to Feishu/Lark Docs. |
| `all` | Run all configured steps. |

## Configuration

Copy `.env.example` to `.env` in the workspace where you run the workflow:

```bash
cp .env.example .env
```

Fill only the services you need.

For Markdown-only usage, no API keys are required.

For WeChat publishing, configure:

```env
WECHAT_APP_ID=
WECHAT_APP_SECRET=
WECHAT_DEFAULT_COVER=
WECHAT_HTTP_PROXY=
```

For Feishu/Lark sync, configure:

```env
FEISHU_DOC_URL=
LARK_CLI_PATH=lark-cli
LARK_CLI_IDENTITY=user
FEISHU_INSERT_MODE=append
FEISHU_TARGET_BLOCK_ID=
```

Feishu/Lark sync requires `lark-cli` to be installed and authenticated in your local environment before running the workflow.

See `references/configuration.md` for more details.

## Safety Notes

- Do not commit `.env`.
- Do not commit API keys, access tokens, private document URLs, or account-specific assets.
- The Skill creates WeChat drafts by design. It should not mass-send or publish publicly unless you explicitly request that behavior and your publishing tool supports it.
- Feishu/Lark sync should default to `append` unless you know the target document structure.

## Report Style

The default report is concise, analytical, and written in Chinese. It avoids generic AI-sounding phrasing and focuses on why each news item matters.

See `references/format.md` for the report template.

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

Daily AI News 是一个用于生成每日 AI 行业资讯简报的 Codex Skill。它可以从网络信源采集近期 AI 新闻，校验关键信息，生成结构清晰的 Markdown 日报，并可选同步到微信公众号草稿箱或飞书/Lark 文档。

这个公开版本不包含个人二维码、私有飞书链接、API 密钥或本机路径。如果你需要发布到公众号或飞书，请使用自己的配置。

## 它能做什么

- 从官方博客、可信媒体、论文、开源发布、公司公告、公开人物发言中采集 AI 新闻。
- 按真实事件去重，避免同一新闻被多个标题重复收录。
- 校验日期、来源链接、融资金额、模型名称、人物引述和敏感信息。
- 默认生成中文 Markdown 日报。
- 可选生成微信公众号草稿。
- 可选同步到飞书/Lark 文档。

## 目录结构

```text
daily-ai-news/
├── SKILL.md
├── README.md
├── .env.example
└── references/
    ├── configuration.md
    ├── feishu-sync.md
    ├── format.md
    ├── sources.md
    └── wechat-publish.md
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

默认情况下，它只会生成 Markdown 文件：

```text
ai-news-YYYY-MM-DD.md
```

## 输出模式

你可以指定不同输出方式：

```text
只生成今天的 AI 日报。
```

```text
生成今天的 AI 日报，并同步到飞书。
```

```text
生成今天的 AI 日报，并创建微信公众号草稿。
```

```text
跑完整流程：生成日报、创建公众号草稿、同步飞书。
```

支持的模式：

| 模式 | 结果 |
| --- | --- |
| `report` | 只生成 Markdown。 |
| `wechat` | 生成 Markdown，并创建微信公众号草稿。 |
| `feishu` | 生成 Markdown，并同步到飞书/Lark 文档。 |
| `all` | 执行所有已配置的步骤。 |

## 配置方式

在运行工作流的目录中，把 `.env.example` 复制为 `.env`：

```bash
cp .env.example .env
```

只填写你需要使用的服务。

如果只是生成 Markdown 日报，不需要任何 API 密钥。

如果需要发布到微信公众号草稿箱，配置：

```env
WECHAT_APP_ID=
WECHAT_APP_SECRET=
WECHAT_DEFAULT_COVER=
WECHAT_HTTP_PROXY=
```

如果需要同步到飞书/Lark，配置：

```env
FEISHU_DOC_URL=
LARK_CLI_PATH=lark-cli
LARK_CLI_IDENTITY=user
FEISHU_INSERT_MODE=append
FEISHU_TARGET_BLOCK_ID=
```

同步到飞书/Lark 之前，需要先在本地安装并完成 `lark-cli` 登录授权。仅配置文档链接还不够。

更多说明见 `references/configuration.md`。

## 安全提醒

- 不要提交 `.env`。
- 不要提交 API 密钥、访问令牌、私有文档链接或账号专属素材。
- 默认只建议创建微信公众号草稿，不建议直接群发或公开发布，除非你明确要求且你的发布工具支持。
- 飞书/Lark 同步在不了解文档结构时，建议使用 `append`。

## 日报风格

默认日报是中文，风格清晰、克制、有判断，不做机械翻译，也不堆砌空泛结论。每条新闻都应该解释“发生了什么”和“为什么重要”。

日报模板见 `references/format.md`。

## 校验原则

这个 Skill 的目标不是堆满新闻，而是减少旧闻、重复新闻和未经证实的传言。

它应该：

- 优先使用官方公告和权威报道。
- 排除被包装成今日新闻的旧内容。
- 避免未经证实的传闻。
- 每条精选新闻都保留直接 URL。
- 对无法确认的信息选择跳过，或明确标注不确定。

信源与事实校验规则见 `references/sources.md`。
