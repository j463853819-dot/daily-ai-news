---
name: daily-ai-news
description: Generate a verified daily AI news briefing as a structured Markdown report. Use when the user asks for AI daily news, AI news roundup, AI industry briefing, AI热点日报, 每日AI资讯, AI日报, or wants recent AI news collected, verified, deduplicated, and written into Markdown.
---

# Daily AI News

Create a reliable daily AI news briefing in Markdown. The core task ends when the Markdown report is generated. Publishing to Feishu/Lark, WeChat, a website, or any other channel is downstream work that should only happen when the user explicitly asks for it.

## Principles

- Prioritize accuracy over speed. Verify dates, original sources, company names, model names, funding amounts, and quoted statements.
- Prefer primary or authoritative sources: company blogs, research papers, official repositories, regulatory filings, credible media, and direct social posts.
- Do not invent news, quotes, rankings, dates, or links. If a claim cannot be verified, exclude it or mark it clearly as unconfirmed.
- Deduplicate by underlying event rather than headline.
- Use fewer strong items instead of padding the report with weak or stale news.

## Workflow

### 1. Confirm Scope

Use today's local date unless the user gives a specific date or date range.

Default output:

```text
ai-news-YYYY-MM-DD.md
```

If the user asks for a different language, output path, or section structure, follow that request while preserving verification quality.

### 2. Collect Sources

Use available web search and fetch tools to collect news published or meaningfully updated within the target date window.

Recommended source mix:

- Primary sources: OpenAI, Anthropic, Google DeepMind, Meta AI, Microsoft, NVIDIA, xAI, Mistral, Hugging Face, GitHub releases, arXiv, company blogs.
- Technology media: The Verge, TechCrunch, VentureBeat, The Information, MIT Technology Review, 36Kr, Sina Tech, AITNT, AI newsletters.
- Business sources: company announcements, funding databases, reputable business media, investor or regulatory materials.
- Public figures: direct posts, interviews, keynote transcripts, or reliable coverage of statements by industry leaders.

For source strategy and verification rules, read `references/sources.md` when collecting news.

### 3. Select and Verify

Build a candidate list, then keep only the items with enough source support and editorial value.

For each selected item, track:

- Title
- Category
- Summary angle
- Source URL
- Publication date or evidence that the event is current
- Verification note for sensitive claims such as funding, layoffs, legal issues, model performance, and quotes

Target 18-25 strong items. Use fewer if the day is quiet.

### 4. Write the Markdown Report

Use the structure in `references/format.md`.

Writing standards:

- Write in clear Chinese by default, unless the user asks for another language.
- Use concise analysis, not mechanical translation.
- Explain why the item matters, not just what happened.
- Keep each item grounded in at least one direct URL.
- Avoid generic AI phrasing such as "值得注意的是", "可以预见", "总而言之", and unsupported grand conclusions.

### 5. Final Response

Tell the user:

- Where the Markdown report was created.
- How many items were selected.
- Which important sources failed or could not be verified, if any.
- That downstream publishing or rendering can be done next if the user wants it.

## Optional Downstream Work

Do not sync, publish, or render the report unless the user explicitly asks.

Common downstream choices:

- Sync the Markdown report to Feishu/Lark Docs.
- Convert the Markdown report into an HTML briefing page.
- Adapt the report for WeChat Official Account drafts.
- Convert the report into another editorial or publishing format.

If the user asks for an HTML page, use `references/html-style.md` as the visual style guide unless they provide another design.

## Failure Handling

| Situation | Response |
| --- | --- |
| Source page unavailable | Search for an archived, official, or second authoritative source. |
| News date unclear | Exclude it unless it is clearly relevant to the target date. |
| Duplicate coverage | Keep the strongest source and merge useful context. |
| Quote cannot be traced | Do not quote it; summarize only what is verified. |
| Quiet news day | Publish fewer items and say the selection was intentionally conservative. |
