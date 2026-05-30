---
name: daily-ai-news
description: Generate a daily AI news briefing from verified web sources, format it as a structured Markdown report, and optionally publish it to WeChat Official Account drafts or sync it to Feishu/Lark Docs. Use when the user asks for AI daily news, AI news roundup, AI industry briefing, AI热点日报, 每日AI资讯, AI日报, or asks to collect and distribute recent AI news.
---

# Daily AI News

Create a reliable daily AI news briefing: collect recent AI news, verify key facts, select the most relevant items, write a polished Markdown report, then optionally publish it to configured channels.

## Principles

- Prioritize accuracy over speed. Verify dates, original sources, company names, model names, funding amounts, and quoted statements.
- Prefer primary or authoritative sources: company blogs, research papers, official repositories, regulatory filings, credible media, and direct social posts.
- Do not invent news, quotes, rankings, dates, or links. If a claim cannot be verified, exclude it or mark it clearly as unconfirmed.
- Keep publishing optional. A user may only want a Markdown report, a Feishu sync, a WeChat draft, or the full workflow.
- Never expose secrets. Read credentials from environment variables or a local `.env` file, and do not write them into generated reports.

## Workflow

### 1. Confirm Scope

Use today's local date unless the user gives a specific date or date range.

Decide the output mode from the user request:

- `report`: generate Markdown only.
- `wechat`: generate Markdown and create a WeChat Official Account draft.
- `feishu`: generate Markdown and sync to Feishu/Lark Docs.
- `all`: generate Markdown, create WeChat draft, and sync to Feishu/Lark Docs.

If the user does not specify a mode, default to `report`.

### 2. Collect Sources

Use available web search and fetch tools to collect news published or meaningfully updated within the target date window.

Recommended source mix:

- Primary sources: OpenAI, Anthropic, Google DeepMind, Meta AI, Microsoft, NVIDIA, xAI, Mistral, Hugging Face, GitHub releases, arXiv, company blogs.
- Technology media: The Verge, TechCrunch, VentureBeat, The Information, MIT Technology Review, 36Kr, Sina Tech, AITNT, AI newsletters.
- Business sources: company announcements, funding databases, reputable business media, investor or regulatory materials.
- Public figures: direct posts, interviews, keynote transcripts, or reliable coverage of statements by industry leaders.

For source strategy and verification rules, read `references/sources.md` when collecting news.

### 3. Select and Verify

Build a candidate list, then deduplicate by underlying event rather than headline.

For each selected item, keep:

- Title
- Category
- Summary angle
- Source URL
- Publication date or evidence that the event is current
- Verification note for sensitive claims such as funding, layoffs, legal issues, model performance, and quotes

Target 18-25 strong items. Use fewer if the day is quiet; do not pad with weak or stale news.

### 4. Write the Report

Create `ai-news-YYYY-MM-DD.md` in the working directory unless the user requests another path.

Use the format in `references/format.md`.

Writing standards:

- Write in clear Chinese by default, unless the user asks for another language.
- Use concise analysis, not mechanical translation.
- Explain why the item matters, not just what happened.
- Keep each item grounded in at least one direct URL.
- Avoid generic AI phrasing such as "值得注意的是", "可以预见", "总而言之", and unsupported grand conclusions.

### 5. Optional: Publish to WeChat

Only publish when the user asks for WeChat output or mode is `wechat` or `all`.

Before publishing, read `references/wechat-publish.md`.

Required configuration is documented in `references/configuration.md`.

After publishing, report the draft status and returned draft or media identifier if available.

### 6. Optional: Sync to Feishu/Lark

Only sync when the user asks for Feishu/Lark output or mode is `feishu` or `all`.

Before syncing, read `references/feishu-sync.md`.

Required configuration is documented in `references/configuration.md`.

After syncing, report the target document and whether the operation succeeded.

### 7. Final Response

Tell the user:

- Where the Markdown report was created.
- How many candidate items were reviewed and how many were selected, if known.
- Which channels were published or skipped.
- Any verification gaps or failed sources.

## Configuration

For portable usage, copy `.env.example` to `.env` and fill only the channels you plan to use.

Never commit `.env`, credentials, private document URLs, local access tokens, or personal QR codes.

Read `references/configuration.md` before running publication or sync steps.

## Failure Handling

| Situation | Response |
| --- | --- |
| Source page unavailable | Search for an archived, official, or second authoritative source. |
| News date unclear | Exclude it unless it is clearly relevant to the target date. |
| Duplicate coverage | Keep the strongest source and merge useful context. |
| Quote cannot be traced | Do not quote it; summarize only what is verified. |
| WeChat credentials missing | Generate the Markdown report and explain that WeChat publishing was skipped. |
| Feishu/Lark auth expired | Ask the user to re-authenticate locally, then retry sync if possible. |
| Publication partially succeeds | Preserve the Markdown report and report the exact failed channel. |
