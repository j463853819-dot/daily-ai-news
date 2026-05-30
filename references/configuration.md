# Configuration

Copy `.env.example` to `.env` in the workspace where the workflow runs. Fill only the channels you need.

## Common

- `DAILY_AI_NEWS_OUTPUT_DIR`: where generated Markdown reports should be saved. Defaults to the current working directory.
- `DAILY_AI_NEWS_LANGUAGE`: report language. Defaults to `zh-CN`.
- `DAILY_AI_NEWS_TIMEZONE`: timezone used for date selection. Example: `Asia/Shanghai`.

## WeChat Official Account

- `WECHAT_APP_ID`: Official Account app ID.
- `WECHAT_APP_SECRET`: Official Account app secret.
- `WECHAT_DEFAULT_COVER`: media ID or URL for the default cover image, depending on the publishing script.
- `WECHAT_HTTP_PROXY`: optional proxy for environments where WeChat API access requires a fixed outbound IP.

Do not commit these values.

## Feishu/Lark

Feishu/Lark sync requires `lark-cli` to be installed and authenticated before use.

- `FEISHU_DOC_URL`: target document or wiki URL.
- `LARK_CLI_PATH`: path to `lark-cli`. Defaults to `lark-cli` if it is available in `PATH`.
- `LARK_CLI_IDENTITY`: usually `user` for personal document sync or `bot` for bot-owned documents.
- `FEISHU_INSERT_MODE`: recommended values are `append`, `insert_before`, or `insert_after`, depending on the document structure.
- `FEISHU_TARGET_BLOCK_ID`: required only for insert modes that need a target block.

For public distribution, never include a private Feishu document URL in the skill.

## Local Files

Generated outputs should be safe to commit only after review. Do not commit:

- `.env`
- access tokens
- generated logs containing tokens
- private draft IDs if they reveal account information
- personal QR codes or private account promotion images
