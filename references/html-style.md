# HTML Briefing Style Guide

Use this guide only when the user explicitly asks to convert a generated Markdown report into an HTML page.

The core Skill output remains Markdown. HTML rendering is an optional downstream format.

## Design Direction

The briefing should feel like a clean editorial digest, not a dark dashboard.

Use:

- White or near-white background.
- Dark readable text.
- Compact cards with soft borders.
- Restrained accent colors.
- Clear section rhythm.
- Source links that are easy to copy.
- A mobile-friendly single-column layout.

Avoid:

- Black or dark full-page background.
- Heavy gradients.
- Neon colors.
- Large decorative blobs or ornamental backgrounds.
- Overly tall cards with weak information density.

## Layout

Recommended page structure:

```html
<body>
  <main class="page">
    <header class="hero">
      <p class="eyebrow">AI Daily Briefing</p>
      <h1>AI 圈今日动态</h1>
      <p class="date">2026 年 5 月 31 日</p>
      <div class="summary">今日三条主线...</div>
    </header>

    <section class="section">
      <div class="section-heading">
        <span class="section-icon">🔥</span>
        <h2>重磅</h2>
      </div>
      <article class="item">
        <div class="item-topline">
          <span class="item-num">01</span>
          <span class="tag tag-hot">重磅</span>
        </div>
        <h3>新闻标题</h3>
        <p>新闻说明...</p>
        <div class="source-row">
          <span>Source</span>
          <code>https://example.com</code>
          <button>复制</button>
        </div>
      </article>
    </section>
  </main>
</body>
```

## CSS Reference

This CSS is intentionally plain and self-contained. Adapt colors and spacing as needed.

```css
:root {
  color-scheme: light;
  --bg: #f7f8fb;
  --panel: #ffffff;
  --text: #172033;
  --muted: #667085;
  --line: #e5e7ef;
  --soft-line: #eff1f6;
  --blue: #2563eb;
  --red: #dc2626;
  --green: #16a34a;
  --amber: #d97706;
  --purple: #7c3aed;
  --pink: #db2777;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC",
    "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
  line-height: 1.72;
}

a {
  color: var(--blue);
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

.page {
  width: min(860px, calc(100% - 32px));
  margin: 0 auto;
  padding: 32px 0 48px;
}

.hero {
  padding: 28px 0 24px;
  border-bottom: 1px solid var(--line);
  margin-bottom: 28px;
}

.eyebrow {
  margin: 0 0 8px;
  color: var(--blue);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0;
  text-transform: uppercase;
}

.hero h1 {
  margin: 0;
  font-size: clamp(28px, 5vw, 42px);
  line-height: 1.18;
  letter-spacing: 0;
}

.date {
  margin: 10px 0 0;
  color: var(--muted);
  font-size: 14px;
}

.summary {
  margin-top: 18px;
  padding: 14px 16px;
  background: #eef4ff;
  border: 1px solid #d9e6ff;
  border-radius: 8px;
  color: #24406f;
  font-size: 15px;
}

.section {
  margin-top: 34px;
}

.section-heading {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 14px;
  padding-bottom: 10px;
  border-bottom: 1px solid var(--line);
}

.section-icon {
  font-size: 20px;
}

.section h2 {
  margin: 0;
  font-size: 20px;
  line-height: 1.3;
}

.item {
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 8px;
  padding: 16px 18px;
  margin-bottom: 12px;
  box-shadow: 0 1px 2px rgba(16, 24, 40, 0.04);
}

.item:hover {
  border-color: #cfd6e4;
}

.item-topline {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  align-items: center;
  margin-bottom: 8px;
}

.item-num {
  color: #98a2b3;
  font-size: 12px;
  font-weight: 700;
}

.item h3 {
  margin: 0;
  color: var(--text);
  font-size: 17px;
  line-height: 1.45;
}

.item p {
  margin: 9px 0 0;
  color: #344054;
  font-size: 14.5px;
}

.tag {
  flex-shrink: 0;
  border-radius: 999px;
  padding: 3px 9px;
  font-size: 12px;
  font-weight: 700;
}

.tag-hot { background: #fee2e2; color: var(--red); }
.tag-model { background: #dbeafe; color: var(--blue); }
.tag-insight { background: #fef3c7; color: var(--amber); }
.tag-business { background: #ede9fe; color: var(--purple); }
.tag-product { background: #dcfce7; color: var(--green); }
.tag-policy { background: #fce7f3; color: var(--pink); }

.source-row {
  display: grid;
  grid-template-columns: auto 1fr auto;
  gap: 8px;
  align-items: center;
  margin-top: 12px;
  padding: 8px 10px;
  background: #f8fafc;
  border: 1px solid var(--soft-line);
  border-radius: 6px;
}

.source-row span {
  color: var(--muted);
  font-size: 12px;
  font-weight: 700;
}

.source-row code {
  overflow: hidden;
  color: #475467;
  font-family: "SF Mono", "Cascadia Code", "Fira Code", monospace;
  font-size: 12px;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.source-row button {
  border: 1px solid #c7d7fe;
  border-radius: 6px;
  background: #eef4ff;
  color: var(--blue);
  cursor: pointer;
  font: inherit;
  font-size: 12px;
  font-weight: 700;
  padding: 4px 8px;
}

.source-row button:hover {
  background: #dbeafe;
}

.footer {
  margin-top: 36px;
  padding-top: 18px;
  border-top: 1px solid var(--line);
  color: var(--muted);
  font-size: 12px;
  text-align: center;
}

@media (max-width: 640px) {
  .page {
    width: min(100% - 24px, 860px);
    padding-top: 20px;
  }

  .hero h1 {
    font-size: 28px;
  }

  .item {
    padding: 14px;
  }

  .source-row {
    grid-template-columns: 1fr auto;
  }

  .source-row span {
    display: none;
  }
}
```

## Interaction

If the page includes copy buttons, use a small, unobtrusive script:

```html
<script>
function copySource(button, url) {
  navigator.clipboard.writeText(url).then(function () {
    var old = button.textContent;
    button.textContent = "已复制";
    setTimeout(function () {
      button.textContent = old;
    }, 1600);
  });
}
</script>
```

## Content Mapping

Map Markdown sections to visual tags:

| Markdown Section | Suggested Tag |
| --- | --- |
| 🔥 重磅 | `tag-hot` |
| 🚀 模型 & 技术突破 | `tag-model` |
| 💡 深度洞见 | `tag-insight` |
| 💰 融资 & 商业 | `tag-business` |
| 🛠️ 工具 & 产品 | `tag-product` |
| 🔍 行业 & 治理 | `tag-policy` |
